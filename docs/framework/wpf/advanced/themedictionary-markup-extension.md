---
title: "Estensione del markup ThemeDictionary | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ThemeDictionaryExtension"
  - "ThemeDictionary"
helpviewer_keywords: 
  - "ThemeDictionary (estensione di markup)"
  - "XAML, ThemeDictionary (estensione di markup)"
ms.assetid: aa75e10b-13dd-4989-972d-51bab63a05e2
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Estensione del markup ThemeDictionary
Fornisce agli autori di controlli personalizzati o alle applicazioni che integrano controlli di terze parti un modo per caricare dizionari di risorse specifici del tema da utilizzare nell'applicazione degli stili al controllo.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{ThemeDictionary assemblyUri}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<object>  
  <object.property>  
    <ThemeDictionary AssemblyName="assemblyUri"/>  
  <object.property>  
<object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`assemblyUri`|[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] dell'assembly contenente le informazioni sul tema.  In genere, si tratta di un URI di tipo pack che fa riferimento a un assembly del package più grande.  Le risorse di assembly e gli URI di tipo pack semplificano i problemi di distribuzione.  Per ulteriori informazioni, vedere [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md).|  
  
## Note  
 Questa estensione deve compilare solo un valore specifico della proprietà, vale a dire un valore per la proprietà <xref:System.Windows.ResourceDictionary.Source%2A?displayProperty=fullName>.  
  
 Utilizzando questa estensione, è possibile specificare un singolo assembly di sole risorse contenente alcuni stili da utilizzare solo quando il tema [!INCLUDE[TLA#tla_aero](../../../../includes/tlasharptla-aero-md.md)] viene applicato al sistema dell'utente; gli altri stili possono essere utilizzati quando il tema Luna è attivo e così via.  Utilizzando questa estensione, il contenuto di un dizionario risorse specifico del controllo può essere invalidato automaticamente e ricaricato in modo che venga considerato specifico per un altro tema quando necessario.  
  
 La stringa `assemblyUri` \(valore della proprietà<xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A>\) costituisce la base di una convenzione di denominazione che identifica il dizionario applicato a un tema particolare.  La logica <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> di `ThemeDictionary` completa la convenzione generando uno [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] che punta a una variante particolare del dizionario dei temi, contenuta all'interno di un assembly di risorse precompilato.  La descrizione di questa convenzione o delle interazioni dei temi con l'applicazione degli stili al controllo generale e a livello di pagina o di applicazione come concetto, non è illustrata completamente in questa sezione.  Lo scenario di base per l'utilizzo di `ThemeDictionary` consiste nello specificare la proprietà <xref:System.Windows.ResourceDictionary.Source%2A> di un oggetto `ResourceDictionary` dichiarato a livello di applicazione.  Quando viene fornito uno [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] per l'assembly tramite un'estensione `ThemeDictionary` anziché uno [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] diretto, grazie alla logica dell'estensione verrà fornita la logica di invalidazione applicata in occasione di tutte le modifiche del tema del sistema.  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Il token di stringa fornito dopo la stringa dell'identificatore `ThemeDictionary` viene assegnato come valore <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> della classe dell'estensione <xref:System.Windows.ThemeDictionaryExtension> sottostante.  
  
 L'oggetto `ThemeDictionary` può essere utilizzato anche nella sintassi per gli elementi oggetto.  In questo caso, è necessario specificare il valore della proprietà <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A>.  
  
 L'oggetto `ThemeDictionary` può anche essere adoperato per un uso dettagliato degli attributi che consente di specificare la proprietà <xref:System.Windows.Markup.StaticExtension.Member%2A> come coppia proprietà\=valore:  
  
```  
<object property="{ThemeDictionary AssemblyName=assemblyUri}" .../>  
```  
  
 L'utilizzo dettagliato spesso è utile per le estensioni con più proprietà da impostare o nel caso in cui alcune proprietà siano facoltative.  Poiché `ThemeDictionary` presenta una sola proprietà da impostare, obbligatoria, l'utilizzo dettagliato non è tipico.  
  
 Nell'implementazione del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.ThemeDictionaryExtension>.  
  
 `ThemeDictionary` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Tutte le estensioni di markup di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzano i caratteri { e } nella relativa sintassi degli attributi. Grazie a questa convenzione il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è in grado di rilevare la necessità che l'attributo venga elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [File di dati e di risorse dell'applicazione WPF.](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)