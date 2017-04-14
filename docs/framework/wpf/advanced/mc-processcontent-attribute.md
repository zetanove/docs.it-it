---
title: "Attributo mc:ProcessContent | Microsoft Docs"
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
  - "mc:ProcessContents (attributo)"
  - "XAML, mc:ProcessContents (attributo)"
ms.assetid: 2689b2c8-b4dc-4b71-b9bd-f95e619122d7
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Attributo mc:ProcessContent
Specifica per quali elementi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] deve ancora essere elaborato il contenuto da parte degli elementi padre rilevanti, anche se l'elemento padre immediato può essere ignorato da un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] a causa della specifica di [Attributo mc:Ignorable](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md).  L'attributo `mc:ProcessContent` supporta la compatibilità del markup sia per il mapping dello spazio dei nomi personalizzato, sia per il controllo della versione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...  
  mc:ProcessContent="ignorablePrefix:ThisElementCanBeIgnored"  
>  
    <ignorablePrefix:ThisElementCanBeIgnored>  
        [content]  
    </ignorablePrefix:ThisElementCanBeIgnored>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|*ignorablePrefix*|Qualsiasi stringa di prefisso valida, per la specifica XML 1.0.|  
|*ignorableUri*|Qualsiasi URI valido per la definizione di un spazio dei nomi, per la specifica XML 1.0.|  
|*ThisElementCanBeIgnored*|Elemento che può essere ignorato dalle implementazioni del processore [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], se il tipo sottostante non può essere risolto.|  
|*\[contenuto\]*|*ThisElementCanBeIgnored* è contrassegnato come ignorable.  Se il processore ignora tale elemento, *\[contenuto\]* viene elaborato da *oggetto*.|  
  
## Note  
 Per impostazione predefinita, un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ignorerà il contenuto di un elemento ignorato.  È possibile specificare un elemento specifico con `mc:ProcessContent`e un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] continuerà a elaborare il contenuto all'interno dell'elemento ignorato.  Questa soluzione verrebbe in genere utilizzata in caso di contenuto annidato all'interno di diversi tag, di cui almeno uno sia ignorable e almeno uno non lo sia.  
  
 È possibile specificare più prefissi nell'attributo, mediante un separatore, ad esempio: `mc:ProcessContent="ignore:Element1 ignore:Element2"`.  
  
 Lo spazio dei nomi [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)] definisce altri elementi e attributi che non sono documentati all'interno di questa area del [!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)].  Per ulteriori informazioni, vedere [XML Markup Compatibility Specification](http://go.microsoft.com/fwlink/?LinkId=73824) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 [Attributo mc:Ignorable](../../../../docs/framework/wpf/advanced/mc-ignorable-attribute.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)