---
title: "{} Escape Sequence / Markup Extension | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "{}"
helpviewer_keywords: 
  - "XAML [XAML Services], quotation mark (")"
  - "{} escape sequence [XAML Services]"
  - "XAML [XAML Services], {} escape sequence"
  - "XAML [XAML Services], escape sequence"
  - "quotation mark (") [XAML Services]"
  - "escape sequence [XAML Services]"
ms.assetid: 3ce3e2ad-a868-43f9-9c98-b29561cb146e
caps.latest.revision: 21
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
---
# {} Escape Sequence / Markup Extension
Fornisce la sequenza di escape di XAML per i valori di attributo.  La sequenza di escape consente ai valori successivi nell'attributo di essere interpretati come un valore letterale.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{} literalValue" .../>  
```  
  
## Utilizzo degli elementi della proprietà XAML  
  
```  
<object>  
  <object.property>  
    {} literalValue  
  </object.property>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|*literalValue*|La stringa letterale che segue la sequenza di escape.  In genere questa stringa contiene una parentesi graffa di apertura o chiusura \({ o }\).|  
  
## Note  
 La sequenza di escape \({}\) viene utilizzata in maniera tale che una parentesi graffa aperta \({\) possa essere utilizzato come carattere letterale in XAML.  
  
 I reader XAML utilizzano in genere la parentesi graffa aperta \({\) per indicare il punto di ingresso di un'estensione di markup. Tuttavia, per prima cosa, analizzano il carattere successivo per determinare se sia una parentesi graffa di chiusura \(}\).  Solo quando le due parentesi graffe \({}\) sono adiacenti, verranno hanno considerato una sequenza di escape.  
  
 Se viene incontrata la sequenza di escape, tutto il resto della stringa deve essere elaborato come una stringa dal lettore XAML.  Tuttavia, se la sequenza di escape è applicata a un membro che dispone di un convertitore di tipi, è ancora possibile che la stringa possa subire la conversione del convertitore di tipi quando è interpretata da un writer XAML.  
  
 La sequenza di escape non è un’estensione di markup e non è supportata da una classe.  Tuttavia, è una convenzione che devono rispettare i lettori XAML \(inclusi i lettori XAML personalizzati\).  
  
 Le virgolette \("\) non possono essere utilizzate come sequenza di escape in questo modo.  Se è necessario impostare un carattere di virgoletta come valore di proprietà per una proprietà noncontent, utilizzare la sintassi degli elementi proprietà e posizionare la virgoletta come stringa all’interno dell'elemento proprietà oppure utilizzare un'entità carattere XML.  Per una proprietà di contenuto, la virgoletta può essere l’intero contenuto.  
  
 La sequenza di escape \({}\) è spesso necessaria quando si specifica un tipo XML che deve includere un qualificatore dello spazio dei nomi in un percorso in cui può essere presente un'estensione di markup XAML.  Questo include l'avvio del valore di un attributo XAML all'interno di un'estensione di markup immediatamente dopo un segno di uguale \(\=\).  Nell'esempio seguente vengono illustrate le sequenze di escape per uno spazio dei nomi XML visualizzato all'inizio del valore di un attributo XAML.  
  
 [!code-xml[XLINQExample#StackPanelResources](../../../samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
  
## Vedere anche  
 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)   
 [XML Character Entities and XAML](../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md)