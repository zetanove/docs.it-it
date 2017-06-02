---
title: "Procedura: ereditare dalla classe UserControl | Microsoft Docs"
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
  - "controlli composti, creazione"
  - "ereditarietà, Windows Form (controlli personalizzati)"
  - "controlli utente [Windows Form], creazione"
  - "UserControl (classe), ereditare da"
ms.assetid: 67713625-e2e4-4f6a-bce7-0855ee5043d9
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: ereditare dalla classe UserControl
Per combinare la funzionalità di uno o più controlli Windows Form con codice personalizzato, è possibile creare un *controllo utente*.  I controlli utente combinano lo sviluppo rapido, funzionalità standard dei controlli Windows Form, con la versatilità delle proprietà e dei metodi personalizzati.  Quando si inizia a creare un controllo utente, viene visualizzata una finestra di progettazione in cui è possibile inserire i controlli standard Windows Form  che conservano tutta la funzionalità intrinseca nonché l'aspetto e il comportamento dei controlli standard,  ma, una volta incorporati nel controllo utente, non sono più disponibili mediante codice.  Il controllo utente esegue il proprio disegno e gestisce inoltre tutta la funzionalità di base associata ai controlli.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un controllo utente  
  
1.  Creare un nuovo progetto **Libreria di controlli Windows**.  
  
     Viene creato un nuovo progetto con un controllo utente vuoto.  
  
2.  Trascinare i controlli dalla scheda **Windows Form** della **Casella degli strumenti** nella finestra di progettazione.  
  
3.  Posizionare e progettare questi controlli nel modo in cui si desidera che vengano visualizzati nel controllo utente finale.  Per consentire agli sviluppatori di accedere ai controlli costitutivi, è necessario dichiararli come Public o esporne le proprietà in modo selettivo.  Per informazioni dettagliate, vedere [Procedura: esporre le proprietà dei controlli costitutivi](../../../../docs/framework/winforms/controls/how-to-expose-properties-of-constituent-controls.md).  
  
4.  Implementare eventuali metodi o proprietà personalizzate da incorporare nel controllo.  
  
5.  Per compilare il progetto ed eseguire il controllo in **UserControl Test Container**, premere F5.  Per ulteriori informazioni, vedere [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md).  
  
## Vedere anche  
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [Procedura: ereditare dalla classe Control](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [Procedura: ereditare da controlli di Windows Form esistenti](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [Procedura: creare controlli per Windows Form](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [Troubleshooting Inherited Event Handlers in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)   
 [Procedura: eseguire il test del comportamento in fase di esecuzione di UserControl](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)