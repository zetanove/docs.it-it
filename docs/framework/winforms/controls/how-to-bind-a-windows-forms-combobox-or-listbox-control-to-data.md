---
title: "Procedura: associare a dati un controllo ComboBox o ListBox Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli con associazione, caselle combinate"
  - "caselle combinate, associazione dati"
  - "ComboBox (controllo) [Windows Form], associazione dati"
  - "dati [Windows Form], associazione a controlli"
  - "associazione dati, caselle combinate"
  - "controlli con associazione a dati, Windows Form"
  - "caselle di riepilogo, associazione dati"
  - "ListBox (controllo) [Windows Form], associazione dati"
  - "controlli Windows Form, associazione dati"
ms.assetid: dfd7f081-8bea-4a41-86a3-86a1934828ef
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: associare a dati un controllo ComboBox o ListBox Windows Form
È possibile associare a dati i controlli <xref:System.Windows.Forms.ComboBox> e <xref:System.Windows.Forms.ListBox> per eseguire attività quali l'esplorazione di dati in un database, l'immissione di nuovi dati o la modifica di dati esistenti.  
  
### Per associare un controllo ComboBox o ListBox  
  
1.  Impostare la proprietà `DataSource` su un oggetto origine dati.  Le origini dati possono essere costituite da una classe <xref:System.Windows.Forms.BindingSource> associata a dati, una tabella di dati, una visualizzazione dati, un dataset, un gestore di visualizzazione dati, una matrice o qualsiasi classe che implementa l'interfaccia <xref:System.Collections.IList>.  Per ulteriori informazioni, vedere [Origini dati supportate da Windows Form](../../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md).  
  
2.  Se si effettua l'associazione a una tabella, impostare la proprietà `DisplayMember` sul nome di una colonna nell'origine dati.  
  
     \- oppure \-  
  
     Se si effettua l'associazione a un'interfaccia <xref:System.Collections.IList>, impostare il membro di visualizzazione su una proprietà pubblica del tipo nell'elenco.  
  
    ```vb  
    Private Sub BindComboBox()  
      ComboBox1.DataSource = DataSet1.Tables("Suppliers")  
      ComboBox1.DisplayMember = "ProductName"  
    End Sub  
  
    ```  
  
    ```csharp  
    private void BindComboBox()  
    {  
      comboBox1.DataSource = dataSet1.Tables["Suppliers"];  
      comboBox1.DisplayMember = "ProductName";  
    }  
  
    ```  
  
    > [!NOTE]
    >  Se è stata effettuata l'associazione a un'origine dati che non implementa l'interfaccia <xref:System.ComponentModel.IBindingList>, ad esempio una classe <xref:System.Collections.ArrayList>, i dati del controllo associato non verranno aggiornati contestualmente all'aggiornamento dell'origine dati.  Se ad esempio una casella combinata è associata a una classe <xref:System.Collections.ArrayList> e a tale classe vengono aggiunti dati, questi nuovi elementi non appariranno nella casella combinata.  È tuttavia possibile forzare l'aggiornamento della casella combinata chiamando i metodi <xref:System.Windows.Forms.BindingManagerBase.SuspendBinding%2A> e <xref:System.Windows.Forms.BindingManagerBase.ResumeBinding%2A> sull'istanza della classe <xref:System.Windows.Forms.BindingContext> cui il controllo è associato.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Associazione dati e Windows Form](../../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Controlli Windows Form usati per elencare opzioni](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)