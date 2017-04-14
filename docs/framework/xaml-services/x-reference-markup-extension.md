---
title: "x:Reference Markup Extension | Microsoft Docs"
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
  - "x:Reference markup extension [XAML Services]"
  - "XAML [XAML Services], x:Reference Markup Extension"
  - "Reference markup extension [XAML Services]"
ms.assetid: 2982e68b-d26b-4aa3-826a-34c57a9c5199
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# x:Reference Markup Extension
Fa riferimento a un'istanza dichiarata altrove nel markup XAML.  Il riferimento si riferisce a `x:Name` dell'elemento.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{x:Reference instancexName}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<object>  
  <object.property>  
    <x:Reference Name="instancexName"/>  
  </object.property>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`instancexName`|Valore `x:Name` \(o valore della proprietà identificata da <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>\) dell'istanza a cui si fa riferimento.|  
  
## Note  
 `x:Reference` fornisce supporto per il livello di linguaggio XAML per un concetto di riferimento dell'elemento che diversamente è implementato nei framework specifici come WPF.  
  
## x:Reference e WPF  
 In WPF e XAML 2006, i riferimenti dell'elemento vengono indirizzati dalla funzionalità a livello di framework dell'associazione <xref:System.Windows.Data.Binding.ElementName%2A>.  Per la maggior parte delle applicazioni WPF e degli scenari, l'associazione <xref:System.Windows.Data.Binding.ElementName%2A> deve essere ancora utilizzata.  Eccezioni a questa istruzione generale potrebbero includere casi in cui ci sono il contesto dati o altre considerazioni di scopo che rendono l'associazione dati impraticabile e dove la compilazione del markup non è coinvolta.  
  
 `x:Reference` è un costrutto definito in XAML 2009.  In WPF, è possibile utilizzare le funzionalità XAML 2009, ma solo per XAML che non è compilato dal markup WPF.  XAML compilato dal markup e il form BAML di XAML non supportano attualmente le parole chiave e le funzionalità del linguaggio XAML 2009.