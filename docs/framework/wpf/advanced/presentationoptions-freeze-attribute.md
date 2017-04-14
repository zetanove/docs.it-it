---
title: "Attributo PresentationOptions:Freeze | Microsoft Docs"
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
  - "Freezable (elementi)"
  - "Freeze (attributo)"
  - "PresentationOptions (prefisso)"
ms.assetid: 391032dd-2fba-4804-bb8a-3b071797a9f4
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Attributo PresentationOptions:Freeze
Consente di impostare lo stato di <xref:System.Windows.Freezable.IsFrozen%2A> su `true` sull'elemento <xref:System.Windows.Freezable> che lo contiene.  Il comportamento predefinito per <xref:System.Windows.Freezable> senza l'attributo `PresentationOptions:Freeze` specificato presuppone che <xref:System.Windows.Freezable.IsFrozen%2A> sia `false` al momento del caricamento e dipendente dal comportamento di <xref:System.Windows.Freezable> generale in fase di esecuzione.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object  
  xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="PresentationOptions">  
    <freezableElement PresentationOptions:Freeze="true"/>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`PresentationOptions`|Prefisso dello spazio dei nomi XML, che può essere qualsiasi stringa di prefisso valida in base alla specifica XML 1.0.  In questa discussione, il prefisso `PresentationOptions` viene utilizzato per scopi di identificazione.|  
|`freezableElement`|Elemento che crea un'istanza di qualsiasi classe derivata di <xref:System.Windows.Freezable>.|  
  
## Note  
 L'attributo `Freeze` è il solo attributo o altro elemento di programmazione definito nello spazio dei nomi XML `http://schemas.microsoft.com/winfx/2006/xaml/presentation/options`.  L'attributo `Freeze` viene specificamente incluso in questo spazio dei nomi speciale in modo da poter essere definito come ignorable, utilizzando [Attributo mc:Ignorable](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md) come parte delle dichiarazioni dell'elemento radice.  Il motivo per cui `Freeze` deve essere in grado di essere impostato come ignorable è che non tutte le implementazioni del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] sono in grado di bloccare <xref:System.Windows.Freezable> al momento del caricamento; questa funzionalità non fa parte della specifica [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 La possibilità di elaborare l'attributo `Freeze` è specificamente incorporata nell processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che elabora [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] per le applicazioni compilate.  L'attributo non è supportato da tutte le classi e la sintassi degli attributi non è estendibile o modificabile.  Se si sta implementando il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è possibile scegliere di affiancare il comportamento di blocco del processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)][!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in caso di elaborazione dell'attributo `Freeze` sugli elementi <xref:System.Windows.Freezable> al momento del caricamento.  
  
 Qualsiasi valore per l’attributo `Freeze` diverso da `true` \(in cui non viene applicata la distinzione tra maiuscole e minuscole\) genera un errore al momento del caricamento.  \(la specifica dell'attributo `Freeze` come `false` non costituisce un errore, ma rappresenta già l’impostazione predefinita, quindi impostare l'attributo su `false` non genera alcun effetto\).  
  
## Vedere anche  
 <xref:System.Windows.Freezable>   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Attributo mc:Ignorable](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)