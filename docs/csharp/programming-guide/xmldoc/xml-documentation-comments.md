---
title: Commenti per la documentazione XML (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.xml
dev_langs:
- CSharp
helpviewer_keywords:
- XML [C#], code comments
- comments [C#], XML
- documentation comments [C#]
- C# source code files
- C# language, XML code comments
- XML documentation comments [C#]
ms.assetid: 803b7f7b-7428-4725-b5db-9a6cff273199
caps.latest.revision: 26
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0762bd31ef7732ac6ed91a10aead9dca8050f862
ms.lasthandoff: 03/13/2017

---
# <a name="xml-documentation-comments-c-programming-guide"></a>Commenti relativi alla documentazione XML (Guida per programmatori C#)
In Visual C# è possibile creare la documentazione relativa al codice includendo elementi XML in campi di commento speciali (indicati da barre triple) nel codice sorgente, immediatamente prima del blocco di codice a cui i commenti fanno riferimento, ad esempio:  
  
```  
/// <summary>  
///  This class performs an important function.  
/// </summary>  
public class MyClass{}  
```  
  
 Quando si esegue la compilazione con l'opzione [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) il compilatore cerca tutti i tag XML presenti nel codice sorgente e crea un file di documentazione XML. Per creare la documentazione finale basata sul file generato dal compilatore, è possibile creare uno strumento personalizzato o usare uno strumento come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061).  
  
 Per fare riferimento agli elementi XML (ad esempio, la funzione elabora elementi XML specifici che si desidera descrivere in un commento della documentazione XML), è possibile utilizzare il meccanismo standard (`<` e `>`).  Per fare riferimento agli identificatori generici in elementi di riferimento di codice (`cref`), è possibile usare caratteri di escape, ad esempio `cref=”List<T>”`, o parentesi graffe (`cref=”List{T}”`).  Come caso particolare, il compilatore analizza le parentesi graffe come parentesi uncinate per rendere il commento relativo alla documentazione meno complesso da creare quando viene fatto riferimento a identificatori generici.  
  
> [!NOTE]
>  I commenti relativi alla documentazione XML non sono metadati, ovvero non vengono inclusi nell'assembly compilato e pertanto non sono accessibili mediante reflection.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)  
  
-   [Elaborazione del file XML](../../../csharp/programming-guide/xmldoc/processing-the-xml-file.md)  
  
-   [Delimitatori per i tag della documentazione](../../../csharp/programming-guide/xmldoc/delimiters-for-documentation-tags.md)  
  
-   [Procedura: Usare le funzionalità relative alla documentazione XML](../../../csharp/programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md)  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per altre informazioni, vedere:  
  
-   [/doc (elaborazione dei commenti per la documentazione)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)
