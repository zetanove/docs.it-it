---
title: "Procedura: ereditare dalla classe Control | Microsoft Docs"
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
  - "Control (classe), ereditare da"
  - "controlli personalizzati [Windows Form], creazione"
  - "controlli personalizzati [Windows Form], ereditarietà"
  - "ereditarietà, Windows Form (controlli personalizzati)"
  - "OnPaint (metodo) [Windows Form]"
ms.assetid: 46ba0df3-5cf7-443c-a3b4-a72660172476
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: ereditare dalla classe Control
Per creare un controllo completamente personalizzato da utilizzare in Windows Form, è necessario ereditarlo dalla classe <xref:System.Windows.Forms.Control>.  Benché richieda pianificazione e implementazione più ampie, l'eredità dalla classe <xref:System.Windows.Forms.Control> offre la più vasta gamma di opzioni.  Dalla classe <xref:System.Windows.Forms.Control> si eredita la funzionalità di base che consente di attivare i controlli.  La funzionalità intrinseca alla classe <xref:System.Windows.Forms.Control> consente di gestire l'input dell'utente tramite tastiera e mouse, definire i limiti e le dimensioni del controllo, fornire un handle di finestre nonché la gestione e la sicurezza dei messaggi.  Non consente di incorporare alcun disegno, ossia il rendering effettivo dell'interfaccia grafica del controllo, né alcuna funzionalità di interazione utente specifica.  È necessario fornire questi aspetti tramite codice personalizzato.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un controllo personalizzato  
  
1.  Creare un nuovo progetto **Applicazione Windows** o **Libreria di controlli Windows**.  
  
2.  Scegliere **Aggiungi classe** dal menu **Progetto**.  
  
3.  Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **Controllo personalizzato**.  
  
     Un nuovo controllo personalizzato verrà aggiunto al progetto.  
  
4.  Premere F7 per aprire l'**editor di codice** per il controllo personalizzato.  
  
5.  Individuare il metodo <xref:System.Windows.Forms.Control.OnPaint%2A>, che sarà vuoto a eccezione di una chiamata al metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base.  
  
6.  Modificare il codice in modo da incorporare il disegno personalizzato per il controllo.  
  
     Per informazioni sulla scrittura del codice per il rendering della grafica dei controlli, vedere [Disegno e rendering di controlli personalizzati](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md).  
  
7.  Implementare eventuali metodi, proprietà o eventi personalizzati da incorporare nel controllo.  
  
8.  Salvare ed eseguire il test del controllo.  
  
## Vedere anche  
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [Procedura: ereditare dalla classe UserControl](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [Procedura: ereditare da controlli di Windows Form esistenti](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [Procedura: creare controlli per Windows Form](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [Troubleshooting Inherited Event Handlers in Visual Basic](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)   
 [Sviluppo di controlli Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)