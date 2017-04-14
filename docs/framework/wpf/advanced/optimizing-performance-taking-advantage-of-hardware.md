---
title: "Ottimizzazione delle prestazioni: sfruttare appieno l&#39;hardware | Microsoft Docs"
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
  - "grafica (livelli di rendering)"
  - "grafica, prestazioni"
  - "grafica, livelli di rendering"
  - "rendering hardware (pipeline)"
  - "livelli di rendering"
  - "rendering software (pipeline)"
ms.assetid: bfb89bae-7aab-4cac-a26c-a956eda8fce2
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Ottimizzazione delle prestazioni: sfruttare appieno l&#39;hardware
L'architettura interna di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] presenta due pipeline di rendering, hardware e software.  In questo argomento vengono fornite informazioni su tali pipeline di rendering, in modo da consentire di decidere le operazioni più opportune per ottimizzare le prestazioni delle applicazioni.  
  
## Pipeline di rendering hardware  
 Uno dei fattori più importanti per determinare le prestazioni di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste nel fatto che queste sono associate al rendering: maggiore è il numero di pixel di cui eseguire il rendering, maggiore sarà l'incidenza sulle prestazioni.  Tuttavia, maggiore è il volume di rendering che è possibile scaricare alla [!INCLUDE[TLA#tla_gpu](../../../../includes/tlasharptla-gpu-md.md)], maggiori saranno i vantaggi in termini di prestazioni.  La pipeline di rendering hardware dell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sfrutta le funzionalità [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] sull'hardware che supporta almeno [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] versione 7.0.  Ulteriori ottimizzazioni possono essere sfruttate dall'hardware che supporta le funzionalità di [!INCLUDE[TLA#tla_dx](../../../../includes/tlasharptla-dx-md.md)] versione 7.0 e PixelShader 2.0 o superiore.  
  
## Pipeline di rendering software  
 La pipeline di rendering software [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è totalmente associata alla CPU.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sfrutta i set di istruzioni SSE e SSE2 della CPU per implementare un'unità di rasterizzazione software ottimizzata e completa.  Il fallback al software risulta semplificato nei casi in cui non è possibile eseguire il rendering di una funzionalità dell'applicazione tramite la pipeline di rendering hardware.  
  
 Il problema più rilevante relativamente alle prestazioni si verifica quando il rendering in modalità software è correlato alla velocità di riempimento, definita come numero di pixel di cui si sta eseguendo il rendering.  Se si desidera evitare problemi di prestazioni durante il rendering in modalità software, provare a ridurre al minimo il numero di volte in cui un pixel viene ridisegnato.  Se, ad esempio, si sta utilizzando un'applicazione con sfondo blu, che esegue il rendering di un'immagine leggermente trasparente sullo sfondo stesso, sarà necessario eseguire due volte il rendering di tutti i pixel dell'applicazione.  Di conseguenza, l'operazione di rendering dell'applicazione con l'immagine impiegherà il doppio del tempo rispetto a quello necessario nel caso in cui l'applicazione presenti solo lo sfondo blu.  
  
### Livelli di rendering della grafica  
 Prevedere la configurazione hardware in cui sarà eseguita l'applicazione può essere molto difficile.  Tuttavia, è possibile prendere in considerazione una progettazione che consenta di passare facilmente da una funzionalità dell'applicazione all'altra durante l'esecuzione su hardware diverso, in modo da sfruttare appieno tutte le differenti configurazioni hardware.  
  
 A tal fine, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce le funzionalità necessarie per determinare le funzionalità grafiche di un sistema in fase di esecuzione.  Le funzionalità grafiche sono determinate dalla categorizzazione della scheda video come uno dei tre livelli di funzionalità di rendering.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] espone un'[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] che consente a un'applicazione di ricercare il livello di funzionalità di rendering.  L'applicazione può quindi accettare diversi percorsi del codice in fase di esecuzione, a seconda del livello di rendering supportato dall'hardware.  
  
 Di seguito sono riportate le funzionalità dell'hardware grafico che influiscono maggiormente sui livelli di rendering:  
  
-   **RAM video**: la quantità di memoria video disponibile nell'hardware grafico determina le dimensioni e il numero di buffer che possono essere utilizzati per la composizione della grafica.  
  
-   **Pixel shader**: un pixel shader è una funzione di elaborazione grafica che calcola gli effetti per singolo pixel.  A seconda della risoluzione della grafica visualizzata, può essere necessario elaborare milioni di pixel per ogni fotogramma di visualizzazione.  
  
-   **Vertex shader**: un vertex shader è una funzione di elaborazione grafica che esegue operazioni matematiche sui dati vertex dell'oggetto.  
  
-   **Supporto multitrama**: il supporto multitrama fa riferimento alla possibilità di applicare due o più trame distinte durante un'operazione di sfumatura su un oggetto di grafica tridimensionale.  Il grado del supporto multitrama è determinato dal numero di unità multitrama dell'hardware grafico.  
  
 Le funzionalità pixel shader, vertex shader e multitrama vengono utilizzate per definire specifici livelli di versione di [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)], che a loro volta consentono di determinare i diversi livelli di rendering in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Le funzionalità dell'hardware grafico determinano la capacità di rendering di un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Nel sistema [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono definiti tre livelli di rendering:  
  
-   **Livello di rendering 0**: nessuna accelerazione dell'hardware grafico.  Il livello di versione di [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] è inferiore alla versione 7.0.  
  
-   **Livello di rendering 1**: accelerazione dell'hardware grafico parziale.  Il livello di versione di [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] è superiore o uguale rispetto alla versione 7.0 e **inferiore** alla versione 9.0.  
  
-   **Livello di rendering 2**: la maggior parte delle funzionalità grafiche utilizzano l'accelerazione dell'hardware grafico.  Il livello di versione di [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] è superiore o uguale rispetto alla versione 9.0.  
  
 Per ulteriori informazioni sui livelli di rendering di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Livelli di rendering della grafica](../../../../docs/framework/wpf/advanced/graphics-rendering-tiers.md).  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)