---
title: "xml:lang Handling in XAML | Microsoft Docs"
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
  - "XAML [XAML Services], xml:lang attribute"
  - "xml:lang attribute [XAML Services]"
  - "RFC 3066 standard [XAML Services]"
  - "standards [XAML Services], RFC 3066"
ms.assetid: 7aac0078-a1c5-41f8-b8b0-975510d9dca0
caps.latest.revision: 16
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 15
---
# xml:lang Handling in XAML
L'attributo `xml:lang` è un attributo definito da [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)] che dichiara le informazioni relative a lingua e cultura per un elemento in XML. Il significato dell'attributo rimane persistente in XAML. Tuttavia, sono valide alcune considerazioni aggiuntive.  
  
## Uso della sintassi XAML per gli attributi  
  
```  
<object xml:lang="rfc3066lang" />  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|*rfc3066lang*|Stringa derivata dallo standard [RFC 3066](http://go.microsoft.com/fwlink/?LinkId=132454) che identifica una lingua o un'area linguistica. Se identifica un'area linguistica, la lingua e l'area sono separate da un trattino. Per altre informazioni su valori e formato, vedere <xref:System.Windows.Markup.XmlLanguage>.|  
  
## Note  
 La definizione dell'attributo `xml:lang` in [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] è derivata dall'attributo `xml:lang` definito come "attributo speciale" da [!INCLUDE[TLA#tla_w3c](../../../includes/tlasharptla-w3c-md.md)] per [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]. Le informazioni su lingua e cultura sono potenzialmente elaborate in modi diversi in base agli elementi, a seconda delle relative implementazioni. Tuttavia, non esiste alcuna elaborazione [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] predefinita dell'attributo `xml:lang`.  
  
 Il valore predefinito dell'attributo `xml:lang` è una stringa vuota a livello di attributo.  
  
 Gli effetti e il valore dell'attributo `xml:lang` vengono in genere trasferiti agli elementi figlio, quando vengono interpretati da sistemi che usano i valori `xml:lang`.  
  
 Quando sono interpretati da writer XAML dei servizi di .NET Framework XAML, un valore `xml:lang` può creare oggetti <xref:System.Windows.Markup.XmlLanguage> o <xref:System.Globalization.CultureInfo> nella rappresentazione dell'oggetto sottostante. Tuttavia, tale comportamento dipende dal fatto che il valore specificato per `xml:lang` sia una costruzione valida per tali classi.  
  
 I framework possono creare associazioni tra le proprietà definite dal framework e il significato di `xml:lang` in XML mediante l'applicazione di <xref:System.Windows.Markup.XmlLangPropertyAttribute> alla proprietà.  
  
## Nodi di uso di WPF  
 Per gli elementi che sono classi derivate di <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>, è possibile usare l'equivalente proprietà di dipendenza <xref:System.Windows.FrameworkElement.Language%2A> anziché l'attributo `xml:lang`. Per impostazione predefinita, la proprietà <xref:System.Windows.FrameworkElement.Language%2A> usa "en\-US" se non viene specificato un valore diverso tramite la proprietà o tramite l'elaborazione dell'attributo `xml:lang`.  
  
## Vedere anche  
 [Globalizzazione per WPF](../../../ocs/framework/wpf/advanced/globalization-for-wpf.md)