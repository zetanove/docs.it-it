---
title: "Procedura: associare un controllo Windows Form a un tipo mediante la finestra di progettazione | Microsoft Docs"
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
  - "BindingSource (componente) [Windows Form], associazione a un tipo"
  - "controlli [Windows Form], associazione a un tipo"
  - "tipi [Windows Form], associazione dei controlli"
ms.assetid: 5ab984b5-c2d0-4638-a572-1c84013e8746
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: associare un controllo Windows Form a un tipo mediante la finestra di progettazione
Quando si compilano controlli che interagiscono con dati, è a volte necessario associare un controllo a un tipo anziché a un oggetto.  In genere si preferisce associare un controllo a un tipo in fase di progettazione, quando i dati potrebbero non essere disponibili, ma si desidera che nei controlli associati a dati vengano comunque visualizzati i dati dell'interfaccia pubblica di un tipo.  Nella procedura descritta di seguito viene illustrato come creare un nuovo componente <xref:System.Windows.Forms.BindingSource> associato a un tipo, quindi come associare una delle proprietà del tipo alla proprietà <xref:System.Windows.Forms.TextBox.Text%2A> di una classe <xref:System.Windows.Forms.TextBox>.  
  
### Per associare il componente BindingSource a un tipo  
  
1.  Creare un progetto Windows Form.  
  
     Per ulteriori informazioni, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Nella visualizzazione **Progettazione** trascinare un componente <xref:System.Windows.Forms.BindingSource> nel form.  
  
3.  Nella finestra **Proprietà** fare clic sulla freccia relativa alla proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A>.  
  
4.  Nell'editor del tipo di interfaccia utente **DataSource** fare clic su **Aggiungi origine dati progetto**.  
  
5.  Nella pagina **Seleziona un tipo di origine dati** selezionare **Oggetto** e fare clic su **Avanti**.  
  
6.  Selezionare il tipo con cui si desidera creare un'associazione:  
  
    -   Se il tipo con cui si desidera creare un'associazione è nel progetto corrente o se l'assembly che contiene il tipo è già stato aggiunto come riferimento, espandere i nodi per trovare il tipo desiderato, quindi selezionarlo.  
  
         In alternativa  
  
    -   Se il tipo che si desidera associare è in un altro assembly, attualmente non presente nell'elenco di riferimenti, fare clic su **Aggiungi riferimento**, quindi sulla scheda **Progetti**.  Selezionare il progetto contenente l'oggetto business desiderato e fare clic su **OK**.  Poiché il progetto verrà visualizzato nell'elenco di assembly, sarà possibile espandere i nodi per trovare il tipo desiderato e selezionarlo.  
  
        > [!NOTE]
        >  Se si desidera associare un tipo in un framework o assembly Microsoft, deselezionare la casella di controllo **Nascondi assembly che iniziano con Microsoft o System**.  
  
7.  Fare clic su **Avanti**, quindi su **Fine**.  
  
### Per associare il controllo al componente BindingSource  
  
1.  Aggiungere una classe <xref:System.Windows.Forms.TextBox> al form.  
  
2.  Nella finestra **Proprietà** espandere il nodo **\(DataBindings\)**.  
  
3.  Fare clic sulla freccia posta accanto alla proprietà <xref:System.Windows.Forms.TextBox.Text%2A>.  
  
4.  Nell'editor del tipo di interfaccia utente **DataSource** espandere il nodo relativo al componente <xref:System.Windows.Forms.BindingSource> precedentemente aggiunto e selezionare la proprietà del tipo associato che si desidera associare alla proprietà <xref:System.Windows.Forms.TextBox.Text%2A> della classe <xref:System.Windows.Forms.TextBox>.  
  
## Vedere anche  
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Procedura: associare un controllo Windows Form a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)   
 [Associazione di controlli ai dati in Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)