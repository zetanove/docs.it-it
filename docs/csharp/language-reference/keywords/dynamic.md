---
title: dynamic (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- dynamic_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- dynamic [C#]
- dynamic keyword [C#]
ms.assetid: 9e797102-cc83-4964-bf58-afe4f54d16bc
caps.latest.revision: 25
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
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 7cec26e59a865e78bf02a84cfe2d3b5177fa55af
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="dynamic-c-reference"></a>dynamic (Riferimenti per C#)
`dynamic` abilita le operazioni in cui il tipo appare per ignorare il controllo del tipo in fase di compilazione. Queste operazioni vengono risolte in fase di esecuzione. Il tipo `dynamic` semplifica l'accesso alle API COM, ad esempio le API di automazione di Office, e anche ad API dinamiche come le librerie di IronPython e al modello DOM (Document Object Model) HTML.  
  
 Il tipo `dynamic` si comporta come tipo `object` nella maggior parte dei casi. Tuttavia, le operazioni che contengono espressioni di tipo `dynamic` non vengono risolte o il tipo non viene verificato dal compilatore. Il compilatore raggruppa le informazioni sull'operazione e tali informazioni successivamente vengono usate per valutare l'operazione in fase di esecuzione. Come parte del processo, le variabili di tipo `dynamic` vengono compilate in variabili di tipo `object`. Di conseguenza, il tipo `dynamic` esiste solo in fase di compilazione, non in fase di esecuzione.  
  
 Nell'esempio seguente vengono messe a confronto una variabile di tipo `dynamic` e una variabile di tipo `object`. Per verificare il tipo di ogni variabile in fase di compilazione, posizionare il puntatore del mouse su `dyn` o `obj` nelle istruzioni `WriteLine`. IntelliSense visualizza **dynamic** per `dyn` e **object** per `obj`.  
  
 [!code-cs[csrefKeywordsTypes#21](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_1.cs)]  
  
 Le istruzioni `WriteLine` visualizzano i tipi in fase di esecuzione di `dyn` e `obj`. A questo punto, entrambe hanno lo stesso tipo, un numero intero. Viene generato l'output seguente:  
  
 `System.Int32`  
  
 `System.Int32`  
  
 Per vedere la differenza tra `dyn` e `obj` in fase di compilazione, aggiungere le due righe seguenti tra le dichiarazioni e le istruzioni `WriteLine` dell'esempio precedente.  
  
```csharp  
dyn = dyn + 3;  
obj = obj + 3;  
```  
  
 Viene segnalato un errore del compilatore per il tentativo di aggiunta di un numero intero e di un oggetto nell'espressione `obj + 3`. Tuttavia non vengono segnalati errori per `dyn + 3`. L'espressione che contiene `dyn` non viene controllata in fase di compilazione perché il tipo di `dyn` è `dynamic`.  
  
## <a name="context"></a>Contesto  
 La parola chiave `dynamic` può apparire direttamente o come componente di un tipo costruito nelle situazioni seguenti:  
  
-   Nelle dichiarazioni, come tipo di proprietà, campo, indicizzatore, parametro, valore restituito, variabile locale o vincolo di tipo. La definizione di classe seguente usa `dynamic` in molte dichiarazioni diverse.  
  
     [!code-cs[csrefKeywordsTypes#22](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_2.cs)]  
  
-   Nelle conversioni di tipo esplicito, ad esempio il tipo di destinazione di una conversione.  
  
     [!code-cs[csrefKeywordsTypes#23](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_3.cs)]  
  
-   In qualsiasi contesto in cui i tipi vengono usati come valori, ad esempio sul lato destro di un operatore `is` o un operatore `as`, o come argomento di `typeof` come parte di un tipo costruito. Ad esempio, `dynamic` può essere usato nelle espressioni seguenti.  
  
     [!code-cs[csrefKeywordsTypes#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_4.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene usato `dynamic` in diverse dichiarazioni. Il metodo `Main` confronta anche il controllo dei tipi in fase di compilazione con il controllo dei tipi in fase di esecuzione.  
  
 [!code-cs[csrefKeywordsTypes#25](../../../csharp/language-reference/keywords/codesnippet/CSharp/dynamic_5.cs)]  
  
 Per altre informazioni ed esempi, vedere [Uso del tipo dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Dynamic.ExpandoObject?displayProperty=fullName>   
 <xref:System.Dynamic.DynamicObject?displayProperty=fullName>   
 [Uso del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [object](../../../csharp/language-reference/keywords/object.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [as](../../../csharp/language-reference/keywords/as.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [Procedura: Eseguire il cast sicuro usando gli operatori as e is](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md)   
 [Procedura dettagliata: Creazione e utilizzo di oggetti dinamici](../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)
