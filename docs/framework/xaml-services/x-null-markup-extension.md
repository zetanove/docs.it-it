---
title: "x:Null Markup Extension | Microsoft Docs"
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
  - "NullExtension"
  - "x:NullExtension"
  - "x:Null"
  - "Null"
  - "xNull"
helpviewer_keywords: 
  - "Null markup extension in XAML [XAML Services]"
  - "x:Null markup extension [XAML Services]"
  - "XAML [XAML Services], x:Null markup extension"
ms.assetid: 2e3ccc21-4996-481d-91b5-3910d8b3bfa3
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 20
---
# x:Null Markup Extension
Specifica `null` come valore per un membro XAML.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{x:Null}" .../>  
```  
  
## Note  
 La parola chiave per un riferimento null in [!INCLUDE[TLA#tla_cshrp](../../../includes/tlasharptla-cshrp-md.md)] e [!INCLUDE[TLA#tla_cpp](../../../includes/tlasharptla-cpp-md.md)] è null.  La parola chiave [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] per un riferimento null è `Nothing`, ma si utilizza sempre `{x:Null}` come utilizzo di XAML indipendentemente da quale linguaggio code\-behind viene associato a XAML.  
  
 L’estensione di markup `x:Null` non presenta proprietà impostabili.  
  
 Un utilizzo null spesso è associato all'esposizione del membro XAML di un valore <xref:System.Nullable%601> CLR.  
  
 L'estensione di markup `x:Null`, ad esempio tutte le estensioni di markup XAML, utilizza le parentesi graffe \(`{,}`\) per l'utilizzo di caratteri di escape nella gestione dei valori di attributo affinché siano diversi da valori letterali o da riferimenti al gestore eventi.  La sintassi per gli attributi è quella utilizzata più di frequente con questa estensione di markup.  Un sintassi degli elementi oggetto `<x:Null />` è tecnicamente possibile, ma raramente è utilizzato perché l'estensione di markup `x:Null` non dispone di argomenti dei parametri posizionali o della costruzione.  
  
 Per informazioni sulle estensioni di markup, vedere [Estensioni di markup e XAML WPF](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
 Nei servizi XAML di .NET Framework la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.Markup.NullExtension>.  
  
## Note sull'utilizzo di WPF  
 Si noti che `null` non rappresenta necessariamente il valore iniziale non impostato per una proprietà di dipendenza di tipo di riferimento.  Il valore predefinito iniziale può variare per ogni proprietà di dipendenza e può essere basato sui metadati specifici della proprietà.  Molte proprietà di dipendenza non accettano `null` come valore, tramite markup o codice, a causa delle implementazioni dei callback di convalida.  Per ulteriori informazioni sulle proprietà di dipendenza, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../ocs/framework/wpf/advanced/dependency-properties-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.DependencyProperty.UnsetValue>   
 [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)