---
title: "Code-behind e XAML in WPF | Microsoft Docs"
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
  - "file code-behind, XAML"
  - "XAML, code-behind"
ms.assetid: 9df6d3c9-aed3-471c-af36-6859b19d999f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Code-behind e XAML in WPF
<a name="introduction"></a> Code\-behind è un termine utilizzato per descrivere il codice che viene unito agli oggetti definiti dal markup quando viene compilata una pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  In questo argomento vengono descritti i requisiti per il code\-behind, nonché un meccanismo di codice inline alternativo per il codice in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Prerequisiti](#Prerequisites)  
  
-   [Code\-behind e linguaggio XAML](#codebehind_and_the_xaml_language)  
  
-   [Code\-behind, gestore eventi e requisiti della classe parziale in WPF](#Code_behind__Event_Handler__and_Partial_Class)  
  
-   [x:Code](#x_Code)  
  
-   [Limitazioni del codice inline](#Inline_Code_Limitations)  
  
<a name="Prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone che l'utente abbia letto [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md) e che disponga di una conoscenza di base di [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e della programmazione orientata a oggetti.  
  
<a name="codebehind_and_the_xaml_language"></a>   
## Code\-behind e linguaggio XAML  
 In XAML sono incluse funzionalità a livello di linguaggio che rendono possibile l'associazione di file di codice a file di markup dal lato del file di markup.  In particolare, il linguaggio XAML definisce le funzionalità del linguaggio [Direttiva x:Class](../../../../docs/framework/xaml-services/x-class-directive.md), [Direttiva x:Subclass](../../../../docs/framework/xaml-services/x-subclass-directive.md) e [Direttiva x:ClassModifier](../../../../docs/framework/xaml-services/x-classmodifier-directive.md).  Il linguaggio XAML non specifica le modalità esatte da utilizzare per la produzione di codice e l'integrazione di markup e codice.  La scelta della modalità di integrazione del codice, di utilizzo di XAML nei modelli di applicazione e programmazione, nonché delle azioni di compilazione o dell'ulteriore supporto richiesto viene lasciata ai framework, ad esempio WPF.  
  
<a name="Code_behind__Event_Handler__and_Partial_Class"></a>   
## Code\-behind, gestore eventi e requisiti della classe parziale in WPF  
  
-   La classe parziale deve derivare dal tipo di classe che supporta l'elemento radice.  
  
-   Si noti che con il comportamento predefinito delle azioni di compilazione del markup, è possibile lasciare vuota la derivazione nella definizione della classe parziale sul lato code\-behind.  Nel risultato compilato si presupporrà che il tipo di supporto della radice della pagina costituisca la base per la classe parziale, anche se non viene specificato.  Basarsi su questo comportamento non è tuttavia una procedura consigliata.  
  
-   I gestori eventi scritti nel code\-behind devono essere metodi di istanza e non possono essere metodi statici.  Questi metodi devono essere definiti dalla classe parziale all'interno dello spazio dei nomi CLR identificato da `x:Class`.  Non è possibile qualificare il nome di un gestore eventi per indicare a un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] di cercare un gestore eventi per il collegamento di eventi in un ambito della classe diverso.  
  
-   Il gestore deve corrispondere al delegato per l'evento appropriato nel sistema di tipi di supporto.  
  
-   Nel caso specifico del linguaggio [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)], è possibile utilizzare la parola chiave `Handles` specifica del linguaggio per associare i gestori eventi alle istanze e agli eventi della dichiarazione del gestore, anziché associare i gestori eventi agli attributi in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Questa tecnica presenta tuttavia alcuni limiti, poiché la parola chiave `Handles` non è in grado di supportare tutte le funzioni specifiche del sistema di eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], ad esempio alcuni scenari di eventi indirizzati o eventi associati.  Per informazioni dettagliate, vedere [Visual Basic e la gestione degli eventi WPF](../../../../docs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md).  
  
<a name="x_Code"></a>   
## x:Code  
 [x:Code](../../../../docs/framework/xaml-services/x-code-intrinsic-xaml-type.md) è un elemento della direttiva definito in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. Un elemento della direttiva `x:Code` può contenere il codice di programmazione inline.  Il codice definito inline può interagire con la sintassi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] nella stessa pagina.  Nell'esempio seguente viene mostrato il codice [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] inline.  Notare che il codice si trova all'interno dell'elemento `x:Code` e che deve essere racchiuso da `<CDATA[`...`]]>` per utilizzare caratteri di escape del contenuto per [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)], in modo che un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] \(che interpreta lo schema [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o lo schema [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]\) non tenti di interpretare il contenuto in modo letterale come [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)].  
  
 [!code-xml[XAMLOvwSupport#ButtonWithInlineCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page4.xaml#buttonwithinlinecode)]  
  
<a name="Inline_Code_Limitations"></a>   
## Limitazioni del codice inline  
 È necessario evitare o limitare l'utilizzo di codice inline.  In termini di architettura e codifica, una separazione tra markup e code\-behind consente di mantenere più distinti i ruoli del progettista e dello sviluppatore.  A un livello più tecnico, la scrittura del codice inline può risultare difficile, poiché si scrive nella classe parziale generata di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ed è possibile utilizzare solo i mapping dello spazio dei nomi XML predefiniti.  Dal momento che non è possibile aggiungere istruzioni `using`, è necessario qualificare in modo completo molte delle chiamate [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] effettuate.  I mapping [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] predefiniti includono la maggior parte, ma non tutti, degli spazi dei nomi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] presenti negli assembly [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Di conseguenza sarà necessario qualificare in modo completo le chiamate a tipi e membri inclusi all'interno degli altri spazi dei nomi CLR.  Nel codice inline non è inoltre possibile definire nient'altro che la classe parziale e tutte le entità di codice dell'utente a cui viene fatto riferimento devono essere disponibili come membro o variabile all'interno della classe parziale generata.  Non sono neanche disponibili altre funzionalità di programmazione specifiche del linguaggio, ad esempio macro o `#ifdef` nelle variabili globali o di compilazione.  Per ulteriori informazioni, vedere [Tipo XAML intrinseco x:Code](../../../../docs/framework/xaml-services/x-code-intrinsic-xaml-type.md).  
  
## Vedere anche  
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Tipo XAML intrinseco x:Code](../../../../docs/framework/xaml-services/x-code-intrinsic-xaml-type.md)   
 [Compilazione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)