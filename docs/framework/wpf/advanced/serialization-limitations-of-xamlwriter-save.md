---
title: "Limitazioni relative alla serializzazione di XamlWriter.Save | Microsoft Docs"
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
  - "limitazioni di XamlWriter.Save"
  - "limitazioni relative alla serializzazione di XamlWriter.Save"
  - "XamlWriter.Save, limitazioni relative alla serializzazione"
ms.assetid: f86acc91-2b67-4039-8555-505734491d36
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Limitazioni relative alla serializzazione di XamlWriter.Save
È possibile utilizzare [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] <xref:System.Windows.Markup.XamlWriter.Save%2A> per serializzare il contenuto di un'applicazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] come file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Esistono tuttavia delle limitazioni considerevoli relative alla definizione precisa dell'oggetto della serializzazione.  Tali limitazioni e alcune considerazioni generali vengono esaminate in questo argomento.  
  
   
  
<a name="Run_Time__Not_Design_Time_Representation"></a>   
## Rappresentazione della fase di esecuzione e delle fasi esterne alla progettazione  
 La scelta degli elementi da serializzare tramite una chiamata a <xref:System.Windows.Markup.XamlWriter.Save%2A> deve basarsi sul fatto che il risultato sarà una rappresentazione dell'oggetto della serializzazione in fase di esecuzione.  È possibile che molte proprietà della fase di progettazione del file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] originale siano già state ottimizzate oppure perse al momento del caricamento di dati [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] come oggetti in memoria e non vengano mantenute nella chiamata a <xref:System.Windows.Markup.XamlWriter.Save%2A> per la serializzazione.  Il risultato della serializzazione consiste in una rappresentazione effettiva dell'albero logico dell'applicazione costruito, ma non necessariamente del file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che lo ha prodotto.  Tale condizione rende estremamente difficile l'utilizzo della serializzazione <xref:System.Windows.Markup.XamlWriter.Save%2A> come parte di un'area di progettazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] estensiva.  
  
<a name="Serialization_is_Self_Contained"></a>   
## La serializzazione è indipendente da riferimenti esterni  
 L'output di serializzazione di <xref:System.Windows.Markup.XamlWriter.Save%2A> è indipendente; tutti gli elementi serializzati sono contenuti in una singola pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], con un unico elemento radice e nessun riferimento esterno ad eccezione degli [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)].  Ad esempio, se in una pagina vengono fatti riferimenti alle risorse dalle risorse dell'applicazione, questi saranno visualizzati come componenti della pagina serializzata.  
  
<a name="Extension_References_are_Dereferenced"></a>   
## I riferimenti alle estensioni vengono dereferenziati  
 I riferimenti comuni agli oggetti costituiti da diversi formati di estensione di markup, ad esempio `StaticResource` o `Binding`, saranno dereferenziati durante il processo di serializzazione.  La dereferenziazione avviene già al momento della creazione degli oggetti in memoria durante la fase di esecuzione dell'applicazione e la logica di <xref:System.Windows.Markup.XamlWriter.Save%2A> non prevede la revisione dei dati [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] originali per il ripristino di tali riferimenti nell'output della serializzazione.  In questo modo, potenzialmente qualsiasi valore associato ai dati o proveniente dalla risorsa viene bloccato come ultimo valore utilizzato dalla rappresentazione in fase di esecuzione, con possibilità solo limitate o indirette di distinguerlo da qualsiasi altro valore impostato localmente.  Anche le immagini vengono serializzate come riferimenti a oggetti in base alle immagini esistenti nel progetto, piuttosto che come riferimenti all'origine effettiva, con conseguente perdita di qualsiasi nome file o [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] a cui si faceva originariamente riferimento.  Perfino le risorse dichiarate all'interno della stessa pagina sono serializzate nel punto in cui vengono fatti i relativi riferimenti, anziché essere conservate come chiave della raccolta delle risorse.  
  
<a name="Event_Handling_is_Not_Preserved"></a>   
## La gestione degli eventi non viene mantenuta  
 Quando i gestori di evento aggiunti tramite [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] sono serializzati, non vengono mantenuti.  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] senza code\-behind \(e senza il relativo meccanismo x:Code\) non consente di serializzare la logica procedurale runtime.  Dal momento che la serializzazione è indipendente e limitata all'albero logico, non sono disponibili funzionalità per l'archiviazione dei gestori eventi.  Di conseguenza, gli attributi dei gestori eventi, sia l'attributo stesso che il valore della stringa indicante il nome del gestore, vengono rimossi dall'output [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
<a name="Realistic_Scenarios_for_Use_of_XAMLWriter_Save"></a>   
## Scenari realistici per l'utilizzo di XAMLWriter.Save  
 Sebbene le limitazioni qui elencate siano piuttosto rilevanti, esistono diversi scenari appropriati per l'utilizzo di <xref:System.Windows.Markup.XamlWriter.Save%2A> per la serializzazione.  
  
-   Output vettoriale o grafico: l'output dell'area sottoposta a rendering può essere utilizzato per riprodurre lo stesso vettore o la stessa grafica se caricato nuovamente.  
  
-   Documenti RTF o dinamici: il testo con tutta la formattazione e il contenimento degli elementi inclusi viene mantenuto nell'output.  Tale opzione può risultare utile per i meccanismi che si avvicinano a una funzionalità degli Appunti.  
  
-   Conservazione dei dati di oggetti business: se in elementi personalizzati sono stati archiviati dei dati, quali i dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)], finché gli oggetti business seguono le regole [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] di base, ad esempio fornire costruttori personalizzati e la conversione per valori di proprietà per riferimento, sarà possibile conservare tali oggetti business mediante la serializzazione.