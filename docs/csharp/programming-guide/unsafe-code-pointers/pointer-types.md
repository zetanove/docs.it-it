---
title: Tipi di puntatori (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.assetid: 3319faf9-336d-4148-9af2-1da2579cdd1e
caps.latest.revision: 19
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 100fa20e69c9a1cd6133437c29d1d5955e871656
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="pointer-types-c-programming-guide"></a>Tipi di puntatori (Guida per programmatori C#)
In un contesto unsafe, un tipo può essere un tipo di puntatore, un tipo di valore o un tipo di riferimento. La dichiarazione di un tipo di puntatore può assumere uno dei seguenti formati:  
  
```  
type* identifier;  
void* identifier; //allowed but not recommended  
```  
  
 I tipi seguenti possono essere tipi di puntatore:  
  
-   [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [byte](../../../csharp/language-reference/keywords/byte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [char](../../../csharp/language-reference/keywords/char.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md), [decimal](../../../csharp/language-reference/keywords/decimal.md) o [bool](../../../csharp/language-reference/keywords/bool.md).  
  
-   Qualsiasi tipo [enum](../../../csharp/language-reference/keywords/enum.md).  
  
-   Qualsiasi tipo di puntatore.  
  
-   Qualsiasi tipo struct definito dall'utente che contenga campi solo di tipi non gestiti.  
  
 I tipi di puntatore non ereditano da [object](../../../csharp/language-reference/keywords/object.md). Non sono inoltre previste conversioni tra i tipi di puntatore e `object`. Con i puntatori non sono inoltre supportate le operazioni di boxing e unboxing. È tuttavia possibile eseguire conversioni tra tipi di puntatore diversi e tra tipi di puntatore e tipi integrali.  
  
 Quando si dichiarano più puntatori nella stessa dichiarazione, l'asterisco (*) viene scritto solo con il tipo sottostante. Non viene utilizzato come prefisso di ogni nome di puntatore. Ad esempio:  
  
```  
int* p1, p2, p3;   // Ok  
int *p1, *p2, *p3;   // Invalid in C#  
```  
  
 Un puntatore non può puntare a un riferimento o a uno [struct](../../../csharp/language-reference/keywords/struct.md) che contiene riferimenti, perché un riferimento a un oggetto può essere sottoposto a processi di Garbage Collection anche se un puntatore punta a esso. Il Garbage Collector non tiene traccia degli altri tipi di puntatore che puntano all'oggetto.  
  
 Il valore della variabile del puntatore di tipo `myType*` è l'indirizzo di una variabile di tipo `myType`. Di seguito sono riportati alcuni esempi di dichiarazioni di tipi di puntatore:  
  
|Esempio|Descrizione|  
|-------------|-----------------|  
|`int* p`|`p` è un puntatore a un Integer.|  
|`int** p`|`p` è un puntatore a un puntatore a un Integer.|  
|`int*[] p`|`p` è una matrice unidimensionale di puntatori a Integer.|  
|`char* p`|`p` è un puntatore a un carattere.|  
|`void* p`|`p` è un puntatore a un tipo sconosciuto.|  
  
 Per accedere al contenuto nella posizione a cui punta la variabile del puntatore, è possibile utilizzare *, ovvero l'operatore di riferimento indiretto a puntatore. Si consideri ad esempio la seguente dichiarazione:  
  
```  
int* myVariable;  
```  
  
 L'espressione `*myVariable` indica la variabile `int` individuata all'indirizzo contenuto in `myVariable`.  
  
 Gli argomenti [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md) e [Conversioni di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-conversions.md) includono diversi esempi di puntatori.  Nell'esempio seguente viene illustrata la necessità della parola chiave `unsafe` e dell'istruzione `fixed` e come incrementare un puntatore interno.  È possibile incollare il codice nella funzione Main di un'applicazione console per eseguirlo. Ricordarsi di abilitare il codice unsafe in **Creazione progetti**. Scegliere **Progetto**, **Proprietà** nella barra dei menu e quindi selezionare **Consenti codice unsafe** nella scheda **Compilazione**.  
  
```  
// Normal pointer to an object.  
int[] a = new int[5] {10, 20, 30, 40, 50};  
// Must be in unsafe code to use interior pointers.  
unsafe  
{  
    // Must pin object on heap so that it doesn't move while using interior pointers.  
    fixed (int* p = &a[0])  
    {  
        // p is pinned as well as object, so create another pointer to show incrementing it.  
        int* p2 = p;  
        Console.WriteLine(*p2);  
        // Incrementing p2 bumps the pointer by four bytes due to its type ...  
        p2 += 1;  
        Console.WriteLine(*p2);  
        p2 += 1;  
        Console.WriteLine(*p2);  
        Console.WriteLine("--------");  
        Console.WriteLine(*p);  
        // Deferencing p and incrementing changes the value of a[0] ...  
        *p += 1;  
        Console.WriteLine(*p);  
        *p += 1;  
        Console.WriteLine(*p);  
    }  
}  
  
Console.WriteLine("--------");  
Console.WriteLine(a[0]);  
Console.ReadLine();  
  
// Output:  
//10  
//20  
//30  
//--------  
//10  
//11  
//12  
//--------  
//12  
```  
  
 Non è possibile applicare l'operatore di riferimento indiretto a un puntatore di tipo `void*`. È tuttavia possibile eseguire un cast per convertire un puntatore void in qualsiasi altro tipo e viceversa.  
  
 Un puntatore può essere `null`. Se l'operatore di riferimento indiretto viene applicato a un puntatore Null, si otterrà un comportamento definito dall'implementazione.  
  
 Tenere presente che il passaggio di puntatori tra metodi può generare un comportamento non definito, ad esempio se un puntatore viene restituito a una variabile locale tramite un parametro Out o Ref oppure come risultato della funzione. Se il puntatore è stato impostato in un blocco fisso, la variabile a cui punta potrebbe non essere più fissa.  
  
 Nella tabella riportata di seguito sono elencati gli operatori e le istruzioni che è possibile utilizzare con i puntatori in un contesto unsafe:  
  
|Operatore/istruzione|Uso|  
|-------------------------|---------|  
|*|Esegue il riferimento indiretto al puntatore.|  
|->|Accede a un membro di struct tramite un puntatore.|  
|[]|Indicizza un puntatore.|  
|`&`|Ottiene l'indirizzo di una variabile.|  
|++ e --|Incrementa e decrementa puntatori.|  
|+ e -|Utilizza l'aritmetica dei puntatori.|  
|==, !=, \<, >, \<= e >=|Confronta puntatori.|  
|`stackalloc`|Alloca memoria nello stack.|  
|Istruzione `fixed`|Corregge temporaneamente una variabile per consentire di trovarne l'indirizzo.|  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Conversioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-conversions.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)   
 [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md)

