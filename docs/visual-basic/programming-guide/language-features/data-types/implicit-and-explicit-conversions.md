---
title: Conversioni implicite ed esplicite (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- conversions, type
- variables [Visual Basic], changing data type
- casting
- conversions, data type
- type conversion, implicit conversions
- CType function, conversions
- casting, data types
- data type conversion, explicit
- type conversion, explicit conversions
- data types [Visual Basic], casting
- conversions, implicit
- explicit data type conversions
- conversions
- changing data types
- conversions, explicit
- data type conversion, implicit
- implicit data type conversions
ms.assetid: 77de1659-af8a-492c-967e-e7ef60ccce66
caps.latest.revision: 25
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 24c434df4be480c290b3e4e36bd9f294d12b99ef
ms.lasthandoff: 03/13/2017

---
# <a name="implicit-and-explicit-conversions-visual-basic"></a>Conversioni implicite ed esplicite (Visual Basic)
Un *la conversione implicita* non richiede alcuna sintassi speciale nel codice sorgente. Nell'esempio seguente, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte in modo implicito il valore di `k` su un valore a virgola mobile a precisione singola prima di assegnarlo a `q`.  
  
```  
Dim k As Integer  
Dim q As Double  
' Integer widens to Double, so you can do this with Option Strict On.  
k = 432  
q = k  
```  
  
 Un *conversione esplicita* utilizza una parola chiave conversione di tipo. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce diverse parole chiave di questo tipo, che assegnano un'espressione tra parentesi al tipo di dati desiderato. Queste parole chiave operano come funzioni, ma il compilatore genera il codice inline, pertanto l'esecuzione risulta leggermente più veloci con una chiamata di funzione.  
  
 Nella seguente estensione dell'esempio precedente, il `CInt` (parola chiave) Converte il valore di `q` in un intero prima di assegnarlo a `k`.  
  
```  
' q had been assigned the value 432 from k.  
q = Math.Sqrt(q)  
k = CInt(q)  
' k now has the value 21 (rounded square root of 432).  
```  
  
## <a name="conversion-keywords"></a>Parole chiave di conversione  
 Nella tabella seguente mostra le parole chiave di conversione disponibili.  
  
|Parola chiave di conversione di tipo|Converte un'espressione di tipo di dati|Tipi di dati consentita dell'espressione da convertire|  
|---|---|---|  
|`CBool`|[Tipo di dati Boolean](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `String`,`Object`|  
|`CByte`|[Tipo di dati Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|Qualsiasi tipo numerico (inclusi `SByte` e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CChar`|[Tipo di dati Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`String`, `Object`|  
|`CDate`|[Tipo di dati Date](../../../../visual-basic/language-reference/data-types/date-data-type.md)|`String`, `Object`|  
|`CDbl`|[Tipo di dati Double](../../../../visual-basic/language-reference/data-types/double-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CDec`|[Tipo di dati Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CInt`|[Tipo di dati Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CLng`|[Tipo di dati Long](../../../../visual-basic/language-reference/data-types/long-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CObj`|[Tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)|Qualsiasi tipo|  
|`CSByte`|[Tipo di dati SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte` e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CShort`|[Tipo di dati Short](../../../../visual-basic/language-reference/data-types/short-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CSng`|[Tipo di dati Single](../../../../visual-basic/language-reference/data-types/single-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CStr`|[Tipo di dati String](../../../../visual-basic/language-reference/data-types/string-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `Char`, `Char` matrice, `Date`,`Object`|  
|`CType`|Tipo specificato dopo la virgola (`,`)|Durante la conversione di un *tipo di dati elementari* (inclusa una matrice di un tipo elementare), lo stesso tipi consentito per la corrispondente parola chiave di conversione<br /><br /> Durante la conversione di un *tipo di dati composito*, le interfacce implementate e le classi da cui eredita<br /><br /> Quando si converte in una classe o struttura in cui è effettuato l'overload `CType`, tale classe o struttura|  
|`CUInt`|[Tipo di dati UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CULng`|[Tipo di dati ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
|`CUShort`|[Tipo di dati UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|Qualsiasi tipo numerico (inclusi `Byte`, `SByte`e i tipi enumerati), `Boolean`, `String`,`Object`|  
  
## <a name="the-ctype-function"></a>CType (funzione)  
 Il [funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) opera su due argomenti. Il primo è l'espressione da convertire e il secondo è una classe oggetto o tipo di dati di destinazione. Si noti che il primo argomento deve essere un'espressione, non è un tipo.  
  
 `CType`è un *funzione inline*, vale a dire il codice compilato effettua la conversione, spesso senza la generazione di una funzione chiamata. Ciò migliora le prestazioni.  
  
 Per un confronto tra `CType` con l'altra tipo parole chiave di conversione, vedere [operatore DirectCast](../../../../visual-basic/language-reference/operators/directcast-operator.md) e [operatore TryCast](../../../../visual-basic/language-reference/operators/trycast-operator.md).  
  
### <a name="elementary-types"></a>I tipi di base  
 L'esempio seguente illustra l'uso di `CType`.  
  
```  
k = CType(q, Integer)  
' The following statement coerces w to the specific object class Label.  
f = CType(w, Label)  
```  
  
### <a name="composite-types"></a>Tipi composti  
 È possibile utilizzare `CType` per convertire i valori in tipi di dati compositi nonché in tipi di base. È possibile inoltre utilizzare per assegnare una classe di oggetto per il tipo di una delle interfacce, come nell'esempio seguente.  
  
```  
' Assume class cZone implements interface iZone.  
Dim h As Object  
' The first argument to CType must be an expression, not a type.  
Dim cZ As cZone  
' The following statement coerces a cZone object to its interface iZone.  
h = CType(cZ, iZone)  
```  
  
### <a name="array-types"></a>Tipi di matrice  
 `CType`Inoltre è possibile convertire i tipi di dati matrice, come nell'esempio seguente.  
  
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
  
 Per ulteriori informazioni e un esempio, vedere [conversioni di matrici](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md).  
  
### <a name="types-defining-ctype"></a>Tipi che definiscono CType  
 È possibile definire `CType` su una classe o una struttura definita. Ciò consente di convertire i valori da e verso il tipo di classe o struttura. Per ulteriori informazioni e un esempio, vedere [procedura: definire un operatore di conversione](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
> [!NOTE]
>  I valori utilizzati con una parola chiave di conversione devono essere validi per il tipo di dati di destinazione o si verifica un errore. Ad esempio, se si tenta di convertire un `Long` per un `Integer`, il valore di `Long` deve essere compreso nell'intervallo valido per il `Integer` tipo di dati.  
  
> [!CAUTION]
>  Specificare `CType` per convertire un tipo di classe in un altro non riesce in fase di esecuzione se il tipo di origine non deriva dal tipo di destinazione. Questo errore genera un <xref:System.InvalidCastException>(eccezione).</xref:System.InvalidCastException>  
  
 Tuttavia, se uno dei tipi è una struttura o una classe è stata definita, e se sono stati definiti `CType` su tale classe o struttura, una conversione può avere esito positivo se soddisfa i requisiti di `CType`. Vedere [procedura: definire un operatore di conversione](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
 Eseguire una conversione esplicita è noto anche come *cast* un'espressione a una classe di oggetto o tipo di dati specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Conversioni fra stringhe e altri tipi](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [Procedura: convertire un oggetto in un altro tipo in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Strutture](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Risoluzione dei problemi relativi ai tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
