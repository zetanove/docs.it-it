---
title: "Estensione del markup TemplateBinding | Microsoft Docs"
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
  - "TemplateBinding"
  - "TemplateBindingExtension"
helpviewer_keywords: 
  - "TemplateBinding (estensioni di markup)"
  - "XAML, TemplateBinding (estensione di markup)"
ms.assetid: 1d25bbfc-dbc2-499d-9f12-419d23d4ac6a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Estensione del markup TemplateBinding
Collega il valore di una proprietà in un modello di controllo come valore di un'altra proprietà sul controllo basato su modelli.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{TemplateBinding sourceProperty}" .../>  
```  
  
## Utilizzo dell'attributo XAML \(per proprietà Set in modelli o stili\)  
  
```  
<Setter Property="propertyName" Value="{TemplateBinding sourceProperty}" .../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`propertyName`|<xref:System.Windows.DependencyProperty.Name%2A?displayProperty=fullName> della proprietà impostata nella sintassi del setter.|  
|`sourceProperty`|Altra proprietà di dipendenza esistente nel tipo basato su modelli, specificata da <xref:System.Windows.DependencyProperty.Name%2A?displayProperty=fullName>.<br /><br /> oppure<br /><br /> Nome della proprietà puntato definito da un tipo diverso rispetto al tipo di destinazione basato su modelli.  Si tratta in effetti di un oggetto <xref:System.Windows.PropertyPath>.  Vedere [Sintassi XAML di PropertyPath](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md).|  
  
## Note  
 `TemplateBinding` è un formato ottimizzato di [associazione](../../../../docs/framework/wpf/advanced/binding-markup-extension.md) per gli scenari di modelli, analogo a una `Binding` costruita con `{Binding RelativeSource={RelativeSource TemplatedParent}}`.  `TemplateBinding` è sempre un'associazione unidirezionale, anche se le proprietà implicano come impostazione predefinita l'associazione bidirezionale.  Entrambe le proprietà in questione devono essere proprietà di dipendenza.  
  
 [RelativeSource](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md) è un'altra estensione di markup che talvolta è utilizzata con o in sostituzione di `TemplateBinding` per eseguire l'associazione di proprietà relativa in un modello.  
  
 La descrizione dei modelli di controllo come concetto non viene trattata in questo argomento; per ulteriori informazioni, vedere [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md).  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Il token di stringa fornito dopo la stringa dell'identificatore `TemplateBinding` viene assegnato come valore <xref:System.Windows.TemplateBindingExtension.Property%2A> della classe dell'estensione <xref:System.Windows.TemplateBindingExtension> sottostante.  
  
 La sintassi di elementi oggetto è possibile, ma non viene mostrata poiché non ha applicazioni realistiche.  `TemplateBinding` viene utilizzato per inserire valori all'interno dei setter, tramite espressioni valutate e l'utilizzo della sintassi dell'elemento oggetto per `TemplateBinding` per riempire la sintassi dell'elemento di proprietà `<Setter.Property>` è inutilmente dettagliata.  
  
 L'oggetto `TemplateBinding` può anche essere utilizzato per un utilizzo dettagliato degli attributi che consente di specificare la proprietà <xref:System.Windows.TemplateBindingExtension.Property%2A> come coppia proprietà\=valore:  
  
```  
<object property="{TemplateBinding Property=sourceProperty}" .../>  
```  
  
 L'utilizzo dettagliato spesso è utile per le estensioni con più proprietà da impostare o nel caso in cui alcune proprietà siano facoltative.  Poiché `TemplateBinding` presenta una sola proprietà da impostare, obbligatoria, l'utilizzo dettagliato non è tipico.  
  
 Nell'implementazione del processore XAML di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.TemplateBindingExtension>.  
  
 `TemplateBinding` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Per tutte le estensioni di markup in XAML vengono utilizzati i caratteri `{` e `}` nella relativa sintassi degli attributi, vale a dire la convenzione in base alla quale il processore XAML riconosce che l'attributo deve essere elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 <xref:System.Windows.Style>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Estensione del markup RelativeSource](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md)   
 [Associazione dell'estensione di markup](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)