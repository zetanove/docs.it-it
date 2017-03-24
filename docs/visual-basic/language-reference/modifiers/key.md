---
title: "Key (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AnonymousKey"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "anonymous types [Visual Basic], key"
  - "Key [Visual Basic]"
  - "Key keyword [Visual Basic]"
ms.assetid: 7697a928-7d14-4430-a72a-c9e96e8d6c11
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Key (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La parola chiave `Key` consente di specificare il comportamento per le proprietà di tipi anonimi.  Solo le proprietà che si definiscono come proprietà chiave vengono utilizzate nei test di uguaglianza tra le istanze di tipo anonimo o nel calcolo dei valori del codice hash.  I valori delle proprietà chiave non possono essere modificati.  
  
 Si definisce una proprietà di un tipo anonimo come proprietà chiave inserendo la parola chiave `Key` davanti alla dichiarazione nell'elenco di inizializzazione.  Nell'esempio riportato di seguito `Airline` e `FlightNo` sono proprietà chiave, ma `Gate` non lo è.  
  
 [!code-vb[VbVbalrAnonymousTypes#26](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_1.vb)]  
  
 Quando viene creato un nuovo tipo anonimo nuovo, eredita direttamente da <xref:System.Object>.  Il compilatore esegue l'override di tre membri ereditati: <xref:System.Object.Equals%2A>, <xref:System.Object.GetHashCode%2A>e <xref:System.Object.ToString%2A>.  Il codice di override prodotto per gli oggetti <xref:System.Object.Equals%2A> e <xref:System.Object.GetHashCode%2A> è basato sulle proprietà chiave.  Se non esistono proprietà chiave nel tipo, non viene eseguito l'override di <xref:System.Object.GetHashCode%2A> e <xref:System.Object.Equals%2A>.  
  
## Uguaglianza  
 Due istanze di tipi anonimi sono uguali solo se sono istanze dello stesso tipo e se i valori delle relative proprietà chiave sono uguali.  Negli esempi riportati di seguito, l'oggetto `flight2` è uguale all'oggetto `flight1` dell'esempio precedente poiché sono istanze dello stesso tipo anonimo e dispongono di valori corrispondenti per le proprietà chiave.  Tuttavia, l'oggetto `flight3` non è uguale all'oggetto `flight1` poiché dispone di un valore diverso per una proprietà chiave, ovvero `FlightNo`.  Il tipo dell'istanza dell'oggetto `flight4` non è uguale all'oggetto `flight1` poiché definiscono proprietà diverse come proprietà chiave.  
  
 [!code-vb[VbVbalrAnonymousTypes#27](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_2.vb)]  
  
 Se due istanze vengono dichiarate con solo proprietà non chiave identiche per nome, tipo, ordine e valore, le due istanze non sono uguali.  Un'istanza senza proprietà chiave è uguale solo a se stessa.  
  
 Per ulteriori informazioni sulle condizioni in cui due istanze di tipo anonimo sono istanze dello stesso tipo anonimo, vedere [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
## Calcolo del codice hash  
 Come per l'oggetto <xref:System.Object.Equals%2A>, la funzione hash definita nell'oggetto <xref:System.Object.GetHashCode%2A> per un tipo anonimo è basata sulle proprietà chiave del tipo.  Negli esempi seguenti viene mostrata l'interazione tra le proprietà chiave e i valori del codice hash.  
  
 Le istanze di un tipo anonimo che dispongono degli stessi valori per tutte le proprietà chiave hanno lo stesso valore di codice hash, anche se le proprietà non chiave non dispongono di valori corrispondenti.  L'istruzione seguente restituisce `True`.  
  
 [!code-vb[VbVbalrAnonymousTypes#37](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_3.vb)]  
  
 Le istanze di un tipo anonimo che dispongono di valori diversi per una o più proprietà chiave hanno valori di codice hash differenti.  L'istruzione seguente restituisce `False`.  
  
 [!code-vb[VbVbalrAnonymousTypes#38](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_4.vb)]  
  
 Le istanze di tipo anonimo che definiscono diverse proprietà come proprietà chiave non sono istanze dello stesso tipo.  Dispongono di valori di codice hash diversi anche quando i nomi e i valori di tutte le proprietà sono gli stessi.  L'istruzione seguente restituisce `False`.  
  
 [!code-vb[VbVbalrAnonymousTypes#39](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_5.vb)]  
  
## Valori di sola lettura.  
 I valori delle proprietà chiave non possono essere modificati.  Ad esempio, nell'oggetto `flight1` degli esempi descritti in precedenza, i campi `Airline` e `FlightNo` sono di sola lettura, ma l'oggetto `Gate` può essere modificato.  
  
 [!code-vb[VbVbalrAnonymousTypes#28](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_6.vb)]  
  
## Vedere anche  
 [Anonymous Type Definition](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)   
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)