---
title: Tipi di enumerazione (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- enumerations [C#]
- enums [C#]
- C# Language, enums
- bit flags [C#]
ms.assetid: 64a9b731-9e3c-4336-8a09-018db2aa10b7
caps.latest.revision: 17
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
ms.openlocfilehash: 8c23c17967474af0f91c0dda6d071073234736c6
ms.lasthandoff: 03/13/2017

---
# <a name="enumeration-types-c-programming-guide"></a>Tipi di enumerazione (Guida per programmatori C#)
Un tipo di enumerazione (detto anche enumerazione o enum) rappresenta un modo efficiente per definire un set di costanti integrali denominate che possono essere assegnate a una variabile. Si supponga ad esempio di dover definire una variabile il cui valore rappresenterà un giorno della settimana. Ci sono solo sette valori significativi che la variabile potrà mai archiviare. Per definire tali valori, è possibile usare un tipo di enumerazione, dichiarato tramite la parola chiave [enum](../../csharp/language-reference/keywords/enum.md).  
  
 [!code-cs[csProgGuideEnums#1](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_1.cs)]  
  
 Per impostazione predefinita, il tipo sottostante di ogni elemento dell'enumerazione è [int](../../csharp/language-reference/keywords/int.md). È possibile specificare un altro tipo numerico integrale usando i due punti, come illustrato nell'esempio precedente. Per un elenco completo dei tipi possibili, vedere [enum (Riferimenti per C#)](../../csharp/language-reference/keywords/enum.md).  
  
 È possibile verificare i valori numerici sottostanti eseguendo il cast al tipo sottostante, come illustrato nell'esempio seguente.  
  
```csharp  
Days today = Days.Monday;  
int dayNumber =(int)today;  
Console.WriteLine("{0} is day number #{1}.", today, dayNumber);  
  
Months thisMonth = Months.Dec;  
byte monthNumber = (byte)thisMonth;  
Console.WriteLine("{0} is month number #{1}.", thisMonth, monthNumber);  
  
// Output:  
// Monday is day number #1.  
// Dec is month number #11.  
```  
  
 I vantaggi dell'uso di enum anziché di un tipo numerico sono i seguenti:  
  
-   Si specifica in modo chiaro per il codice client quali sono i valori validi per la variabile.  
  
-   In [!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)], IntelliSense elenca i valori definiti.  
  
 Quando non si specificano valori per gli elementi nell'elenco di enumeratori, i valori vengono incrementati automaticamente di 1. Nell'esempio precedente, `Days.Sunday` ha valore 0, `Days.Monday` ha valore 1 e così via. Quando si crea un nuovo oggetto `Days`, se a questo non si assegna un valore in modo esplicito, l'oggetto avrà il valore predefinito `Days.Sunday` (0). Quando si crea un enum, selezionare il valore predefinito più logico e assegnare a questo un valore pari a zero. In tal modo tutti gli enum avranno quel valore predefinito, se non è stato loro assegnato un valore in modo esplicito al momento della creazione.  
  
 Se la variabile `meetingDay` è di tipo `Days`, è possibile assegnare (senza un cast esplicito) solo uno dei valori definiti da `Days`. E se il giorno della riunione cambia, è possibile assegnare un nuovo valore da `Days` a `meetingDay`:  
  
 [!code-cs[csProgGuideEnums#4](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_2.cs)]  
  
> [!NOTE]
>  È possibile assegnare a `meetingDay` qualsiasi valore intero arbitrario. Ad esempio, questa riga di codice non genera un errore: `meetingDay = (Days) 42`. Questa impostazione, tuttavia, non è consigliabile perché l'aspettativa implicita è che una variabile enum contenga solo uno dei valori definiti dal tipo enum. L'assegnazione di un valore arbitrario a una variabile di tipo enum comporta un rischio elevato di errore.  
  
 È possibile assegnare qualsiasi valore agli elementi nell'elenco di enumeratori di un tipo di enumerazione ed è anche possibile usare valori calcolati:  
  
 [!code-cs[csProgGuideEnums#3](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_3.cs)]  
  
## <a name="enumeration-types-as-bit-flags"></a>Tipi di enumerazione come flag di bit  
 È possibile usare un tipo di enumerazione per definire flag di bit, che consentono a un'istanza del tipo di enumerazione di archiviare qualsiasi combinazione dei valori definiti nell'elenco di enumeratori. Naturalmente alcune combinazioni potrebbero non essere significative o consentite nel codice del programma.  
  
 Un enum di flag di bit viene creato applicando l'attributo <xref:System.FlagsAttribute?displayProperty=fullName> e definendo in modo appropriato i valori in modo che sia possibile eseguirvi operazioni bit per bit `AND`, `OR`, `NOT` e `XOR`. In un enum di flag di bit, includere una costante denominata con valore zero, che indica che non sono impostati flag. Assegnare a un flag un valore pari a zero solo per indicare che non sono impostati flag.  
  
 Nell'esempio seguente viene definita un'altra versione dell'enum `Days` denominata `Days2`. `Days2` dispone dell'attributo `Flags`. A ogni valore viene assegnata la successiva potenza di 2. In questo modo è possibile creare una variabile `Days2` il cui valore è `Days2.Tuesday` e `Days2.Thursday`.  
  
 [!code-cs[csProgGuideEnums#2](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_4.cs)]  
  
 Per impostare un flag su un enum, usare l'operatore `OR` bit per bit come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideEnums#6](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_5.cs)]  
  
 Per determinare se un flag specifico è impostato, usare l'operatore `AND` bit per bit come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideEnums#7](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_6.cs)]  
  
 Per altre informazioni sugli aspetti da considerare quando si definiscono tipi di enumerazione con l'attributo <xref:System.FlagsAttribute?displayProperty=fullName>, vedere <xref:System.Enum?displayProperty=fullName>.  
  
## <a name="using-the-systemenum-methods-to-discover-and-manipulate-enum-values"></a>Uso dei metodi System.Enum per individuare e modificare valori enum  
 Tutti gli enum sono istanze del tipo <xref:System.Enum?displayProperty=fullName>. Non è possibile derivare nuove classi da <xref:System.Enum?displayProperty=fullName>, ma è possibile usarne i metodi per individuare informazioni e modificare valori in un'istanza dell'enum.  
  
 [!code-cs[csProgGuideEnums#5](../../csharp/programming-guide/codesnippet/CSharp/enumeration-types_7.cs)]  
  
 Per altre informazioni, vedere <xref:System.Enum?displayProperty=fullName>.  
  
 È anche possibile creare un nuovo metodo per un enum tramite un metodo di estensione. Per altre informazioni, vedere [Procedura: Creare un nuovo metodo per una enumerazione (Guida per programmatori C#)](../../csharp/programming-guide/classes-and-structs/how-to-create-a-new-method-for-an-enumeration.md).  
  
## <a name="featured-book-chapter"></a>Capitoli del libro rappresentati  
 [More About Variables](http://go.microsoft.com/fwlink/?LinkId=221230) (Altre informazioni sulle variabili) in [Beginning Visual C# 2010](http://go.microsoft.com/fwlink/?LinkId=221214) (Introduzione a Visual C# 2010)  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Enum?displayProperty=fullName>   
 [Guida per programmatori C#](../../csharp/programming-guide/index.md)   
 [enum](../../csharp/language-reference/keywords/enum.md)
