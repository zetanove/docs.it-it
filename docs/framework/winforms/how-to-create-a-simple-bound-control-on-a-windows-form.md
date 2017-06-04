---
title: "Procedura: creare un controllo con associazione semplice in un Windows Form | Microsoft Docs"
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
  - "associazione dati, associazione dati semplice"
  - "controlli Windows Form, associazione dati"
ms.assetid: 3bcaded8-0f1a-4cc0-8830-f59be253bf4e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare un controllo con associazione semplice in un Windows Form
L'*associazione semplice* consente di visualizzare in un controllo un singolo elemento di dati, ad esempio il valore di una colonna in una tabella di DataSet.  È possibile eseguire un'associazione semplice di qualsiasi proprietà di un controllo a un valore dei dati.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per eseguire l'associazione semplice di un controllo  
  
1.  Connessione a un'origine dati.  Per ulteriori informazioni, vedere [Connessione a un'origine dati](../../../docs/framework/data/adonet/connecting-to-a-data-source.md).  
  
2.  Selezionare il controllo nel form e visualizzare la finestra **Proprietà**.  
  
3.  Espandere la proprietà **\(DataBindings\)**.  
  
     Le proprietà più frequentemente associate vengono visualizzate sotto la proprietà **\(DataBindings\)**.  Nella maggior parte dei controlli, ad esempio, la proprietà più frequentemente associata è **Text**.  
  
4.  Se la proprietà che si desidera associare non è una delle proprietà comunemente associate, fare clic sul pulsante dei **puntini di sospensione** \(![Schermata VisualStudioEllipsesButton](../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) nella casella **\(Avanzate\)** per visualizzare la finestra di dialogo **Formattazione e associazione avanzata** contenente l'elenco completo delle proprietà per tale controllo.  
  
5.  Selezionare la proprietà che si desidera associare e fare clic sulla freccia a discesa sotto **Binding**.  
  
     Verrà visualizzato un elenco di origini dati disponibili.  
  
6.  Espandere l'origine dati che si desidera associare fino a quando non vengono visualizzati i dati desiderati.  Se ad esempio si desidera associare il valore di una colonna in una tabella di dataset, espandere il nome del dataset, quindi espandere il nome della tabella per visualizzare i nomi delle colonne.  
  
7.  Fare clic sul nome dell'elemento a cui effettuare l'associazione.  
  
8.  Se si utilizza la finestra di dialogo **Formattazione e associazione avanzata**, scegliere **OK** per tornare nella finestra **Proprietà**.  
  
9. Se si desidera associare proprietà aggiuntive del controllo, ripetere i passaggi da 3 a 7.  
  
    > [!NOTE]
    >  Poiché i controlli con associazione semplice consentono di visualizzare un solo elemento di dati, in un Windows Form comprendente controlli con associazione semplice viene in genere incluso un sistema di navigazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Binding>   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)