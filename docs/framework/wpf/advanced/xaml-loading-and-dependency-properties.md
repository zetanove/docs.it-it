---
title: "Caricamento XAML e propriet&#224; di dipendenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "proprietà Dependency personalizzate"
  - "proprietà di dipendenza, caricamento XAML"
  - "caricamento di dati XML"
ms.assetid: 6eea9f4e-45ce-413b-a266-f08238737bf2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Caricamento XAML e propriet&#224; di dipendenza
L'implementazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corrente del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] dipende implicitamente dalle proprietà di dipendenza.  Il processore [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizza metodi del sistema di proprietà per le proprietà di dipendenza al momento del caricamento del codice [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] binario e dell'elaborazione di attributi che sono proprietà di dipendenza.  Ciò consente di ignorare in modo efficace i wrapper della proprietà.  Quando si implementano proprietà di dipendenza personalizzate, è necessario tenere presente questo comportamento ed evitare di inserire nel wrapper della proprietà qualsiasi altro codice oltre ai metodi del sistema di proprietà <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone la conoscenza delle proprietà di dipendenza sia in qualità di consumer, sia in qualità di autore oltre alla lettura di [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md) e [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  È necessario inoltre aver letto [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md) e [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
<a name="implementation"></a>   
## Implementazione del caricatore XAML WPF e prestazioni  
 Per motivi di implementazione, dal punto di vista del calcolo risulta meno oneroso identificare una proprietà come proprietà di dipendenza e accedere al metodo <xref:System.Windows.DependencyObject.SetValue%2A> del sistema di proprietà per impostarla, che utilizzare il wrapper della proprietà e il relativo metodo di impostazione.  Ciò si verifica in quanto un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] deve dedurre l'intero modello a oggetti del codice di supporto esclusivamente in base alla conoscenza delle relazioni tra tipi e membri indicate dalla struttura del markup e da varie stringhe.  
  
 Il tipo viene ricercato tramite una combinazione di attributi xmlns e di assembly, ma l'identificazione dei membri, la determinazione dei membri che è possibile impostare come attributi e la risoluzione dei tipi supportati dai valori di proprietà richiedono la reflection estesa mediante l'oggetto <xref:System.Reflection.PropertyInfo>.  Dal momento che è possibile accedere alle proprietà di dipendenza di un determinato tipo come tabella di archiviazione tramite il sistema di proprietà, l'implementazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] del relativo processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizza questa tabella e deduce che una data proprietà *ABC* può essere impostata in modo più efficace chiamando l'oggetto <xref:System.Windows.DependencyObject.SetValue%2A> sul tipo derivato <xref:System.Windows.DependencyObject> contenitore, mediante l'identificatore della proprietà di dipendenza *ProprietàABC*.  
  
<a name="implications"></a>   
## Implicazioni per le proprietà di dipendenza personalizzate  
 Poiché l'implementazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corrente del comportamento del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per l'impostazione delle proprietà ignora completamente i wrapper, non è opportuno inserire logica aggiuntiva nelle definizioni stabilite del wrapper per la proprietà di dipendenza personalizzata.  Se si inserisce tale logica nella definizione stabilita, questa non sarà eseguita quando la proprietà viene impostata in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] piuttosto che nel codice.  
  
 Analogamente, anche altri aspetti del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che ottengono valori di proprietà dall'elaborazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzano l'oggetto <xref:System.Windows.DependencyObject.GetValue%2A> piuttosto che il wrapper.  Pertanto, è necessario evitare qualsiasi implementazione aggiuntiva nella definizione `get` oltre alla chiamata di <xref:System.Windows.DependencyObject.GetValue%2A>.  
  
 L'esempio seguente è una definizione di una proprietà di dipendenza consigliata con wrapper, in cui l'identificatore di proprietà è archiviato come campo `static` `public` `readonly` e le definizioni `get` e `set` non contengono codice oltre ai metodi del sistema di proprietà necessari che definiscono il supporto della proprietà di dipendenza.  
  
 [!code-csharp[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
 [!code-vb[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]  
  
## Vedere anche  
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [Proprietà di dipendenza di tipo raccolta](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md)   
 [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md)   
 [Modelli di costruttore sicuri per DependencyObject](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md)