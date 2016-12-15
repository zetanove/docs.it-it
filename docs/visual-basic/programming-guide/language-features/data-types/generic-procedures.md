---
title: "Generic Procedures in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/08/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "generic methods, type inference"
  - "generics [Visual Basic], type inference"
  - "procedures, generic"
  - "generic procedures"
  - "type inference, generics"
  - "generic methods"
  - "type inference"
  - "generics [Visual Basic], procedures"
  - "generic procedures, type inference"
ms.assetid: 95577b28-137f-4d5c-a149-919c828600e5
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Generic Procedures in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una *routine generica*, chiamata anche *metodo generico*, indica una routine definita con almeno un parametro di tipo.  Essa consente al codice chiamante di personalizzare i tipi di dati per soddisfare le relative esigenze ad ogni chiamata della routine.  
  
 Una routine non è generica semplicemente perché definita all'interno di una classe generica o di una struttura generica.  Affinché sia generica, la routine deve utilizzare almeno un parametro di tipo, oltre a tutti i normali parametri che può utilizzare.  Una classe o struttura generica può contenere routine non generiche mentre una classe, una struttura o un modulo non generico può contenere routine generiche.  
  
 Una routine generica può utilizzare i parametri di tipo contenuti nel relativo elenco di parametri normali, nel tipo restituito se ne presenta uno e nel relativo codice della routine.  
  
## Inferenza di tipi  
 È possibile chiamare una routine generica senza fornire alcun argomento di tipo.  Se la chiamata viene effettuata con questa modalità, il compilatore tenta di determinare i tipi di dati appropriati da passare agli argomenti di tipo della routine.  Questo meccanismo è denominato *inferenza di tipi*.  Nel codice riportato di seguito viene illustrata una chiamata in cui il compilatore deduce che il tipo `String` deve essere passato al parametro di tipo `t`.  
  
 [!code-vb[VbVbalrDataTypes#15](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/generic-procedures_1.vb)]  
  
 Se il compilatore non è in grado di dedurre gli argomenti di tipo dal contesto della chiamata, viene segnalato un errore.  Una possibile causa di tale errore è dovuta a una mancata corrispondenza del numero di dimensioni della matrice.  Si supponga ad esempio di definire un normale parametro come matrice di un parametro di tipo.  Se si chiama la routine generica fornendo una matrice con un numero di dimensioni differenti, la mancata corrispondenza provoca la non riuscita dell'inferenza di tipi.  Nel codice riportato di seguito viene illustrata una chiamata in cui una matrice bidimensionale viene passata a una routine che prevede una matrice unidimensionale.  
  
 `Public Sub demoSub(Of t)(ByVal arg() As t)`  
  
 `End Sub`  
  
 `Public Sub callDemoSub()`  
  
 `Dim twoDimensions(,) As Integer`  
  
 `demoSub(twoDimensions)`  
  
 `End Sub`  
  
 È possibile richiamare l'inferenza di tipi solo omettendo tutti gli argomenti di tipo.  Nel caso fornisca un argomento di tipo, sarà necessario fornirli tutti.  
  
 L'inferenza di tipi è supportata solo per le routine generiche.  Non è possibile richiamare l'inferenza di tipi su classi, strutture, interfacce o delegati generici.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio riportato di seguito viene definita una routine generica `Function` per trovare un particolare elemento in una matrice.  Viene definito un parametro di tipo e viene utilizzato per costruire i due parametri nell'elenco di parametri.  
  
### Codice  
 [!code-vb[VbVbalrDataTypes#14](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/generic-procedures_2.vb)]  
  
### Commenti  
 Nell'esempio precedente viene richiesto di confrontare `searchValue` in ogni elemento di `searchArray`.  Per garantire questa operazione, al parametro di tipo `T` viene vincolata l'implementazione dell'interfaccia <xref:System.IComparable%601>.  Nel codice viene utilizzato il metodo <xref:System.IComparable%601.CompareTo%2A> anziché l'operatore `=`, poiché non è garantito che un argomento di tipo fornito per `T` supporti l'operatore `=`.  
  
 È possibile eseguire il test della routine `findElement` mediante il codice riportato di seguito.  
  
 [!code-vb[VbVbalrDataTypes#13](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/generic-procedures_3.vb)]  
  
 Nelle chiamate precedenti a `MsgBox` vengono visualizzati rispettivamente "0", "1" e "\-1".  
  
## Vedere anche  
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Procedura: definire una classe in grado di fornire funzionalità identiche con tipi di dati diversi](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)   
 [Procedura: utilizzare una classe generica](../../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Type List](../../../../visual-basic/language-reference/statements/type-list.md)   
 [Parameter List](../../../../visual-basic/language-reference/statements/parameter-list.md)