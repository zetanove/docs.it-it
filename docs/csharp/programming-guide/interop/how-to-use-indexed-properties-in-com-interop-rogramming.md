---
title: "Procedura: Usare proprietà indicizzate nella programmazione dell&quot;interoperabilità COM (Guida per programmatori C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- indexed properties [C#]
- Office programming [C#], indexed properties
- properties [C#], indexed
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
caps.latest.revision: 20
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: ae550ba7d3f2767cf7cc64a14bc177d15f426c36
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-use-indexed-properties-in-com-interop-programming-c-programming-guide"></a>Procedura: utilizzare proprietà indicizzate nella programmazione dell'interoperabilità COM (Guida per programmatori C#)
Le *proprietà indicizzate* migliorano l'uso delle proprietà COM dotate di parametri nella programmazione C#. Tali proprietà operano congiuntamente ad altre funzionalità di Visual C#, ad esempio gli [argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md), un nuovo tipo ([dynamic](../../../csharp/language-reference/keywords/dynamic.md)) e le [informazioni sul tipo incorporate](../../../csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md), per migliorare la programmazione di Microsoft Office.  
  
 Nelle versioni precedenti di C# i metodi sono accessibili come proprietà solo se il metodo `get` non dispone di parametri e il metodo `set` ha un unico parametro valore. Non tutte le proprietà COM soddisfano tuttavia tali restrizioni. Ad esempio, la proprietà [Range](http://go.microsoft.com/fwlink/?LinkId=166053) di Excel dispone di una funzione di accesso `get` che richiede un parametro per il nome dell'intervallo. In passato, poiché non era possibile accedere direttamente alla proprietà `Range`, era necessario usare il metodo`get_Range`, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideIndexedProperties#1](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_1.cs)]  
  
 Le proprietà indicizzate consentono invece di scrivere quanto segue:  
  
 [!code-cs[csProgGuideIndexedProperties#2](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_2.cs)]  
  
> [!NOTE]
>  Nell'esempio precedente viene usata anche la funzionalità degli [argomenti facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md), che consente di omettere `Type.Missing`.  
  
 In modo analogo, per impostare il valore della proprietà `Value` di un oggetto [Range](https://msdn.microsoft.com/library/microsoft.office.interop.excel.range.aspx) in Visual C# 2008 e versioni precedenti, sono necessari due argomenti. Uno specifica un argomento per un parametro facoltativo che specifica il tipo del valore dell'intervallo. L'altro indica il valore per la proprietà `Value`. Queste tecniche vengono illustrate negli esempi riportati di seguito. Entrambe impostano il valore della cella A1 su `Name`.
  
 [!code-cs[csProgGuideIndexedProperties#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_3.cs)]  
  
 Le proprietà indicizzate consentono invece di scrivere il codice riportato di seguito.  
  
 [!code-cs[csProgGuideIndexedProperties#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_4.cs)]  
  
 Non è possibile creare proprietà indicizzate personalizzate. La funzionalità supporta solo l'utilizzo di proprietà indicizzate esistenti.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra un esempio completo. Per altre informazioni sulla configurazione di un progetto che accede all'API di Office, vedere [Procedura: Accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md).  
  
 [!code-cs[csProgGuideIndexedProperties#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-indexed-properties-in-com-interop-rogramming_5.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Uso del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Procedura: Usare argomenti denominati e facoltativi nella programmazione di Office](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [Procedura: Accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)   
 [Procedura dettagliata: Programmazione di Office](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)
