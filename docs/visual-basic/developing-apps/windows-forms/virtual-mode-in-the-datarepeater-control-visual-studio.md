---
title: "Modalità virtuale nel controllo DataRepeater (Visual Studio) | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- virtual data binding
- DataRepeater
- DataRepeater, virtual mode
ms.assetid: 5fb805dc-2d8b-4139-b1e3-86e4c2667221
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 85f7e250c57a507e891eb30756c0550098cce9e0
ms.lasthandoff: 03/13/2017

---
# <a name="virtual-mode-in-the-datarepeater-control-visual-studio"></a>Modalità virtuale nel controllo DataRepeater (Visual Studio)
Quando si desidera visualizzare quantità elevate di dati tabulari in un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo, è possibile migliorare le prestazioni impostando la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>proprietà `True` e gestendo in modo esplicito l'interazione del controllo con l'origine dati.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo fornisce diversi eventi che è possibile gestire per interagire con l'origine dati e visualizzare i dati in base alle necessità in fase di esecuzione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>  
  
## <a name="how-virtual-mode-works"></a>Funzionamento della modalità virtuale  
 Lo scenario più comune per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo consiste nell'associare i controlli figlio del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A>per dati di origine in fase di progettazione e consentire il <xref:System.Windows.Forms.BindingSource>per passare i dati e viceversa in base alle esigenze.</xref:System.Windows.Forms.BindingSource> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Quando si utilizza la modalità virtuale, i controlli non associati a un'origine dati e i dati vengono passati avanti e indietro all'origine dati sottostante in fase di esecuzione.  
  
 Quando il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>è impostata su `True`, si crea l'interfaccia utente aggiungendo i controlli dal **della casella degli strumenti** invece di aggiungere controlli associati dal **origini dati** finestra.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>  
  
 Gli eventi vengono generati in modo da controlli e aggiungere il codice per gestire la visualizzazione dei dati. Quando un nuovo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>mostrata nella visualizzazione di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>evento viene generato una volta per ogni controllo ed è necessario fornire i valori per ogni controllo il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>gestore dell'evento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>  
  
 Se uno dei controlli di dati verrà modificato dall'utente, il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>viene generato l'evento ed è necessario convalidare i dati e salvarlo con l'origine dati.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>  
  
 Se l'utente aggiunge un nuovo elemento, il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>viene generato l'evento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded> Utilizzare il gestore dell'evento per creare un nuovo record nell'origine dati. Per evitare modifiche impreviste, è necessario monitorare il <xref:System.Windows.Forms.Control.KeyDown>evento per ogni controllo e chiamare <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A>Se l'utente preme il tasto ESC.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> </xref:System.Windows.Forms.Control.KeyDown>  
  
 Se l'origine dati le modifiche, è possibile aggiornare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo chiamando la <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A>e <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A>metodi.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Entrambi i metodi devono essere chiamati in ordine.  
  
 Infine, è necessario implementare i gestori eventi per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>evento che si verifica quando viene eliminato un elemento e, facoltativamente, per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletingItems>e <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletedItems>che si verificano ogni volta che un utente elimina un elemento premendo il tasto CANC.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletedItems> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.UserDeletingItems> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>  
  
## <a name="implementing-virtual-mode"></a>Implementazione della modalità virtuale  
 Di seguito sono i passaggi necessari per implementare la modalità virtuale.  
  
#### <a name="to-implement-virtual-mode"></a>Per implementare la modalità virtuale  
  
1.  Trascinare un <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>da controllare il **Visual Basic Power Packs** nella scheda il **della casella degli strumenti** a un form o un controllo contenitore.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Impostare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>proprietà `True`.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.VirtualMode%2A>  
  
2.  Trascinare i controlli dal **della casella degli strumenti** area del modello di elemento (l'area superiore) del <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> È necessario un controllo per ogni campo dell'origine dati che si desidera visualizzare.  
  
3.  Implementare un gestore per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>evento per fornire valori per ogni controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded> Questo evento viene generato quando un nuovo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>viene scorso nella visualizzazione.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> Il codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[N.&1; VbPowerPacksDataRepeaterVirtualMode](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_1.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode n.&1;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_1.cs)]  
  
4.  Implementare un gestore per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>archiviare i dati dell'evento.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> Questo evento viene generato quando l'utente esegue il commit delle modifiche a un controllo figlio di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> Il codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[N.&2; VbPowerPacksDataRepeaterVirtualMode](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_2.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode n.&2;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_2.cs)]  
  
5.  Implementare un gestore per ogni controllo figlio <xref:System.Windows.Forms.Control.KeyDown>eventi e monitorare il tasto ESC.</xref:System.Windows.Forms.Control.KeyDown> Chiamare il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A>per impedire il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>eventi vengano generati.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed> </xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CancelEdit%2A> Il codice sarà simile all'esempio seguente.  
  
     [!code-vb[N.&3; VbPowerPacksDataRepeaterVirtualMode](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_3.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode n.&3;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_3.cs)]  
  
6.  Implementare un gestore per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>eventi.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded> Questo evento viene generato quando l'utente aggiunge un nuovo elemento per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>controllo.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> Il codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[N.&4; VbPowerPacksDataRepeaterVirtualMode](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_4.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode n.&4;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_4.cs)]  
  
7.  Implementare un gestore per il <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved>eventi.</xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemsRemoved> Questo evento si verifica quando un utente elimina un elemento esistente. Il codice sarà simile all'esempio seguente, che fa riferimento a un'origine dati denominata `Employees`.  
  
     [!code-vb[N.&5; VbPowerPacksDataRepeaterVirtualMode](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_5.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode n.&5;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_5.cs)]  
  
8.  Per la convalida a livello di controllo, è possibile implementare gestori per il <xref:System.Windows.Forms.Control.Validating>gli eventi dei controlli figlio.</xref:System.Windows.Forms.Control.Validating> Il codice sarà simile all'esempio seguente.  
  
     [!code-vb[VbPowerPacksDataRepeaterVirtualMode&6;](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/virtual-mode-in-the-datarepeater-control-visual-studio_6.vb) ] 
     [!code-cs [VbPowerPacksDataRepeaterVirtualMode n.&6;](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/virtual-mode-in-the-datarepeater-control-visual-studio_6.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValuePushed>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.NewItemNeeded>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded></xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemValueNeeded>   
 [Introduzione al controllo DataRepeater](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)
