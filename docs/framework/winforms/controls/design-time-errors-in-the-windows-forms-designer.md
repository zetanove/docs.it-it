---
title: "Errori in fase di progettazione in Progettazione Windows Form | Microsoft Docs"
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
  - "DTELErrorList"
  - "WhyDTELPage"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "fase di progettazione (errori) [Progettazione Windows Form]"
  - "errori [Progettazione Windows Form]"
ms.assetid: ad408380-825a-46d8-9a4a-531b130b88ce
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Errori in fase di progettazione in Progettazione Windows Form
In questo argomento vengono illustrati il significato e l'utilizzo dell'elenco degli errori in fase di progettazione visualizzato in Microsoft Visual Studio quando si verifica un errore di caricamento di Progettazione Windows Form.  Se viene visualizzato questo elenco errori, non deve essere interpretato come un bug nella finestra di progettazione, ma come strumento di supporto per risolvere gli errori nel codice.  
  
 Una conoscenza di base di questo elenco errori consentirà l'esecuzione del debug delle applicazioni fornendo informazioni dettagliate sugli errori e suggerendo le possibili soluzioni.  
  
## Interfaccia dell'elenco errori in fase di progettazione  
 Se Progettazione Windows Form non viene caricato correttamente, nella finestra di progettazione viene visualizzato un elenco errori.  Gli errori vengono raggruppati in categorie.  Ad esempio, se si hanno quattro istanze di variabili non dichiarate, queste verranno raggruppate nella stessa categoria di errore.  Ogni categoria di errore include una breve descrizione che riepiloga l'errore.  
  
 È possibile espandere o comprimere una categoria di errore facendo clic sull'intestazione della categoria di errore o facendo clic sulle virgolette acute di espansione\/compressione.  Quando si espande una categoria di errore, vengono visualizzate le seguenti informazioni aggiuntive:  
  
-   Istanze dell'errore  
  
-   Informazioni sull'errore  
  
-   Post dei forum sull'errore  
  
### Istanze dell'errore  
 Nelle informazioni aggiuntive vengono riportate tutte le istanze dell'errore nel progetto corrente.  Molti errori includono un percorso esatto nel formato seguente: *\[Nome progetto\]* *\[Nome form\]* Riga:*\[Numero riga\]* Colonna:*\[Numero colonna\]*.  Il collegamento **Vai al codice** consente di visualizzare la posizione all'interno del codice in cui si è verificato l'errore.  
  
 Se uno stack di chiamate è associato all'errore, è possibile fare clic sul collegamento **Mostra stack di chiamate** che espande ulteriormente l'errore per mostrare lo stack di chiamate.  L'analisi dello stack può fornire informazioni di debug particolarmente utili.  Ad esempio, è possibile registrare le funzioni chiamate prima del verificarsi dell'errore.  Lo stack di chiamate è selezionabile in modo da poter essere copiato e salvato.  
  
> [!NOTE]
>  In Visual Basic, nell'elenco errori in fase di progettazione viene visualizzato un solo errore; è possibile però visualizzare più istanze dello stesso errore.  In Visual C\+\+, gli errori non dispongono dei collegamenti Vai a codice o Numero riga.  
  
### Informazioni sull'errore  
 Se l'errore contiene un collegamento a un argomento della Guida MSDN associato, nelle informazioni aggiuntive verrà incluso un collegamento all'argomento della Guida.  Quando si fa clic sul collegamento, in Visual Studio verrà visualizzato l'argomento della Guida associato.  
  
### Post dei forum sull'errore  
 Nelle informazioni aggiuntive verrà incluso un collegamento ai post dei forum MSDN relativi all'errore.  La ricerca nei forum viene eseguita in base alla stringa del messaggio di errore.  È inoltre possibile provare a eseguire la ricerca nei forum seguenti:  
  
-   [Forum di Progettazione Windows Form](http://go.microsoft.com/fwlink/?LinkId=203524)  
  
-   [Forum di Windows Form](http://go.microsoft.com/fwlink/?LinkId=203523)  
  
### Ignorare e continua  
 È possibile scegliere di ignorare la condizione di errore e continuare il caricamento della finestra di progettazione.  La scelta di questa azione può generare un comportamento imprevisto.  Ad esempio, è possibile che nell'area di progettazione non vengano visualizzati i controlli.  
  
## Vedere anche  
 [Troubleshooting Design\-Time Development](../Topic/Troubleshooting%20Design-Time%20Development.md)   
 [Risoluzione dei problemi relativi alla modifica di controlli e componenti](../../../../docs/framework/winforms/controls/troubleshooting-control-and-component-authoring.md)   
 [Sviluppo di controlli Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [Windows Forms Designer Error Messages](http://msdn.microsoft.com/it-it/cf610bf4-5fe4-471c-bce7-6a05ece07bd2)