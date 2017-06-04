---
title: "Estensione del markup DynamicResource | Microsoft Docs"
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
  - "DynamicResource"
  - "DynamicResourceExtension"
helpviewer_keywords: 
  - "DynamicResource (estensioni di markup)"
  - "XAML, DynamicResource (estensione di markup)"
ms.assetid: 7324f243-03af-4c2b-b0db-26ac6cdfcbe4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Estensione del markup DynamicResource
Fornisce un valore per tutti gli attributi della proprietà [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] rinviando tale valore come riferimento per una risorsa definita.  Il comportamento di ricerca per tale risorsa è analogo alla ricerca in fase di esecuzione.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{DynamicResource key}" .../>  
```  
  
## Utilizzo degli elementi della proprietà XAML  
  
```  
<object>  
  <object.property>  
    <DynamicResource ResourceKey="key" .../>  
  </object.property>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`key`|Chiave della risorsa richiesta.  Questa chiave è stata inizialmente assegnata da [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md) se una risorsa è stata creata nel markup oppure è stata fornita come parametro `key` al momento della chiamata all'oggetto <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> se la risorsa è stata creata nel codice.|  
  
## Note  
 Un oggetto `DynamicResource` crea un'espressione temporanea durante la compilazione iniziale, pertanto la ricerca delle risorse viene rinviata finché il valore della risorsa richiesta non risulta effettivamente necessario per costruire un oggetto.  Questa situazione potrebbe verificarsi dopo il caricamento della pagina [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Il valore della risorsa sarà individuato in base alla ricerca della chiave in tutti i dizionari risorse attivi, iniziando dall'ambito della pagina corrente e sarà sostituito con l'espressione del segnaposto della compilazione.  
  
> [!IMPORTANT]
>  In termini di precedenza della proprietà di dipendenza, un'espressione `DynamicResource` è equivalente alla posizione in cui viene applicato il riferimento di risorsa dinamica.  Se viene impostato un valore locale per una proprietà che in precedenza disponeva di un'espressione `DynamicResource` come valore locale, l'oggetto `DynamicResource` viene completamente rimosso.  Per informazioni dettagliate, vedere [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md).  
  
 Alcuni scenari di accesso alla risorsa sono particolarmente appropriati per `DynamicResource` in contrapposizione a [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md).  Per una descrizione sui relativi pregi e sulle implicazioni in termini di prestazioni di `DynamicResource` e `StaticResource`, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 L'oggetto <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> specificato deve corrispondere a una risorsa esistente determinata da un attributo [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md) a un certo livello della pagina, dell'applicazione; dei temi dei controlli e delle risorse esterne disponibili oppure delle risorse di sistema, e la ricerca delle risorse verrà eseguita in quell'ordine.  Per ulteriori informazioni sulla ricerca delle risorse statiche e dinamiche, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 Una chiave di risorsa può essere una qualsiasi stringa definita in [Grammatica XamlName](../../../../docs/framework/xaml-services/xamlname-grammar.md).  Una chiave di risorsa può anche essere costituita da altri tipi di oggetto, ad esempio <xref:System.Type>.  Una chiave <xref:System.Type> è fondamentale per il modo in cui i temi possono applicare stili ai controlli.  Per ulteriori informazioni, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 Le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] per la ricerca dei valori delle risorse, ad esempio <xref:System.Windows.FrameworkElement.FindResource%2A>, seguono la stessa logica di ricerca delle risorse utilizzata da `DynamicResource`.  
  
 Un metodo alternativo per fare riferimento a una risorsa è come [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md).  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Il token di stringa fornito dopo la stringa dell'identificatore `DynamicResource` viene assegnato come valore <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> della classe dell'estensione <xref:System.Windows.DynamicResourceExtension> sottostante.  
  
 L'oggetto `DynamicResource` può essere utilizzato nella sintassi per gli elementi oggetto.  In questo caso, è necessario specificare il valore della proprietà <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A>.  
  
 L'oggetto `DynamicResource` può anche essere adoperato per un uso dettagliato degli attributi che consente di specificare la proprietà <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> come coppia proprietà\=valore:  
  
```  
<object property="{DynamicResource ResourceKey=key}" .../>  
```  
  
 L'utilizzo dettagliato spesso è utile per le estensioni con più proprietà da impostare o nel caso in cui alcune proprietà siano facoltative.  Poiché `DynamicResource` presenta una sola proprietà da impostare, obbligatoria, l'utilizzo dettagliato non è tipico.  
  
 Nell'implementazione del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.DynamicResourceExtension>.  
  
 `DynamicResource` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Tutte le estensioni di markup di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzano i caratteri { e } nella relativa sintassi degli attributi. Grazie a questa convenzione il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è in grado di rilevare la necessità che l'attributo venga elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Risorse e codice](../../../../docs/framework/wpf/advanced/resources-and-code.md)   
 [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)