---
title: "Procedura: garantire la sincronizzazione di pi&#249; controlli associati alla stessa origine dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form], associazione di più controlli"
  - "controlli [Windows Form], sincronizzazione con l'origine dati"
ms.assetid: c2f0ecc6-11e6-4c2c-a1ca-0759630c451e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: garantire la sincronizzazione di pi&#249; controlli associati alla stessa origine dati
Spesso quando si utilizza l'associazione dati in Windows Form, più controlli vengono associati alla stessa origine dati.  In alcuni casi, può essere necessario eseguire altri passaggi per assicurarsi che le proprietà associate dei controlli rimangano sincronizzate tra loro e con l'origine dati.  Questi passaggi sono necessari in due situazioni:  
  
-   Se l'origine dati non implementa <xref:System.ComponentModel.IBindingList> e pertanto genera gli eventi <xref:System.ComponentModel.IBindingList.ListChanged> di tipo <xref:System.ComponentModel.ListChangedType>.  
  
-   Se l'origine dati implementa <xref:System.ComponentModel.IEditableObject>.  
  
 Nel primo caso, è possibile utilizzare un componente <xref:System.Windows.Forms.BindingSource> per associare l'origine dati ai controlli.  Nel secondo caso, utilizzare un componente <xref:System.Windows.Forms.BindingSource>, gestire l'evento <xref:System.Windows.Forms.BindingSource.BindingComplete> ed eseguire una chiamata al metodo <xref:System.Windows.Forms.BindingManagerBase.EndCurrentEdit%2A> sul controllo <xref:System.Windows.Forms.BindingManagerBase> associato.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come associare tre controlli, ossia due controlli casella di testo e un controllo <xref:System.Windows.Forms.DataGridView>, alla stessa colonna di un controllo <xref:System.Data.DataSet> utilizzando un componente <xref:System.Windows.Forms.BindingSource>.  Viene descritto come gestire l'evento <xref:System.Windows.Forms.BindingSource.BindingComplete> e assicurarsi che, quando il valore di testo di una delle caselle di testo viene modificato, l'altra casella di testo e il controllo <xref:System.Windows.Forms.DataGridView> vengano aggiornati con il valore corretto.  
  
 Nell'esempio si utilizza un componente <xref:System.Windows.Forms.BindingSource> per associare l'origine dati e i controlli.  In alternativa, è possibile associare i controlli direttamente all'origine dati e recuperare il componente <xref:System.Windows.Forms.BindingManagerBase> per l'associazione dalla proprietà <xref:System.Windows.Forms.Control.BindingContext%2A> del form, quindi gestire l'evento <xref:System.Windows.Forms.BindingManagerBase.BindingComplete> per <xref:System.Windows.Forms.BindingManagerBase>.  Per un esempio di come eseguire questa operazione, vedere la pagina Guida sull'evento <xref:System.Windows.Forms.BindingManagerBase.BindingComplete> di <xref:System.Windows.Forms.BindingManagerBase>.  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleControls#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleControls#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/VB/Form1.vb#1)]  
  
## Compilazione del codice  
  
-   Per questo esempio di codice sono necessari i seguenti requisiti  
  
-   Riferimenti agli assembly <xref:System>, <xref:System.Windows.Forms> e <xref:System.Drawing>.  
  
-   Un form con l'evento <xref:System.Windows.Forms.Form.Load> gestito e una chiamata al metodo `InitializeControlsAndDataSource` nell'esempio dal gestore eventi <xref:System.Windows.Forms.Form.Load> del form.  
  
## Vedere anche  
 [Procedura: condividere dati associati tra form tramite il componente BindingSource](../../../docs/framework/winforms/controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)   
 [Notifica delle modifiche nell'associazione dati dei Windows Form](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [Interfacce correlate all'associazione dati](../../../docs/framework/winforms/interfaces-related-to-data-binding.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)