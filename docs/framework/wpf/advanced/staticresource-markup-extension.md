---
title: "Estensione del markup StaticResource | Microsoft Docs"
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
  - "StaticResource"
  - "StaticResourceExtension"
helpviewer_keywords: 
  - "StaticResource (estensioni di markup)"
  - "XAML, StaticResource (estensione di markup)"
ms.assetid: 97af044c-71f1-4617-9a94-9064b68185d2
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Estensione del markup StaticResource
Fornisce un valore per qualsiasi attributo di proprietà [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] eseguendo la ricerca di un riferimento a una risorsa già definita.  Il comportamento della ricerca per quella risorsa è analogo alla ricerca in fase di caricamento, che cercherà le risorse caricate in precedenza dal markup della pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] corrente oltre che le altre origini dell'applicazione e genererà il valore di risorsa come valore della proprietà negli oggetti runtime.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{StaticResource key}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<object>  
  <object.property>  
<StaticResource ResourceKey="key" .../>  
  </object.property>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`key`|Chiave della risorsa richiesta.  Questa chiave è stata inizialmente assegnata da [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md) se una risorsa è stata creata nel markup oppure è stata fornita come parametro `key` al momento della chiamata all'oggetto <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> se la risorsa è stata creata nel codice.|  
  
## Note  
  
> [!IMPORTANT]
>  Un oggetto `StaticResource` non deve tentare di eseguire un riferimento diretto a una risorsa con una definizione lessicale ulteriore all'interno del file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Un tentativo di questo tipo non è supportato e persino se tale riferimento ha esito positivo, si verificherà una riduzione delle prestazioni in fase di caricamento durante la ricerca nelle tabelle hash interne che rappresentano un oggetto <xref:System.Windows.ResourceDictionary>.  Per risultati ottimali, regolare la composizione dei dizionari di risorse in modo da evitare tali riferimenti diretti.  Se non è possibile evitare un riferimento diretto, utilizzare invece [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md).  
  
 L'oggetto <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> specificato deve corrispondere a una risorsa esistente, identificata con un oggetto [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md) a un certo livello nella pagina, nell'applicazione, nei temi dei controlli e nelle risorse esterne disponibili oppure nelle risorse di sistema.  La ricerca delle risorse viene eseguita in quell'ordine.  Per ulteriori informazioni sul comportamento della ricerca delle risorse statiche e dinamiche, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 Una chiave di risorsa può essere una qualsiasi stringa definita in [Grammatica XamlName](../../../../docs/framework/xaml-services/xamlname-grammar.md).  Una chiave di risorsa può anche essere costituita da altri tipi di oggetto, ad esempio <xref:System.Type>.  Una chiave <xref:System.Type> è fondamentale per il modo in cui i temi possono applicare stili ai controlli mediante una chiave di stile implicita.  Per ulteriori informazioni, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 Un modo alternativo per fare riferimento a una risorsa è come [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md).  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Il token di stringa fornito dopo la stringa dell'identificatore `StaticResource` viene assegnato come valore <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> della classe dell'estensione <xref:System.Windows.StaticResourceExtension> sottostante.  
  
 L'oggetto `StaticResource` può essere utilizzato nella sintassi per gli elementi oggetto.  In questo caso, è necessario specificare il valore della proprietà <xref:System.Windows.StaticResourceExtension.ResourceKey%2A>.  
  
 L'oggetto `StaticResource` può anche essere adoperato per un uso dettagliato degli attributi che consente di specificare la proprietà <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> come coppia proprietà\=valore:  
  
```  
<object property="{StaticResource ResourceKey=key}" .../>  
```  
  
 L'utilizzo dettagliato spesso è utile per le estensioni con più proprietà da impostare o nel caso in cui alcune proprietà siano facoltative.  Poiché `StaticResource` presenta una sola proprietà da impostare, obbligatoria, l'utilizzo dettagliato non è tipico.  
  
 Nell'implementazione del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.StaticResourceExtension>.  
  
 `StaticResource` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Tutte le estensioni di markup di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzano i caratteri { e } nella relativa sintassi degli attributi. Grazie a questa convenzione il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è in grado di rilevare la necessità che l'attributo venga elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Risorse e codice](../../../../docs/framework/wpf/advanced/resources-and-code.md)