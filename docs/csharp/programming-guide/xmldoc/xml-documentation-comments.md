---
title: "Commenti relativi alla documentazione XML (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "cs.xml"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, XML (commenti del codice)"
  - "file di codice sorgente C#"
  - "commenti [C#], XML"
  - "commenti sulla documentazione [C#]"
  - "XML [C#], commenti del codice"
  - "commenti sulla documentazione XML (C#)"
ms.assetid: 803b7f7b-7428-4725-b5db-9a6cff273199
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Commenti relativi alla documentazione XML (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In Visual C\# è possibile creare la documentazione relativa al codice includendo elementi XML in campi di commento speciali \(indicati da barre triple\) nel codice sorgente, immediatamente prima del blocco di codice a cui i commenti fanno riferimento, ad esempio:  
  
```  
/// <summary>  
///  This class performs an important function.  
/// </summary>  
public class MyClass{}  
```  
  
 Quando si esegue la compilazione con l'opzione [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md), il compilatore cerca tutti i tag XML presenti nel codice sorgente e crea un file di documentazione XML.  Per creare la documentazione finale basata sul file generato dal compilatore, è possibile creare uno strumento personalizzato o utilizzare uno strumento come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061).  
  
 Per fare riferimento agli elementi XML \(ad esempio, la funzione elabora elementi XML specifici che si desidera descrivere in un commento della documentazione XML\), è possibile utilizzare il meccanismo standard \(`<` e `>`\).  Per fare riferimento agli identificatori generici in elementi di riferimento di codice \(`cref`\), è possibile utilizzare caratteri di escape \(ad esempio, `cref=”List<T>”`\) o parentesi graffe \(`cref=”List{T}”`\).  Come caso particolare, il compilatore analizza le parentesi graffe come parentesi uncinate per rendere il commento relativo alla documentazione meno complesso da creare quando viene fatto riferimento a identificatori generici.  
  
> [!NOTE]
>  I commenti relativi alla documentazione XML non sono metadati, ovvero non vengono inclusi nell'assembly compilato e pertanto non sono accessibili mediante reflection.  
  
## Argomenti della sezione  
  
-   [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)  
  
-   [Elaborazione del file XML](../../../csharp/programming-guide/xmldoc/processing-the-xml-file.md)  
  
-   [Delimitatori per i tag della documentazione](../../../csharp/programming-guide/xmldoc/delimiters-for-documentation-tags.md)  
  
-   [Procedura: utilizzare le funzionalità relative alla documentazione XML](../../../csharp/programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md)  
  
## Sezioni correlate  
 Per ulteriori informazioni, vedere:  
  
-   [\/doc \(elaborazione dei commenti per la documentazione\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)