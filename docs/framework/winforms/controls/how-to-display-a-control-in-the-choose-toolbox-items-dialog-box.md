---
title: "Procedura: visualizzare un controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti | Microsoft Docs"
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
  - "Global Assembly Cache, finestra di dialogo Scegli elementi della Casella degli strumenti"
  - "AssemblyFoldersEx, finestra di dialogo Scegli elementi della Casella degli strumenti"
  - "controlli, visualizzazione nella finestra di dialogo Scegli elementi della Casella degli strumenti"
  - "registrazione cartella dell'assembly, finestra di dialogo Scegli elementi della Casella degli strumenti"
  - "Finestra di dialogo Scegli elementi della Casella degli strumenti, visualizzazione controllo"
ms.assetid: 01ef6eba-d044-40f0-951d-78eff7ebd9a9
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: visualizzare un controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti
Quando si sviluppano e distribuiscono controlli, è possibile fare in modo che tali controlli siano riportati nella finestra di dialogo **Scegli elementi della Casella degli strumenti**, visualizzata facendo clic con il pulsante destro del mouse su **Casella degli strumenti** e scegliendo **Scegli elementi**.  Per visualizzare il controllo in questa finestra di dialogo, utilizzare la procedura di registrazione AssemblyFoldersEx.  
  
### Per visualizzare il controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti  
  
-   Installare l'assembly del controllo nella Global Assembly Cache.  Per ulteriori informazioni, vedere [Procedura: installare un assembly nella Global Assembly Cache](../../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)  
  
     In alternativa  
  
-   Registrare il controllo e gli assembly della fase di progettazione correlati tramite la procedura di registrazione AssemblyFoldersEx.  AssemblyFoldersEx è un percorso del Registro di sistema in cui i fornitori di terze parti archiviano i percorsi per ogni versione del framework che supportano.  La risoluzione della fase di progettazione può cercare in questo percorso del Registro di sistema per trovare gli assembly di riferimento.  Lo script del Registro di sistema può specificare i controlli che si desidera visualizzare nella casella degli strumenti.  Per ulteriori informazioni, vedere [Distribuzione di un controllo personalizzato e di assembly della fase di progettazione](http://msdn.microsoft.com/it-it/96158eb0-b691-4ae1-9e7b-3c65a1b798cb).  
  
## Vedere anche  
 [Choose Toolbox Items Dialog Box \(Visual Studio\)](http://msdn.microsoft.com/it-it/bd07835f-18a8-433e-bccc-7141f65263bb)   
 [Distribuzione di un controllo personalizzato e di assembly della fase di progettazione](http://msdn.microsoft.com/it-it/96158eb0-b691-4ae1-9e7b-3c65a1b798cb)   
 [Sviluppo di controlli Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [Procedura: installare un assembly nella Global Assembly Cache](../../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)   
 [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)