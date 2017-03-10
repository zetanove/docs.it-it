---
title: "Implicit and Explicit Conversions (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "conversions, type"
  - "variables [Visual Basic], changing data type"
  - "casting"
  - "conversions, data type"
  - "type conversion, implicit conversions"
  - "CType function, conversions"
  - "casting, data types"
  - "data type conversion, explicit"
  - "type conversion, explicit conversions"
  - "data types [Visual Basic], casting"
  - "conversions, implicit"
  - "explicit data type conversions"
  - "conversions"
  - "changing data types"
  - "conversions, explicit"
  - "data type conversion, implicit"
  - "implicit data type conversions"
ms.assetid: 77de1659-af8a-492c-967e-e7ef60ccce66
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# Implicit and Explicit Conversions (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una *conversione implicita* non richiede alcuna sintassi speciale nel codice sorgente.  Nell'esempio seguente, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente di convertire in modo implicito il valore di `k` in un valore a virgola mobile e precisione singola prima di assegnarlo a `q`.  
  
```  
Dim k As Integer  
Dim q As Double  
' Integer widens to Double, so you can do this with Option Strict On.  
k = 432  
q = k  
```  
  
 In una *conversione esplicita* viene utilizzata una parola chiave per la conversione del tipo.  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] offre diverse parole chiave di questo tipo che assegnano un'espressione tra parentesi al tipo di dati desiderato.  Queste parole chiave operano come funzioni, ma il compilatore genera il codice inline, pertanto l'esecuzione risulta leggermente più veloce rispetto a una chiamata di funzione.  
  
 Nell'estensione che segue dell'esempio precedente la parola chiave `CInt` converte il valore di `q` in un Integer prima di assegnarlo a `k`.  
  
```  
' q had been assigned the value 432 from k.  
q = Math.Sqrt(q)  
k = CInt(q)  
' k now has the value 21 (rounded square root of 432).  
```  
  
## Parole chiave di conversione  
 Nella tabella che segue sono illustrate le parole chiave di conversione disponibili.  
  
||||  
|-|-|-|  
|Parola chiave per la conversione del tipo|Tipo di dati in cui viene convertita un'espressione|Tipi di dati disponibili di un'espressione da convertire|  
|`CBool`|[Boolean Data Type](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `String`, `Object`|  
|`CByte`|[Byte Data Type](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|Qualsiasi tipo numerico, inclusi `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CChar`|[Char Data Type](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`String`, `Object`|  
|`CDate`|[Date Data Type](../../../../visual-basic/language-reference/data-types/date-data-type.md)|`String`, `Object`|  
|`CDbl`|[Double Data Type](../../../../visual-basic/language-reference/data-types/double-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CDec`|[Decimal Data Type](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CInt`|[Integer Data Type](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CLng`|[Long Data Type](../../../../visual-basic/language-reference/data-types/long-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CObj`|[Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)|Qualsiasi tipo|  
|`CSByte`|[SByte Data Type](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CShort`|[Short Data Type](../../../../visual-basic/language-reference/data-types/short-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CSng`|[Single Data Type](../../../../visual-basic/language-reference/data-types/single-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CStr`|[String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte`e i tipi enumerati, `Boolean`, `Char`, la matrice `Char`, `Date`, `Object`|  
|`CType`|Tipo specificato dopo la virgola \(`,`\)|Quando si effettua la conversione in un *tipo di dati elementare*, inclusa una matrice di un tipo elementare, gli stessi tipi disponibili per la corrispondente parola chiave di conversione<br /><br /> Quando si effettua la conversione in un *tipo di dati composito*, le interfacce implementate e le classi dalle quali tale tipo eredita<br /><br /> Quando si effettua la conversione in una classe o struttura sulla quale si è effettuato l'overload `CType`, tale classe o struttura|  
|`CUInt`|[UInteger Data Type](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CULng`|[ULong Data Type](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
|`CUShort`|[UShort Data Type](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|Qualsiasi tipo numerico, inclusi `Byte`, `SByte` e i tipi enumerati, `Boolean`, `String`, `Object`|  
  
## La funzione CType  
 La [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) agisce su due argomenti.  Il primo è l'espressione da convertire e il secondo il tipo di dati o la classe di oggetti di destinazione.  Tenere presente che il primo argomento deve essere un'espressione, non un tipo.  
  
 `CType` è una *funzione inline*, ovvero il codice compilato effettua la conversione, spesso senza generare una chiamata di funzione.  determinando un miglioramento delle prestazioni.  
  
 Per un confronto di `CType` con le altre parole chiave di conversione dei tipi, vedere [DirectCast Operator](../../../../visual-basic/language-reference/operators/directcast-operator.md) e [TryCast Operator](../../../../visual-basic/language-reference/operators/trycast-operator.md).  
  
### Tipi elementari  
 Nell'esempio seguente viene illustrato l'utilizzo di `CType`.  
  
```  
k = CType(q, Integer)  
' The following statement coerces w to the specific object class Label.  
f = CType(w, Label)  
```  
  
### Tipi compositi  
 È possibile utilizzare `CType` per convertire valori in tipi di dati compositi nonché in tipi di base.  È inoltre possibile utilizzarla per assegnare una classe di oggetti al tipo di una delle relative interfacce, come illustrato nell'esempio che segue.  
  
```  
' Assume class cZone implements interface iZone.  
Dim h As Object  
' The first argument to CType must be an expression, not a type.  
Dim cZ As cZone  
' The following statement coerces a cZone object to its interface iZone.  
h = CType(cZ, iZone)  
```  
  
### Tipi di matrice  
 La funzione `CType` consente inoltre di convertire i tipi di dati della matrice, come nell'esempio che segue.  
  
```  
Dim v() As classV  
Dim obArray() As Object  
' Assume some object array has been assigned to obArray.  
' Check for run-time type compatibility.  
If TypeOf obArray Is classV()  
    ' obArray can be converted to classV.  
    v = CType(obArray, classV())  
End If  
```  
  
 Per ulteriori informazioni e un esempio, vedere [Array Conversions](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md).  
  
### Tipi che definiscono CType  
 È possibile definire `CType` su una classe o una struttura definita.  Ciò consente di convertire i valori nel e dal tipo della classe o della struttura.  Per ulteriori informazioni e un esempio, vedere [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
> [!NOTE]
>  È necessario che i valori utilizzati con una parola chiave di conversione siano validi per il tipo di dati di destinazione. In caso contrario verrà generato un errore.  Se si tenta ad esempio di convertire un valore `Long` in un valore `Integer`, è necessario che il valore di `Long` sia compreso nell'intervallo di valori validi per il tipo di dati `Integer`.  
  
> [!CAUTION]
>  In fase di esecuzione la specifica di `CType` per eseguire la conversione da un tipo di classe a un altro non riesce se il tipo di origine non deriva dal tipo di destinazione.  Questo errore genera un'eccezione <xref:System.InvalidCastException>.  
  
 Se, tuttavia, uno dei tipi è una struttura o una classe definita ed è stata specificata la funzione `CType` su tale struttura o classe, è possibile eseguire correttamente una conversione se questa soddisfa i requisiti della funzione `CType`.  Vedere [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
 L'esecuzione di una conversione esplicita è anche nota come *cast* di un'espressione in un tipo di dati o una classe di oggetti specifica.  
  
## Vedere anche  
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Conversions Between Strings and Other Types](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [How to: Convert an Object to Another Type in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)