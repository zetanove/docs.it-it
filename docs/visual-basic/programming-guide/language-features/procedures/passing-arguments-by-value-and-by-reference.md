---
title: Passaggio di argomenti per valore e per riferimento (Visual Basic) | Documenti di Microsoft
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
- ByRef keyword, passing arguments by reference
- Visual Basic code, procedures
- passing arguments, by value or by reference
- ByVal keyword, passing arguments by value
- arguments [Visual Basic], passing by value or by reference
- argument passing, by value or by reference
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
caps.latest.revision: 23
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 56d1ceba14020ca7f3dc750c2318efd3e9586af0
ms.lasthandoff: 03/13/2017

---
# <a name="passing-arguments-by-value-and-by-reference-visual-basic"></a>Passaggio di argomenti per valore e per riferimento (Visual Basic)
In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], è possibile passare un argomento a una routine *dal valore* o *per riferimento*. Ciò è noto come il *meccanismo di trasferimento*, e determina se la routine può modificare l'elemento di programmazione sottostante all'argomento nel codice chiamante. La dichiarazione della routine determina il meccanismo di passaggio per ogni parametro, specificando il [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) (parola chiave).  
  
## <a name="distinctions"></a>Differenze  
 Quando si passa un argomento a una routine, occorre considerare diverse distinzioni diverse che interagiscono tra loro:  
  
-   Se l'elemento di programmazione sottostante è modificabile o meno  
  
-   Se l'argomento stesso sia modificabile o meno  
  
-   Se l'argomento sia passato per valore o riferimento  
  
-   Se il tipo di dati dell'argomento è un tipo di valore o un tipo di riferimento  
  
 Per ulteriori informazioni, vedere [le differenze tra modificabile e non modificabili argomenti](./differences-between-modifiable-and-nonmodifiable-arguments.md) e [le differenze tra il passaggio di un argomento per valore e per riferimento](./differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
## <a name="choice-of-passing-mechanism"></a>Meccanismo di passaggio  
 È consigliabile scegliere il meccanismo di passaggio attentamente per ogni argomento.  
  
-   **Protezione**. Nella scelta tra i due meccanismi di passaggio, il criterio più importante è l'esposizione delle variabili chiamanti da modificare. Il vantaggio di passare un argomento `ByRef` è che la procedura può restituire un valore per il codice chiamante tramite l'argomento. Il vantaggio di passare un argomento `ByVal` è che esso impedisce che la variabile viene modificato dalla procedura.  
  
-   **Prestazioni**. Sebbene il meccanismo di passaggio può influire sulle prestazioni del codice, la differenza è in genere irrilevante. Unica eccezione è un tipo di valore passato `ByVal`. In questo caso, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] copia il contenuto di tutti i dati dell'argomento. Pertanto, per un tipo di valore di grandi dimensioni, ad esempio una struttura, può essere più efficiente passare `ByRef`.  
  
     Per i tipi di riferimento, solo il puntatore ai dati viene copiate (quattro byte in piattaforme a 32 bit, otto byte su piattaforme a 64 bit). Pertanto, è possibile passare gli argomenti di tipo `String` o `Object` dal valore senza compromettere le prestazioni.  
  
## <a name="determination-of-the-passing-mechanism"></a>Determinazione del meccanismo di passaggio  
 La dichiarazione della routine specifica il meccanismo di passaggio per ogni parametro. Il codice chiamante non possono ignorare un `ByVal` meccanismo.  
  
 Se un parametro viene dichiarato con `ByRef`, il codice chiamante può forzare il meccanismo `ByVal` racchiudendo il nome dell'argomento tra parentesi nella chiamata. Per ulteriori informazioni, vedere [procedura: forzare un argomento sia passati per valore](./how-to-force-an-argument-to-be-passed-by-value.md).  
  
 Il valore predefinito in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli argomenti vengono passati per valore.  
  
## <a name="when-to-pass-an-argument-by-value"></a>Quando passare un argomento per valore  
  
-   Se l'elemento di codice chiamante sottostante all'argomento non è modificabile, dichiarare il parametro corrispondente [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md). Codice non è possibile modificare il valore di un elemento non è modificabile.  
  
-   Se l'elemento sottostante è modificabile, ma non si desidera la procedura per essere in grado di modificare il relativo valore, dichiarare il parametro `ByVal`. Solo il codice chiamante può modificare il valore di un elemento modificabile passato per valore.  
  
## <a name="when-to-pass-an-argument-by-reference"></a>Quando un argomento venga passato per riferimento  
  
-   Se la procedura richiede la modifica dell'elemento sottostante nel codice chiamante, dichiarare il parametro corrispondente [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md).  
  
-   Se la corretta esecuzione del codice si basa sulla procedura di modifica dell'elemento nel codice chiamante, dichiarare il parametro `ByRef`. Se viene passato per valore o se il codice chiamante esegue l'override di `ByRef` meccanismo di passaggio racchiudendo l'argomento tra parentesi, la chiamata di procedura potrebbe produrre risultati imprevisti.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene illustrato come passare gli argomenti per valore e quando passarli per riferimento. Procedura `Calculate` ha sia un `ByVal` e `ByRef` parametro. Dato un tasso di interesse, `rate`e una somma di denaro, `debt`, l'attività della procedura consiste nel calcolare un nuovo valore per `debt` che rappresenta il risultato dell'applicazione il tasso di interesse per il valore originale di `debt`. Poiché `debt` è un `ByRef` parametro, il nuovo totale viene riflesso nel valore dell'argomento nel codice chiamante che corrisponde a `debt`. Parametro `rate` è un `ByVal` parametro perché `Calculate` non deve modificare il relativo valore.  
  
### <a name="code"></a>Codice  
 [!code-vb[VbVbcnProcedures&#74;](./codesnippet/VisualBasic/passing-arguments-by-value-and-by-reference_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Procedura: passare argomenti a una routine](./how-to-pass-arguments-to-a-procedure.md)   
 [Procedura: modificare il valore di un argomento di routine](./how-to-change-the-value-of-a-procedure-argument.md)   
 [Procedura: proteggere un argomento di routine modifica del valore](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [Procedura: forzare un argomento sia passati per valore](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passaggio di argomenti in base alla posizione e in base al nome](./passing-arguments-by-position-and-by-name.md)   
 [Tipi valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
