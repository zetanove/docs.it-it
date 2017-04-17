---
title: "x:XData Intrinsic XAML Type | Microsoft Docs"
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
  - "x:XData"
  - "XData"
  - "xXData"
helpviewer_keywords: 
  - "XAML [XAML Services], x:XData directive element"
  - "XData in XAML [XAML Services]"
  - "x:XData XAML directive element [XAML Services]"
ms.assetid: 7ce209c2-621b-4977-b643-565f7e663534
caps.latest.revision: 17
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 17
---
# x:XData Intrinsic XAML Type
Abilita la posizione delle isole di dati XML all'interno della produzione XAML.  Gli elementi XML all'interno di `x:XData` non devono esser considerati dai processori XAML come parte dello spazio dei nomi XAML predefinito attivo o di qualsiasi altro spazio dei nomi XAML.  `x:XData` può contenere codice XML arbitrario ben formato.  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<x:XData>  
  <elementDataRoot>  
    [elementData]  
  </elementDataRoot>  
</x:XData>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`elementDataRoot`|L'unico elemento radice dell'isola di dati inclusa.  Per la maggior parte di consumer finali, l'XML che non dispone di una radice singola è considerato non valido.  In particolare, una singola radice è necessaria se `x:XData` è concepito come un'origine dati XML per WPF o come molte altre tecnologie che utilizzano i database di origine XML per l'associazione dati.|  
|`[elementData]`|Parametro facoltativo.  XML che rappresenta i dati XML.  Qualsiasi numero di elementi può essere contenuto come dati degli elementi e gli elementi annidati possono essere contenuti in altri elementi; tuttavia, le regole generali di XML sono valide.|  
  
## Note  
 Gli elementi XML all'interno di un oggetto `x:XData` possono dichiarare nuovamente tutti gli spazi dei nomi e i prefissi possibili dell'XMLDOM all'interno dei dati.  
  
 L'accesso a livello di codice a dati XML e al tipo XAML intrinseco `x:XData` è possibile nei Servizi XAML di .NET Framework mediante la classe <xref:System.Windows.Markup.XData>.  
  
## Note sull'utilizzo di WPF  
 L'oggetto `x:XData` è utilizzato principalmente come oggetto figlio di un oggetto <xref:System.Windows.Data.XmlDataProvider> o in alternativa come l'oggetto figlio della proprietà <xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=fullName> \(in XAML, viene espresso in genere nella sintassi per l'elemento dell'oggetto\).  
  
 In genere, i dati devono ridefinire lo spazio dei nomi XML di base all'interno dell'isola di dati in modo che divenga il nuovo spazio dei nomi XML predefinito \(impostato su una stringa vuota\).  Ciò è più facile per le isole di dati semplici in quanto le espressioni <xref:System.Windows.Data.Binding.XPath%2A> utilizzate per il riferimento e l'associazione ai dati possono evitare di includere i prefissi.  Per le isole di dati più complesse è possibile scegliere di definire più prefissi per i dati e di utilizzare un prefisso specifico per lo spazio dei nomi XML nella radice.  In questo caso tutti i riferimenti alle espressioni <xref:System.Windows.Data.Binding.XPath%2A> devono includere il prefisso appropriato di cui è stato eseguito il mapping dallo spazio dei nomi.  Per ulteriori informazioni, vedere [Cenni preliminari sull'associazione dati](../../../ocs/framework/wpf/data/data-binding-overview.md).  
  
 Tecnicamente, l'elemento `x:XData` può essere utilizzato come contenuto di qualsiasi proprietà di tipo <xref:System.Xml.Serialization.IXmlSerializable>.  Tuttavia, <xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=fullName> è l'unica implementazione rilevante.  
  
## Vedere anche  
 <xref:System.Windows.Data.XmlDataProvider>   
 [Cenni preliminari sull'associazione dati](../../../ocs/framework/wpf/data/data-binding-overview.md)   
 [Associazione dell'estensione di markup](../../../ocs/framework/wpf/advanced/binding-markup-extension.md)