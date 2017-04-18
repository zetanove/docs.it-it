---
title: Variabile oggetto o variabile del blocco With non impostata | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID91
dev_langs:
- VB
ms.assetid: 2f03e611-f0ed-465c-99a2-a816e034faa3
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 820ef0115a6a27d77f10f4e41d95576bbd79bfa3
ms.lasthandoff: 03/13/2017

---
# <a name="object-variable-or-with-block-variable-not-set"></a>Variabile oggetto o variabile del blocco With non impostata
Riferimento a una variabile di oggetto non valido.   L'errore può essere determinato da numerose cause:  
  
-   È stata dichiarata una variabile senza specificare un tipo. Se una variabile viene dichiarata senza specificare un tipo, per impostazione predefinita per digitare `Object`.  
  
     Ad esempio, una variabile dichiarata con `Dim x` saranno di tipo `Object;` una variabile dichiarata con `Dim x As String` saranno di tipo `String`.  
  
    > [!TIP]
    >  Il `Option Strict` istruzione la tipizzazione implicita che comporta un `Object` tipo. Se si omette il tipo, si verificherà un errore in fase di compilazione. Vedere [Option Strict (istruzione)](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
-   Si sta tentando di fare riferimento a un oggetto che è stato impostato su`Nothing`  
  
     .  
  
-   Si sta tentando di accedere a un elemento di una variabile di matrice non è stato dichiarato correttamente.  
  
     Ad esempio, una matrice dichiarata come `products() As String` attiverà l'errore se si tenta di fare riferimento a un elemento della matrice `products(3) = "Widget"`. La matrice non contiene alcun elemento e viene considerata come un oggetto.  
  
-   Si sta tentando di accedere a codice all'interno di un `With...End With` bloccare prima il blocco è stato inizializzato.   Oggetto `With...End With` blocco deve essere inizializzato mediante l'esecuzione di `With` il punto di ingresso di istruzione.  
  
> [!NOTE]
>  Nelle versioni precedenti di Visual Basic o VBA è stato generato questo errore anche assegnando un valore a una variabile senza utilizzare il `Set` (parola chiave) (`x = "name"` anziché `Set x = "name"`). Il `Set` (parola chiave) non è più valido in Visual Basic .net.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Impostare `Option Strict` a `On` aggiungendo il codice seguente all'inizio del file:  
  
```vb  
Option Strict On  
```  

     When you run the project, a compiler error will appear in the **Error List** for any variable that was specified without a type.  
  
2.  Se non si desidera abilitare `Option Strict`, cercare nel codice di tutte le variabili che sono state specificate senza un tipo (`Dim x` anziché `Dim x As String`) e aggiungere il tipo previsto per la dichiarazione.  
  
3.  Assicurarsi che invece non fa riferimento a una variabile oggetto che è stata impostata su `Nothing`.  Cercare nel codice per la parola chiave `Nothing`e modificare il codice in modo che l'oggetto non è impostato su `Nothing` fino a quando non dopo che è stato fatto riferimento.  
  
4.  Assicurarsi che tutte le variabili di matrice vengono dimensionate prima di accedervi. È possibile assegnare una dimensione quando si crea la matrice (`Dim x(5) As String` anziché `Dim x() As String`), oppure utilizzare il `ReDim` (parola chiave) per impostare le dimensioni della matrice prima che si accede.  
  
5.  Assicurarsi che il `With` blocco viene inizializzato tramite l'esecuzione di `With` il punto di ingresso di istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Dichiarazione di variabili oggetto](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [ReDim (istruzione)](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Istruzione With...End With](../../../visual-basic/language-reference/statements/with-end-with-statement.md)
