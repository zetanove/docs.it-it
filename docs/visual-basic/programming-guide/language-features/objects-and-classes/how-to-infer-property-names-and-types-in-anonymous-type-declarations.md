---
title: "Procedura: dedurre tipi e nomi di propriet&#224; nelle dichiarazioni di tipo anonimo (Visual Basic) | Microsoft Docs"
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
  - "deduzione di nomi delle proprietà [Visual Basic]"
  - "tipi anonimi [Visual Basic], deduzione di nomi e tipi delle proprietà"
  - "deduzione di tipi delle proprietà [Visual Basic]"
ms.assetid: 7c748b22-913f-4d9d-b747-6b7bf296a0bc
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Procedura: dedurre tipi e nomi di propriet&#224; nelle dichiarazioni di tipo anonimo (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I tipi anonimi non offrono alcun meccanismo per specificare direttamente i tipi di dati delle proprietà. I tipi di tutte le proprietà vengono dedotti. Nell'esempio seguente, i tipi di `Name` e `Price` vengono dedotti direttamente dai valori usati per inizializzarli.  
  
 [!code-vb[VbVbalrAnonymousTypes#1](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_1.vb)]  
  
 I tipi anonimi possono anche dedurre i nomi e i tipi delle proprietà da altre origini. Le sezioni che seguono forniscono un elenco delle circostanze in cui l'inferenza è possibile e alcuni esempi di situazioni in cui non lo è.  
  
## Inferenza corretta  
  
#### I tipi anonimi possono dedurre i nomi e i tipi delle proprietà dalle origini seguenti:  
  
-   Dai nomi di variabili. Il tipo anonimo `anonProduct` avrà due proprietà, `productName` e `productPrice`. I relativi tipi di dati saranno quelli delle variabili originali, `String` e `Double`, rispettivamente.  
  
     [!code-vb[VbVbalrAnonymousTypes#11](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_2.vb)]  
  
-   Dai nomi di proprietà o di campo di altri oggetti. Si consideri ad esempio un oggetto `car` di tipo `CarClass` che include le proprietà `Name` e `ID`. Per creare una nuova istanza di tipo anonimo, `car1`, con le proprietà `Name` e `ID` inizializzate con i valori dell'oggetto `car`, è possibile scrivere quanto segue:  
  
     [!code-vb[VbVbalrAnonymousTypes#34](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_3.vb)]  
  
     La dichiarazione precedente è equivalente alla riga di codice più lunga che definisce il tipo anonimo `car2`.  
  
     [!code-vb[VbVbalrAnonymousTypes#35](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_4.vb)]  
  
-   Dai nomi di membri XML.  
  
     [!code-vb[VbVbalrAnonymousTypes#12](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_5.vb)]  
  
     Il tipo risultante per `anon` avrebbe una proprietà, `Book`, di tipo <xref:System.Collections.IEnumerable>\(di XElement\).  
  
-   Da una funzione che non ha parametri, ad esempio `SomeFunction` nell'esempio seguente.  
  
     `Dim sc As New SomeClass`  
  
     `Dim anon1 = New With {Key sc.SomeFunction()}`  
  
     La variabile `anon2` nel codice seguente è un tipo anonimo che ha una proprietà, un carattere denominato `First`. Questo codice visualizzerà una lettera "E", la lettera restituita dalla funzione <xref:System.Linq.Enumerable.First%2A>.  
  
     [!code-vb[VbVbalrAnonymousTypes#13](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_6.vb)]  
  
## Inferenze non corrette  
  
#### In molte circostanze l'inferenza del nome non avrà successo, come illustrato negli esempi seguenti:  
  
-   L'inferenza deriva dalla chiamata di un metodo, di un costruttore o di una proprietà con parametri che richiedono argomenti. La dichiarazione precedente di `anon1` ha esito negativo se `someFunction` ha uno o più argomenti.  
  
     `' Not valid.`  
  
     `' Dim anon3 = New With {Key sc.someFunction(someArg)}`  
  
     L'assegnazione a un nuovo nome della proprietà risolve il problema.  
  
     `' Valid.`  
  
     `Dim anon4 = New With {Key .FunResult = sc.someFunction(someArg)}`  
  
-   L'inferenza deriva da un'espressione complessa.  
  
    ```  
    Dim aString As String = "Act "  
    ' Not valid.  
    ' Dim label = New With {Key aString & "IV"}  
    ```  
  
     L'errore può essere risolto assegnando il risultato dell'espressione a un nome di proprietà.  
  
     [!code-vb[VbVbalrAnonymousTypes#14](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_7.vb)]  
  
-   L'inferenza per più proprietà produce due o più proprietà che hanno lo stesso nome. Riferendosi di nuovo alle dichiarazioni illustrate negli esempi precedenti, non è possibile elencare `product.Name` e `car1.Name` come proprietà dello stesso tipo anonimo, perché l'identificatore dedotto per ognuno di queste sarebbe `Name`.  
  
     `' Not valid.`  
  
     `' Dim anon5 = New With {Key product.Name, Key car1.Name}`  
  
     Il problema può essere risolto assegnando i valori a nomi di proprietà distinti.  
  
     [!code-vb[VbVbalrAnonymousTypes#36](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_8.vb)]  
  
     Si noti che le differenze di lettere maiuscole o minuscole non differenziano i due nomi.  
  
     `Dim price = 0`  
  
     `' Not valid, because Price and price are the same name.`  
  
     `' Dim anon7 = New With {Key product.Price, Key price}`  
  
-   Il tipo e il valore iniziale di una proprietà dipendono da un'altra proprietà non ancora stabilita. Ad esempio, `.IDName = .LastName` non è valido in una dichiarazione di tipo anonimo, a meno che `.LastName` non sia già stato inizializzato.  
  
     `' Not valid.`  
  
     `' Dim anon8 = New With {Key .IDName = .LastName, Key .LastName = "Jones"}`  
  
     In questo esempio, è possibile risolvere il problema invertendo l'ordine in cui sono dichiarate le proprietà.  
  
     [!code-vb[VbVbalrAnonymousTypes#15](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_9.vb)]  
  
-   Un nome di proprietà del tipo anonimo è uguale al nome di un membro di <xref:System.Object>. Ad esempio, la dichiarazione seguente ha esito negativo perché `Equals` è un metodo di <xref:System.Object>.  
  
     `' Not valid.`  
  
     `' Dim relationsLabels1 = New With {Key .Equals = "equals", Key .Greater = _`  
  
     `'                       "greater than", Key .Less = "less than"}`  
  
     È possibile risolvere il problema modificando il nome della proprietà:  
  
     [!code-vb[VbVbalrAnonymousTypes#16](../../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/how-to-infer-property-names-and-types-in-anonymous-type-declarations_10.vb)]  
  
## Vedere anche  
 [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Key](../../../../visual-basic/language-reference/modifiers/key.md)