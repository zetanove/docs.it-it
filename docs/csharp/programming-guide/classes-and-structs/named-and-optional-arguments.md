---
title: Argomenti denominati e facoltativi (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- namedParameter_CSharpKeyword
- cs_namedParameter
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], named
- named arguments [C#]
- arguments [C#], named
- optional arguments [C#]
- arguments [C#], optional
- parameters [C#], optional
- named and optional arguments [C#]
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
caps.latest.revision: 43
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
ms.openlocfilehash: 9827553c1362d92bdf68a50e840b33474a22dcaa
ms.lasthandoff: 03/13/2017

---
# <a name="named-and-optional-arguments-c-programming-guide"></a>Argomenti denominati e facoltativi (Guida per programmatori C#)
In [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp_dev10_long_md.md)] sono stati introdotti gli argomenti denominati e facoltativi. Gli *argomenti denominati* consentono di specificare un argomento per un particolare parametro associando l'argomento al nome del parametro anziché alla posizione del parametro nell'elenco di parametri. Gli *argomenti facoltativi* consentono di omettere gli argomenti per alcuni parametri. Entrambe le tecniche possono essere usate con i metodi, gli indicizzatori, i costruttori e i delegati.  
  
 Quando si usano gli argomenti denominati e facoltativi, gli argomenti vengono valutati nell'ordine nel quale sono visualizzati nell'elenco di argomenti, non nell'elenco di parametri.  
  
 I parametri denominati e facoltativi, se usati insieme, consentono di specificare gli argomenti solo per alcuni parametri di un elenco di parametri facoltativi. Questa funzionalità semplifica considerevolmente le chiamate alle interfacce COM, ad esempio alle API di automazione di Microsoft Office.  
  
## <a name="named-arguments"></a>Argomenti denominati  
 Gli argomenti denominati evitano di dover ricordare o cercare l'ordine di parametri negli elenchi di parametri dei metodi chiamati. Il parametro per ogni argomento può essere specificato dal nome del parametro. Ad esempio, una funzione che calcola l'indice di massa corporea (BMI, Body Mass Index) può essere chiamata normalmente inviando gli argomenti relativi a peso e altezza in base alla posizione, nell'ordine definito dalla funzione.  
  
 `CalculateBMI(123, 64);`  
  
 Se non si ricorda l'ordine dei parametri ma se ne conoscono i nomi, è possibile inviare gli argomenti in qualsiasi ordine, ovvero prima il peso o prima l'altezza.  
  
 `CalculateBMI(weight: 123, height: 64);`  
  
 `CalculateBMI(height: 64, weight: 123);`  
  
 Gli argomenti denominati migliorano anche la leggibilità del codice identificando che cosa rappresenta ogni argomento.  
  
 Un argomento denominato può seguire gli argomenti posizionali, come illustrato di seguito.  
  
 `CalculateBMI(123, height: 64);`  
  
 Un argomento posizionale non può, tuttavia, seguire un argomento denominato. L'istruzione seguente causa un errore di compilazione.  
  
 `//CalculateBMI(weight: 123, 64);`  
  
## <a name="example"></a>Esempio  
 Il codice seguente implementa gli esempi di questa sezione.  
  
 [!code-cs[csProgGuideNamedAndOptional#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_1.cs)]  
  
## <a name="optional-arguments"></a>Argomenti facoltativi  
 La definizione di un metodo, un costruttore, un indicizzatore o un delegato può specificare che i parametri sono obbligatori o facoltativi. Tutte le chiamate devono specificare gli argomenti per tutti i parametri obbligatori, ma possono omettere gli argomenti per i parametri facoltativi.  
  
 Ogni parametro facoltativo ha un valore predefinito incluso nella definizione. Se per il parametro non viene inviato alcun argomento, viene usato il valore predefinito. Il valore predefinito deve essere uno dei tipi di espressioni seguenti:  
  
-   un'espressione costante;  
  
-   un'espressione del form `new ValType()`, dove `ValType` è un tipo di valore, ad esempio [enum](../../../csharp/language-reference/keywords/enum.md) o [struct](../../../csharp/programming-guide/classes-and-structs/structs.md);  
  
-   un'espressione del form [default(ValType)](../../../csharp/programming-guide/generics/default-keyword-in-generic-code.md), dove `ValType` è un tipo di valore.  
  
 I parametri facoltativi sono definiti alla fine dell'elenco di parametri, dopo eventuali parametri obbligatori. Se il chiamante specifica un argomento per un parametro di una successione di parametri facoltativi, deve specificare gli argomenti per tutti i parametri facoltativi precedenti. I gap delimitati da virgole nell'elenco di argomenti non sono supportati. Nel codice seguente, ad esempio, il metodo di istanza `ExampleMethod` viene definito con un parametro obbligatorio e due parametri facoltativi.  
  
 [!code-cs[csProgGuideNamedAndOptional#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_2.cs)]  
  
 La chiamata seguente a `ExampleMethod` genera un errore del compilatore, poiché viene specificato un argomento per il terzo parametro ma non per il secondo.  
  
 `//anExample.ExampleMethod(3, ,4);`  
  
 Se, tuttavia, si conosce il nome del terzo parametro, è possibile usare un argomento denominato per eseguire l'attività.  
  
 `anExample.ExampleMethod(3, optionalint: 4);`  
  
 IntelliSense usa le parentesi per indicare parametri facoltativi, come mostrato nell'immagine seguente.  
  
 ![Informazioni rapide di IntelliSense per il metodo ExampleMethod.](../../../csharp/programming-guide/classes-and-structs/media/optional_parameters.png "Optional_Parameters")  
Parametri facoltativi in ExampleMethod  
  
> [!NOTE]
>  È anche possibile dichiarare i parametri facoltativi usando la classe <xref:System.Runtime.InteropServices.OptionalAttribute> .NET. I parametri `OptionalAttribute` non richiedono un valore predefinito.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente il costruttore per `ExampleClass` ha un solo parametro facoltativo. Il metodo di istanza `ExampleMethod` ha un solo parametro obbligatorio, `required`, e due parametri facoltativi, `optionalstr` e `optionalint`. Il codice in `Main` illustra i diversi modi in cui è possibile richiamare il costruttore e il metodo.  
  
 [!code-cs[csProgGuideNamedAndOptional#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_3.cs)]  
  
## <a name="com-interfaces"></a>Interfacce COM  
 Gli argomenti denominati e facoltativi, insieme al supporto per gli oggetti dinamici e ad altri miglioramenti, aumentano considerevolmente l'interoperabilità con le API COM, quali le API di automazione di Office.  
  
 Ad esempio, il metodo [AutoFormat](http://go.microsoft.com/fwlink/?LinkId=148201) nell'interfaccia [Range](http://go.microsoft.com/fwlink/?LinkId=148196) di Microsoft Office Excel ha sette parametri facoltativi. Questi parametri sono illustrati nell'immagine seguente.  
  
 ![Informazioni rapide di IntelliSense per il metodo AutoFormat.](../../../csharp/programming-guide/classes-and-structs/media/autoformat_parameters.png "AutoFormat_Parameters")  
Parametri di AutoFormat  
  
 In C# 3.0 e versioni precedenti è necessario un argomento per ogni parametro, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideNamedAndOptional#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_4.cs)]  
  
 È tuttavia possibile semplificare in modo sostanziale la chiamata a `AutoFormat` mediante argomenti denominati e facoltativi, introdotti in C# 4.0. Gli argomenti denominati e facoltativi consentono di omettere l'argomento per un parametro facoltativo se non si vuole modificare il valore predefinito del parametro. Nella chiamata seguente viene specificato un valore per uno solo dei sette parametri.  
  
 [!code-cs[csProgGuideNamedAndOptional#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_5.cs)]  
  
 Per altre informazioni ed esempi, vedere [Procedura: Usare argomenti denominati e facoltativi nella programmazione di Office](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md) e [Procedura: Accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md).  
  
## <a name="overload-resolution"></a>Overload Resolution  
 L'uso di argomenti denominati e facoltativi influisce sulla risoluzione dell'overload nei modi seguenti:  
  
-   Un metodo, un indicizzatore o un costruttore è un candidato per l'esecuzione se ogni parametro è facoltativo o corrisponde, per nome o per posizione, a un solo argomento nell'istruzione chiamante e tale argomento può essere convertito nel tipo del parametro.  
  
-   Se è disponibile più di un candidato, agli argomenti specificati in modo esplicito vengono applicate le regole di risoluzione dell'overload per le conversioni preferite. Gli argomenti omessi per i parametri facoltativi vengono ignorati.  
  
-   Se due candidati sono giudicati ugualmente validi, la preferenza va a un candidato che non ha parametri facoltativi per i quali sono stati omessi gli argomenti nella chiamata. Si tratta di una conseguenza di una preferenza generale nella risoluzione dell'overload per i candidati che hanno un numero di parametri inferiore.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: Usare argomenti denominati e facoltativi nella programmazione di Office](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [Uso del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Uso dei costruttori](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)   
 [Uso degli indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)
