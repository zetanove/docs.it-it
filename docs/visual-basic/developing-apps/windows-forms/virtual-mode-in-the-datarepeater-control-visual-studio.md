---
title: "Virtual Mode in the DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "virtual data binding"
  - "DataRepeater"
  - "DataRepeater, virtual mode"
ms.assetid: 5fb805dc-2d8b-4139-b1e3-86e4c2667221
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Virtual Mode in the DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per visualizzare quantità elevate di dati in formato tabulare in un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, è possibile migliorare le prestazioni impostando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> su `True` e gestendo in modo esplicito l'interazione del controllo con la relativa origine dati.  Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> fornisce diversi eventi che è possibile gestire per interagire con l'origine dati e visualizzare i dati secondo necessità in fase di esecuzione.  
  
## Funzionamento della modalità virtuale  
 Nello scenario più comune per il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, i controlli figlio di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> vengono associati in fase di progettazione a un'origine dati e viene consentito il passaggio dei dati da parte di <xref:System.Windows.Forms.BindingSource> secondo necessità.  Quando si utilizza la modalità virtuale, i controlli non vengono associati a un'origine dati e i dati vengono passati in fase di esecuzione all'origine dati sottostante e viceversa.  
  
 Quando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> è impostata su `True`, è possibile creare l'interfaccia utente aggiungendo controlli dalla **Casella degli strumenti** anziché controlli associati dalla finestra **Origini dati**.  
  
 Gli eventi vengono generati per i singoli controlli ed è necessario aggiungere codice per gestire la visualizzazione dei dati.  Quando si scorre nella visualizzazione un nuovo oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>, l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> viene generato una volta per ciascun controllo. È necessario fornire i valori per ciascun controllo nel gestore eventi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>.  
  
 Se i dati di uno dei controlli vengono modificati dall'utente, viene generato l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> ed è necessario convalidare i dati e salvarli nell'origine dati.  
  
 In caso di aggiunta di un nuovo elemento da parte dell'utente, viene generato l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>.  Utilizzare il gestore di questo evento per creare un nuovo record nell'origine dati.  Per impedire che vengano apportate modifiche non intenzionali, è inoltre necessario monitorare l'evento <xref:System.Windows.Forms.Control.KeyDown> per ciascun controllo ed eseguire la chiamata a <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> se viene premuto il tasto ESC.  
  
 Se l'origine dati viene modificata, è possibile aggiornare il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> chiamando i metodi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetTemplateItem%2A> e <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetTemplateItem%2A>.  È necessario chiamare i metodi nell'ordine specificato.  
  
 Infine, è necessario implementare gestori eventi per l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved> che si verifica quando un elemento viene eliminato e, facoltativamente, per gli eventi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletingItems> e <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletedItems> che si verificano ogni volta che viene eliminato un elemento premendo il tasto CANC.  
  
## Implementazione della modalità virtuale  
 Di seguito sono riportati i passaggi necessari per l'implementazione della modalità virtuale.  
  
#### Per implementare la modalità virtuale  
  
1.  Trascinare un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> dalla scheda **Visual Basic Power Pack 1.1** della **Casella degli strumenti** a un form o un controllo contenitore.  Impostare la proprietà<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>su `True`.  
  
2.  Trascinare i controlli dalla **Casella degli strumenti** all'area del modello di elemento \(l'area superiore\) del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Sarà necessario un controllo per ciascun campo dell'origine dati che si desidera visualizzare.  
  
3.  Implementare un gestore per l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> per fornire valori per ciascun controllo.  L'evento viene generato quando si scorre nella visualizzazione un nuovo oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.  L'aspetto del codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterVirtualMode/VbPowerPacksDataRepeaterVirtualMode.vb#1)]
     [!code-cs[VbPowerPacksDataRepeaterVirtualMode#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksDataRepeaterVirtualModeCS/VbPowerPacksDataRepeaterVirtualMode.cs#1)]  
  
4.  Implementare un gestore per l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> per archiviare i dati.  L'evento viene generato quando si esegue il commit delle modifiche apportate a un controllo figlio di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.  L'aspetto del codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterVirtualMode/VbPowerPacksDataRepeaterVirtualMode.vb#2)]
     [!code-cs[VbPowerPacksDataRepeaterVirtualMode#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksDataRepeaterVirtualModeCS/VbPowerPacksDataRepeaterVirtualMode.cs#2)]  
  
5.  Implementare un gestore per ciascun evento <xref:System.Windows.Forms.Control.KeyDown> del controllo figlio e monitorare il tasto ESC.  Eseguire la chiamata al metodo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> per impedire che venga generato l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>.  L'aspetto del codice sarà simile all'esempio seguente.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode#3](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterVirtualMode/VbPowerPacksDataRepeaterVirtualMode.vb#3)]
     [!code-cs[VbPowerPacksDataRepeaterVirtualMode#3](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksDataRepeaterVirtualModeCS/VbPowerPacksDataRepeaterVirtualMode.cs#3)]  
  
6.  Implementare un gestore per l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>.  L'evento viene generato in caso di aggiunta di un nuovo elemento al controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> da parte dell'utente.  L'aspetto del codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode#4](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterVirtualMode/VbPowerPacksDataRepeaterVirtualMode.vb#4)]
     [!code-cs[VbPowerPacksDataRepeaterVirtualMode#4](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksDataRepeaterVirtualModeCS/VbPowerPacksDataRepeaterVirtualMode.cs#4)]  
  
7.  Implementare un gestore per l'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>.  L'evento viene generato in caso di eliminazione di un elemento esistente da parte dell'utente.  L'aspetto del codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode#5](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterVirtualMode/VbPowerPacksDataRepeaterVirtualMode.vb#5)]
     [!code-cs[VbPowerPacksDataRepeaterVirtualMode#5](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksDataRepeaterVirtualModeCS/VbPowerPacksDataRepeaterVirtualMode.cs#5)]  
  
8.  Per la convalida a livello di controllo, è possibile implementare gestori per gli eventi <xref:System.Windows.Forms.Control.Validating> dei controlli figlio.  L'aspetto del codice sarà simile all'esempio seguente.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode#6](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterVirtualMode/VbPowerPacksDataRepeaterVirtualMode.vb#6)]
     [!code-cs[VbPowerPacksDataRepeaterVirtualMode#6](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksDataRepeaterVirtualModeCS/VbPowerPacksDataRepeaterVirtualMode.cs#6)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)