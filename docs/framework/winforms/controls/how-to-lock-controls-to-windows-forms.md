---
title: "Procedura: bloccare i controlli di un Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], blocco"
  - "controlli Windows Form, blocco"
ms.assetid: 94efe0d2-c14e-4d14-b903-63ea9b07e290
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: bloccare i controlli di un Windows Form
Durante la progettazione dell'interfaccia utente di un'applicazione Windows è possibile bloccare i controlli, una volta posizionati correttamente, in modo che non vengano spostati o ridimensionati inavvertitamente quando si impostano altre proprietà.  
  
 È inoltre possibile bloccare e sbloccare tutti i controlli sul form contemporaneamente, operazione che risulta particolarmente vantaggiosa in caso di form con numerosi controlli, oppure sbloccare singoli controlli.  Una volta posizionati tutti i controlli nei punti desiderati del form, bloccarli in modo da evitare spostamenti indesiderati.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per bloccare un controllo  
  
1.  Nella finestra **Proprietà** fare clic sulla proprietà **Locked** e selezionare `true`.  Facendo doppio clic sul nome si attiva o si disattiva l'impostazione della proprietà.  
  
     In alternativa, fare clic sul controllo con il pulsante destro del mouse e scegliere **Blocca controlli**.  
  
    > [!NOTE]
    >  Il blocco dei controlli ne impedisce il trascinamento per modificarne le dimensioni o la posizione nell'area di progettazione.  È tuttavia possibile modificare le dimensioni o la posizione dei controlli mediante la finestra **Proprietà** oppure nel codice.  
  
### Per bloccare tutti i controlli in un form  
  
1.  Scegliere **Blocca controlli** dal menu **Formato**.  
  
    > [!NOTE]
    >  Questo comando blocca anche le dimensioni del form, dato che il form stesso è un controllo.  
  
### Per sbloccare tutti i controlli bloccati in un form  
  
1.  Scegliere **Blocca controlli** dal menu **Formato**.  
  
     Tutti i controlli precedentemente bloccati nel form vengono sbloccati.  
  
### Per sbloccare singolarmente i controlli bloccati  
  
1.  Nella finestra **Proprietà** fare clic sulla proprietà **Locked** e selezionare `false`.  Facendo doppio clic sul nome si attiva o si disattiva l'impostazione della proprietà.  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Impostazione delle etichette di singoli controlli Windows Form e creazione dei relativi tasti di scelta rapida](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)