---
title: "Troubleshooting Procedures (Visual Basic) | Microsoft Docs"
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
  - "troubleshooting Visual Basic, procedures"
  - "procedures, troubleshooting"
  - "Visual Basic code, procedures"
  - "troubleshooting procedures"
  - "procedures, about procedures"
ms.assetid: 525721e8-2e02-4f75-b5d8-6b893462cf2b
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Troubleshooting Procedures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa pagina sono elencati alcuni problemi comuni che possono verificarsi durante l'utilizzo delle routine.  
  
## Restituzione di un tipo di matrice da una routine Function  
 Se una routine `Function` restituisce un tipo di dati matrice, non è possibile utilizzare il nome `Function` per memorizzare valori negli elementi della matrice.  Se si tenta di effettuare questa operazione, il compilatore la interpreterà come una chiamata a `Function`.  Nell'esempio riportato di seguito vengono generati errori del compilatore.  
  
 `Function allOnes(ByVal n As Integer) As Integer()`  
  
 `For i As Integer = 1 To n - 1`  
  
 `' The following statement generates a`   `COMPILER ERROR`  `.`  
  
 `allOnes(i) = 1`  
  
 `Next i`  
  
 `' The following statement generates a`   `COMPILER ERROR`  `.`  
  
 `Return allOnes()`  
  
 `End Function`  
  
 ‎L'istruzione `allOnes(i) = 1` genera un errore del compilatore poiché effettua una chiamata a `allOnes` utilizzando un argomento con tipo di dati errato \(un valore `Integer` singleton anziché una matrice `Integer`\).  L'istruzione `Return allOnes()` genera un errore del compilatore poiché effettua una chiamata a `allOnes` senza argomenti.  
  
 **Approccio corretto:** per modificare gli elementi di una matrice che deve essere restituita, è necessario definire una matrice interna come variabile locale.  Nell'esempio riportato di seguito la compilazione viene eseguita senza errori.  
  
 [!code-vb[VbVbcnProcedures#66](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_1.vb)]  
  
## Argomento non modificato dalla chiamata di routine  
 Per consentire a una routine di modificare un elemento di programmazione sottostante a un argomento nel codice chiamante, è necessario passare tale elemento per riferimento.  Tuttavia, una routine può accedere agli elementi di un argomento tipo di riferimento anche se vengono passati per valore.  
  
-   **Variabile sottostante**.  Per consentire alla routine di sostituire il valore dell'elemento variabile sottostante, è necessario che la routine dichiari il parametro [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md).  Inoltre, il codice chiamante non deve racchiudere l'argomento tra parentesi per evitare di eseguire l'override del meccanismo di passaggio `ByRef`.  
  
-   **Elementi del tipo di riferimento**.  Se si dichiara un parametro [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md), la routine non può modificare l'elemento variabile sottostante.  Tuttavia, se l'argomento è un tipo di riferimento, la routine può modificare i membri dell'oggetto ai quali punta, anche se non può sostituire il valore della variabile.  Se ad esempio l'argomento è una variabile di matrice, la routine non può assegnare una nuova matrice all'argomento, ma può modificare uno o più elementi di quest'ultimo.  Gli elementi modificati vengono riflessi nella variabile di matrice sottostante del codice chiamante.  
  
 Nell'esempio riportato di seguito vengono definite due routine che accettano una variabile di matrice per valore e operano sui relativi elementi.  La routine `increase` aggiunge semplicemente uno a ogni elemento.  La routine `replace` assegna una nuova matrice al parametro `a()`, quindi aggiunge uno a ogni elemento.  Tuttavia, la riassegnazione non ha effetto sulla variabile di matrice sottostante del codice chiamante in quanto `a()` viene dichiarato `ByVal`.  
  
 [!code-vb[VbVbcnProcedures#35](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#38](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_3.vb)]  
  
 Nell'esempio riportato di seguito vengono effettuate chiamate a `increase` e `replace`.  
  
 [!code-vb[VbVbcnProcedures#37](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_4.vb)]  
  
 Alla prima chiamata di `MsgBox` viene visualizzato "After increase\(n\): 11, 21, 31, 41".  Poiché `n` è un tipo di riferimento, `increase` può modificarne i membri, anche se viene passato `ByVal`.  
  
 Alla seconda chiamata di `MsgBox` viene visualizzato "After replace\(n\): 11, 21, 31, 41".  Poiché `n` viene passato `ByVal`, `replace` non può modificare la variabile `n` assegnando a quest'ultima una nuova matrice.  Quando `replace` crea la nuova istanza di matrice `k` e la assegna alla variabile locale `a`, perde il riferimento alla variabile `n` passata dal codice chiamante.  Quando incrementa i membri di `a`, viene influenzata solo la matrice locale `k`.  
  
 **Approccio corretto:** per modificare un elemento variabile sottostante, è necessario passarlo per riferimento.  Nell'esempio riportato di seguito viene illustrata la modifica apportata alla dichiarazione di `replace`, che consente alla routine di sostituire una matrice con un'altra nel codice chiamante.  
  
 [!code-vb[VbVbcnProcedures#64](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_5.vb)]  
  
## Impossibile definire un overload  
 Se si desidera definire una versione di overload di una routine, è necessario utilizzare lo stesso nome con una firma differente.  Se il compilatore non è in grado di distinguere la dichiarazione da un overload con la stessa firma, viene generato un errore.  
  
 La *firma* di una routine viene determinata dal nome della routine e dall'elenco dei parametri.  Ogni overload deve avere lo stesso nome di tutti gli altri overload, ma almeno uno degli altri componenti della firma deve essere differente.  Per ulteriori informazioni, vedere [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md).  
  
 Di seguito sono riportati gli elementi che, sebbene siano inclusi nell'elenco dei parametri, non sono componenti della firma di una routine:  
  
-   Parole chiave di modificatori di routine, come `Public`, `Shared` e `Static`  
  
-   Nomi di parametri  
  
-   Parole chiave di modificatori di parametro, come `ByRef` e `Optional`  
  
-   Tipo di dati del valore restituito \(fatta eccezione per gli operatori di conversione\)  
  
 Non è possibile eseguire l'overload di una routine modificando solo uno o più elementi descritti in precedenza.  
  
 **Approccio corretto:** per definire l'overload di una routine, è necessario modificare la firma.  Poiché è necessario utilizzare lo stesso nome, devono essere modificati il numero, l'ordine o i tipi di dati dei parametri.  In una routine generica è possibile modificare il numero di parametri di tipo.  In un operatore di conversione \([Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md)\) è possibile modificare il tipo restituito.  
  
### Risoluzione dell'overload mediante gli argomenti Optional e ParamArray  
 Se si esegue l'overload di una routine con uno o più parametri [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) o con un parametro [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md), è necessario evitare la duplicazione degli *overload impliciti*.  Per informazioni, vedere [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md).  
  
## Chiamata a una versione errata di una routine di overload  
 Se per una routine sono presenti diverse versioni di overload, è necessario acquisire familiarità con tutti i relativi elenchi di parametri e comprendere la modalità di risoluzione delle chiamate tra gli overload in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)],  per evitare di chiamare un overload diverso da quello desiderato.  
  
 Dopo aver stabilito l'overload da chiamare, è consigliabile attenersi alle seguenti regole:  
  
-   Specificare il numero e l'ordine corretto degli argomenti.  
  
-   I tipi di dati degli argomenti dovrebbero essere identici a quelli dei parametri corrispondenti.  In ogni caso, il tipo di dati di ciascun argomento deve essere convertito verso il tipo di dati più grande del parametro corrispondente,  anche quando l'[Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md) è impostata su `Off`.  Se un overload richiede una conversione verso un tipo di dati più piccolo dall'elenco degli argomenti, non sarà possibile chiamare tale overload.  
  
-   Se si specificano argomenti che richiedono una conversione verso un tipo di dati più grande, definire i relativi tipi di dati in modo che siano più simili possibile ai tipi di dati dei parametri corrispondenti.  Se due o più overload accettano i tipi di dati degli argomenti, il compilatore risolverà la chiamata nell'overload che richiede l'ampliamento di dati minimo.  
  
 È possibile ridurre il rischio di mancata corrispondenza tra i tipi di dati utilizzando la parola chiave di conversione della [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) durante la preparazione degli argomenti.  
  
### Errore di risoluzione dell'overload  
 Quando si chiama una routine di overload, il compilatore tenta di eliminare tutti gli overload eccetto uno.  Se l'operazione riesce, la chiamata viene risolta in questo overload.  Se vengono eliminati tutti gli overload o se non è possibile ridurre gli overload possibili a uno soltanto, viene generato un errore.  
  
 Nell'esempio riportato di seguito viene illustrato il processo di risoluzione dell'overload.  
  
 [!code-vb[VbVbcnProcedures#62](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_6.vb)]  
  
 [!code-vb[VbVbcnProcedures#63](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_7.vb)]  
  
 Durante la prima chiamata il compilatore elimina il primo overload poiché il tipo del primo argomento \(`Short`\) esegue la conversione verso il tipo di dati più piccolo \(`Byte`\) del parametro corrispondente.  Viene quindi eliminato il terzo overload poiché ogni tipo di argomento del secondo overload \(`Short` e `Single`\) esegue la conversione verso il tipo di dati più grande corrispondente del terzo overload \(`Integer` e `Single`\).  Il secondo overload richiede un minore ampliamento dei dati e viene quindi utilizzato dal compilatore per la chiamata.  
  
 Durante la seconda chiamata il compilatore non è in grado di eliminare alcun overload in base al meccanismo della conversione verso un tipo di dati più piccolo.  Viene eliminato il terzo overload per lo stesso motivo indicato nella prima chiamata, in quanto è possibile chiamare il secondo overload con un ampliamento minore dei tipi degli argomenti.  Tuttavia, il compilatore non è in grado di scegliere tra il primo e il secondo overload.  Ciascun overload dispone di un tipo di parametro definito che viene convertito verso il tipo più grande corrispondente nell'altro overload \(`Byte` in `Short` e `Single` in `Double`\).  Il compilatore, di conseguenza, genera un errore di risoluzione dell'overload.  
  
 **Approccio corretto:** per chiamare una routine di overload senza generare ambiguità, è necessario utilizzare la [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) per fare in modo che i tipi di dati degli argomenti corrispondano ai tipi dei parametri.  Nell'esempio riportato di seguito viene illustrata una chiamata a `z` che forza la risoluzione nel secondo overload.  
  
 [!code-vb[VbVbcnProcedures#65](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/troubleshooting-procedures_8.vb)]  
  
### Risoluzione dell'overload mediante gli argomenti Optional e ParamArray  
 Se due overload di una routine hanno firme identiche ma l'ultimo parametro di uno di essi è dichiarato come [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) e l'altro come [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md), il compilatore risolve una chiamata a tale routine in base al grado di corrispondenza maggiore.  Per ulteriori informazioni, vedere [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md).  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Considerations in Overloading Procedures](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)