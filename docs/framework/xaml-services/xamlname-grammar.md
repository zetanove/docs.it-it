---
title: "Grammatica XamlName | Microsoft Docs"
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
  - "DottedXamlName (grammatica) [servizi XAML]"
  - "grammatica [servizi XAML], DottedXamlName"
  - "grammatica [servizi XAML], XamlName"
  - "nomi in XAML [servizi XAML]"
  - "XamlName (grammatica) [servizi XAML]"
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 13
---
# Grammatica XamlName
La grammatica XamlName è una grammatica specifica definita nella specifica di linguaggio XAML \[MS\-XAML\], riprodotta qui per convenienza.  
  
## Dalla specifica XAML  
 La specifica \[MS\-XAML\] definisce la grammatica XamlName per identificare l'insieme di identificatori simbolici validi utilizzati per tipi e proprietà.  
  
 I valori stringa di tipo XamlName devono essere conformi alla grammatica seguente:  
  
```  
XamlName ::= NameStartChar ( NameChar )*   
NameStartChar ::= LetterCharacter | '_'   
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter   
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl   
DecimalDigit ::= UnicodeNd   
CombiningCharacter ::= UnicodeMn | UnicodeMc  
  
```  
  
 che presuppone i valori di categoria generale riportati di seguito, secondo quanto definito in Unicode Character Database  
  
```  
  
Lu  
Letter, Uppercase  
Ll  
Letter, Lowercase  
Lt  
Letter, Titlecase  
Lm  
Letter, Modifier  
Lo  
Letter, Other  
Mn  
Mark, Non-Spacing  
Mc  
Mark, Spacing Combining  
Nd  
Number, Decimal  
Nl  
Number, Letter  
```  
  
 XAML definisce una seconda grammatica, DottedXamlName, utilizzata per i riferimenti completi a proprietà ed eventi, nonché per membri associati.  Per ulteriori informazioni, vedere <xref:System.Windows.DependencyProperty> e [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md).  
  
 I valori stringa di tipo DottedXamlName devono essere conformi alla grammatica seguente:  
  
```  
DottedXamlName ::= XamlName '.' XamlName  
```  
  
## Note  
 Per la specifica completa del linguaggio XAML, vedere[\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525).