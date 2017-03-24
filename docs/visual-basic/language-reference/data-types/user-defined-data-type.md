---
title: "User-Defined Data Type | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "UserDefined"
  - "UDT"
  - "vb.UDT"
  - "User-Defined"
  - "vb.UserDefined"
  - "vb.User-Defined"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "user-defined data types, Visual Basic"
  - "user-defined types"
  - "structures, as user-defined data types"
  - "user-defined types, Visual Basic"
  - "user-defined types, structure declaration"
  - "user-defined types, structures in Visual Basic"
  - "user-defined data types, structure declaration"
  - "data types [Visual Basic], assigning"
  - "Structure statement"
  - "data types [Visual Basic], user-defined"
  - "user-defined data types, structures in Visual Basic"
  - "user-defined data types"
  - "types [Visual Basic], user-defined"
ms.assetid: be913dca-a364-4a51-96a1-549a1b390b0a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# User-Defined Data Type
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene dati nel formato definito  dall'istruzione `Structure`.  
  
 Le versioni precedenti di Visual Basic supportano il tipo definito dall'utente,  mentre la versione corrente lo espande in una *struttura*.  Una struttura rappresenta una concatenazione di uno o più *membri* di vari tipi di dati.  In Visual Basic una struttura viene considerata come una singola unità, anche se è possibile accedere ai relativi membri singolarmente.  
  
## Note  
 Definire e utilizzare un tipo di dati in formato struttura quando è necessario combinare diversi tipi di dati in una singola unità oppure quando nessuno dei tipi di dati elementari soddisfa le esigenze specifiche.  
  
 Il valore predefinito di un tipo di dati in formato struttura è costituito dalla combinazione dei valori predefiniti di ciascuno dei relativi membri.  
  
## Formato della dichiarazione  
 Una dichiarazione di struttura inizia con l'[Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md) e termina con l'istruzione `End` `Structure`.  Nell'istruzione `Structure` è presente il nome della struttura, che corrisponde anche all'identificatore del tipo di dati definito dalla struttura.  Tale identificatore può essere utilizzato da altre parti del codice per dichiarare variabili, parametri e valori restituiti da funzioni come appartenenti al tipo di dati della struttura.  
  
 Le dichiarazioni contenute tra le istruzioni `Structure` ed `End` `Structure` definiscono i membri della struttura.  
  
## Livelli di accesso ai membri  
 È necessario dichiarare ciascun membro utilizzando un'[Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md) o un'istruzione in cui venga specificato il livello di accesso, ad esempio [Public](../../../visual-basic/language-reference/modifiers/public.md), [Friend](../../../visual-basic/language-reference/modifiers/friend.md) o [Private](../../../visual-basic/language-reference/modifiers/private.md).  Se si utilizza un'istruzione `Dim`, il livello di accesso predefinito è Public.  
  
## Suggerimenti per la programmazione  
  
-   **Consumo di memoria.** Come nel caso di tutti i tipi di dati compositi, il calcolo del consumo di memoria totale di una struttura in base alla somma delle allocazioni di memoria nominali dei relativi membri presenta alcuni rischi.  Non è inoltre possibile supporre con certezza che l'ordine di archiviazione in memoria corrisponda esattamente all'ordine di dichiarazione.  Se è necessario controllare il layout di archiviazione di una struttura, è possibile applicare l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> all'istruzione `Structure`.  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che i tipi definiti dall'utente in altri ambienti non sono compatibili con i tipi di struttura Visual Basic.  
  
-   **Conversione verso un tipo di dati più grande.** Non è prevista alcuna conversione automatica da o verso un qualsiasi tipo di dati in formato struttura.  Per definire gli operatori di conversione sulla struttura, è possibile utilizzare l'[Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md) e dichiarare ciascun operatore come `Widening` o `Narrowing`.  
  
-   **Caratteri tipo.** I tipi di dati in formato struttura non hanno alcun carattere di tipo letterale o carattere identificatore di tipo.  
  
-   **Tipo Framework.** Non esiste alcun tipo corrispondente in .NET Framework.  Tutte le strutture ereditano dalla classe .NET Framework <xref:System.ValueType?displayProperty=fullName>, ma nessuna struttura singola corrisponde a <xref:System.ValueType?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato il profilo della dichiarazione di una struttura.  
  
```  
[Public | Protected | Friend | Protected Friend | Private] Structure structname  
    {Dim | Public | Friend | Private} member1 As datatype1  
    ' ...  
    {Dim | Public | Friend | Private} memberN As datatypeN  
End Structure  
```  
  
## Vedere anche  
 <xref:System.ValueType>   
 <xref:System.Runtime.InteropServices.StructLayoutAttribute>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)