---
title: "x:Array Markup Extension | Microsoft Docs"
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
  - "x:Array"
  - "xArray"
helpviewer_keywords: 
  - "x:Array [XAML Services]"
  - "XAML [XAML Services], x:Array markup extension"
ms.assetid: c5358e14-d24c-44c7-b5eb-6062a4fd981c
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 20
---
# x:Array Markup Extension
Fornisce supporto generale per matrici di oggetti in XAML, tramite una gestione delle estensioni di markup.  Corrisponde al tipo XAML `x:ArrayExtension` in \[MS\-XAML\].  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<x:Array Type="typeName">  
  arrayContents  
</x:Array>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`typeName`|Nome del tipo che conterrà `x:Array`.  È possibile che `typeName` siano premessi \(spesso è così\) per uno spazio dei nomi XAML che contiene le definizioni del tipo XAML.|  
|`arrayContents`|Contenuto degli elementi assegnato alla proprietà `ArrayExtension.Items` intrinseca.  In genere, questi elementi vengono specificati come uno o più elementi oggetto contenuti all'interno di `x:Array` che aprono e chiudono tag.  Gli oggetti qui specificati saranno probabilmente assegnabili al tipo XAML specificato in `typeName`.|  
  
## Note  
 L'oggetto `Type` è un attributo necessario per tutti gli elementi oggetto `x:Array`.  Valore di parametro `Type` non deve utilizzare un'estensione di markup `x:Type`; il nome breve del tipo è un tipo XAML, che può essere specificato come stringa.  
  
 Nell'implementazione dei servizi XAML di .NET Framework, la relazione tra il tipo XAML di input e il CLR di output <xref:System.Type> della matrice creata è influenzata dal contesto di servizio delle estensioni di markup.  L'output <xref:System.Type> è il <xref:System.Xaml.XamlType.UnderlyingType%2A> del tipo XAML dell'input, dopo avere cercato il <xref:System.Xaml.XamlType> necessario in base al contesto dello schema XAML e al servizio <xref:System.Windows.Markup.IXamlTypeResolver> fornito dal contesto.  
  
 In caso di elaborazione, i contenuti della matrice sono assegnati alla proprietà intrinseca `ArrayExtension.Items`.  Nell'implementazione <xref:System.Windows.Markup.ArrayExtension>, viene da rappresentato <xref:System.Windows.Markup.ArrayExtension.Items%2A?displayProperty=fullName>.  
  
 Nell'implementazione dei servizi XAML di .NET Framework la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.Markup.ArrayExtension>.  <xref:System.Windows.Markup.ArrayExtension> non è sealed e potrebbe essere utilizzata come base per l'implementazione di un'estensione di markup per un tipo di matrice personalizzato.  
  
 `x:Array` è prevalentemente destinato all'estensibilità del linguaggio generale in XAML.  Tuttavia, `x:Array` può essere utile anche per specificare valori XAML di determinate proprietà mediante raccolte supportate in XAML come contenuto strutturato della proprietà.  Ad esempio, è possibile specificare il contenuto di una proprietà <xref:System.Collections.IEnumerable> con un utilizzo `x:Array`.  
  
 `x:Array` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  `x:Array` è parzialmente un'eccezione a quella regola, perché anziché fornire una gestione del valore dell'attributo alternativa, `x:Array` fornisce una gestione alternativa del contenuto di testo interno.  In tal modo i tipi che potrebbero non essere supportati da alcun modello di contenuto esistente possono essere raggruppati in una matrice e utilizzati come riferimento in un secondo momento all'interno del code\-behind mediante l'accesso alla matrice denominata e la chiamata ai metodi <xref:System.Array> per ottenere singoli elementi della matrice.  
  
 Per tutte le estensioni di markup in XAML vengono utilizzate le parentesi graffe \({,}`)` nella relativa sintassi degli attributi, vale a dire la convenzione in base alla quale il processore XAML riconosce che l'attributo deve essere elaborato da un'estensione di markup.  Per informazioni dettagliate sulle estensioni di markup, vedere [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md).  
  
 In XAML 2009, `x:Array` è definito come un tipo primitivo del linguaggio piuttosto che come un'estensione di markup.  Per ulteriori informazioni, vedere [Built\-in Types for Common XAML Language Primitives](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md).  
  
## Note sull'utilizzo di WPF  
 Generalmente, gli elementi oggetto che popolano un oggetto `x:Array` in genere non sono elementi che esistono nello spazio dei nomi XAML di [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] e richiedono un mapping del prefisso allo spazio dei nomi XAML non predefinito.  
  
 Ad esempio, gli elementi seguenti sono una semplice matrice di due stringhe, con il prefisso `sys` \(nonché `x`\) definito a livello della matrice.  
  
 \[xaml\]  
  
 `<x:Array Type="sys:String" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 `xmlns:sys="clr-namespace:System;assembly=mscorlib">`  
  
 `<sys:String>Hello</sys:String>`  
  
 `<sys:String>World</sys:String>`  
  
 `</x:Array>`  
  
 Per i tipi personalizzati utilizzati come elementi matrice, la classe deve inoltre supportare i requisiti che ne consentono la creazione di istanze in XAML come elementi oggetto.  Per ulteriori informazioni, vedere [Classi XAML e personalizzate per WPF](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md).  
  
## Vedere anche  
 [Estensioni di markup e XAML WPF](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)