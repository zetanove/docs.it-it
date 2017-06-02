---
title: "Pianificazione delle prestazioni dell&#39;applicazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "applicazioni, ottimizzazione"
  - "applicazione WPF, ottimizzazione"
ms.assetid: c91bd0c5-a193-46ff-9da1-eb7a3a76a3b3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Pianificazione delle prestazioni dell&#39;applicazione
La possibilità di raggiungere gli obiettivi prefissati in termini di prestazioni dipende dalla capacità di sviluppare una valida strategia delle prestazioni.  La pianificazione costituisce la prima fase dello sviluppo di qualsiasi prodotto.  In questo argomento vengono descritte poche, semplici regole per lo sviluppo di una strategia delle prestazioni efficace.  
  
## Pensare in termini di scenari  
 Gli scenari consentono di concentrare più facilmente l'attenzione sui componenti critici dell'applicazione.  In genere sono ricavati dai clienti oppure dai prodotti della concorrenza.  È opportuno osservare sempre i propri clienti, per scoprire cosa li attrae di più in un prodotto Microsoft e in quelli della concorrenza.  I commenti e i suggerimenti dei clienti possono risultare molto utili nella definizione dello scenario principale dell'applicazione.  Ad esempio, se si sta progettando un componente che verrà utilizzato all'avvio, è probabile che tale componente verrà chiamato una sola volta, vale a dire all'avvio dell'applicazione.  In questo caso il tempo di avvio costituirà lo scenario principale.  Altri esempi di scenari principali potrebbero essere la frequenza dei fotogrammi desiderata per le sequenze di animazione oppure il working set massimo consentito per l'applicazione.  
  
## Definire gli obiettivi  
 Gli obiettivi consentono di determinare la velocità di esecuzione di un'applicazione.  È opportuno definire obiettivi per tutti gli scenari.  Tutti gli obiettivi definiti in relazione alle prestazioni dovrebbero essere basati sulle aspettative dei clienti.  Può essere difficile stabilire degli obiettivi relativi alle prestazioni all'inizio del ciclo di sviluppo dell'applicazione, quando molti problemi devono ancora essere risolti.  Tuttavia è preferibile definire un obiettivo iniziale e modificarlo successivamente, piuttosto che non definirne nessuno.  
  
## Conoscere esattamente la piattaforma utilizzata  
 Garantire sempre il ciclo di misurazione, analisi, perfezionamento e correzione durante il ciclo di sviluppo dell'applicazione.  Dall'inizio alla fine del ciclo di sviluppo, è necessario misurare le prestazioni dell'applicazione in un ambiente stabile e affidabile,  evitando situazioni variabili provocate da fattori esterni.  Durante il test delle prestazioni, ad esempio, è opportuno disabilitare l'antivirus o qualsiasi altro aggiornamento automatico quale SMS, in modo da non influenzare i risultati del test.  Dopo aver misurato le prestazioni dell'applicazione, sarà necessario individuare le modifiche in grado di garantire i miglioramenti più significativi.  Una volta modificata l'applicazione, avviare nuovamente il ciclo.  
  
## Rendere l'ottimizzazione delle prestazioni un processo iterativo  
 È importante conoscere il costo relativo di ciascuna delle funzionalità che verranno utilizzate.  Ad esempio, poiché la reflection in [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)] richiede in genere prestazioni elevate in termini di risorse di elaborazione, è consigliabile impiegarla con attenzione.  Ciò non significa evitare l'uso della reflection, ma solo fare attenzione a bilanciare i requisiti di prestazioni dell'applicazione e le richieste di prestazioni della funzionalità utilizzate.  
  
## Eseguire la compilazione in direzione di una maggiore ricchezza grafica  
 Una tecnica chiave per la creazione di un approccio scalabile rivolto a ottenere le massime prestazioni dall'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste in una compilazione indirizzata a una maggiore ricchezza e complessità grafica.  Iniziare sempre utilizzando le risorse che richiedono prestazioni minime per raggiungere gli obiettivi stabiliti per lo scenario.  Una volta raggiunti questi obiettivi, puntare a una maggiore ricchezza grafica utilizzando funzionalità più impegnative in termini di prestazioni, tenendo sempre ben presenti gli obiettivi dello scenario.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è una piattaforma molto articolata e offre funzionalità grafiche altrettanto complesse.  L'utilizzo sconsiderato di funzionalità impegnative in termini di prestazioni può influire negativamente sulle prestazioni dell'applicazione in generale.  
  
 È possibile estendere i controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consentendo la personalizzazione diffusa dell'aspetto, senza tuttavia alterarne il comportamento.  L'utilizzo degli stili, dei modelli di dati e dei modelli dei controlli consente di creare e sviluppare gradualmente un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] personalizzabile in grado di adattarsi ai requisiti di prestazioni.  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)