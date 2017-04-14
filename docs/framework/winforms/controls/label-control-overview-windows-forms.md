---
title: "Cenni preliminari sul controllo Label (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Label"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "immagini [Windows Form], visualizzazione in etichette"
  - "Label (controllo) [Windows Form], informazioni sul controllo Label"
  - "etichette"
ms.assetid: dcad7f44-11b7-4c55-b0c0-d984ade43d7d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul controllo Label (Windows Form)
I controlli <xref:System.Windows.Forms.Label> Windows Form vengono utilizzati per visualizzare testo o immagini non modificabili dall'utente.  La loro funzione consiste nell'identificare gli oggetti in un form per fornire una descrizione, ad esempio, dell'azione di un determinato controllo quando viene selezionato o per visualizzare informazioni in risposta a un evento o processo in fase di esecuzione dell'applicazione.  Si possono utilizzare etichette per aggiungere didascalie descrittive a caselle di testo, caselle di riepilogo, caselle combinate e così via.  È inoltre possibile scrivere il codice per modificare il testo visualizzato da un'etichetta in risposta a eventi in fase di esecuzione.  Se ad esempio l'applicazione in uso impiega alcuni minuti per elaborare una modifica, è possibile visualizzare un messaggio relativo all'elaborazione all'interno di un'etichetta.  
  
## Utilizzo del controllo Label  
 Poiché il controllo <xref:System.Windows.Forms.Label> non può ricevere lo stato attivo, è utilizzabile anche per la creazione di tasti di scelta per altri controlli.  Un tasto di scelta consente di scegliere l'altro controllo premendo contemporaneamente ALT e il tasto assegnato.  Per ulteriori informazioni, vedere [Creazione di tasti di scelta per i controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md) e [Procedura: creare tasti di scelta con i controlli Label di Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md).  
  
 La didascalia visualizzata nell'etichetta fa parte della proprietà <xref:System.Windows.Forms.Label.Text%2A>.  La proprietà <xref:System.Windows.Forms.Label.TextAlign%2A> consente di impostare l'allineamento del testo all'interno dell'etichetta.  Per ulteriori informazioni, vedere [Procedura: impostare il testo visualizzato da un controllo di Windows Form](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.Label>   
 [Procedura: ridimensionare un controllo Label Windows Form in base al contenuto](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)   
 [Procedura: creare tasti di scelta con i controlli Label di Windows Form](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md)