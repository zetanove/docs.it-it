---
title: "Anonymous Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AnonymousType"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "anonymous types [Visual Basic], about anonymous types"
  - "anonymous types [Visual Basic]"
  - "types [Visual Basic], anonymous"
ms.assetid: 7b87532c-4b3e-4398-8503-6ea9d67574a4
caps.latest.revision: 46
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 46
---
# Anonymous Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Visual Basic supporta i tipi anonimi che consentono di creare oggetti senza scrivere una definizione della classe per il tipo di dati.  La classe viene generata direttamente dal compilatore.  La classe non ha un nome utilizzabile, eredita direttamente da <xref:System.Object>e contiene le proprietà specificate nella dichiarazione dell'oggetto.  Perché il nome del tipo di dati non è specificato, viene considerato un *tipo anonimo*.  
  
 Nell'esempio riportato di seguito viene dichiarato e creato un oggetto `product` variabile come istanza di un tipo anonimo che ha due proprietà, `Name` e `Price`.  
  
 [!code-vb[VbVbalrAnonymousTypes#1](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_1.vb)]  
  
 Una *espressione di query* utilizza tipi anonimi per combinare colonne di dati selezionate da una query.  Non è possibile definire il tipo di risultato in anticipo, perché non è possibile prevedere quali colonne possono venire selezionate da una particolare query.  I tipi anonimi consentono di scrivere una query che seleziona qualsiasi numero di colonne, in qualsiasi ordine.  Il compilatore crea un tipo di dati che corrisponde alle proprietà specificate e all'ordine specificato.  
  
 Negli esempi riportati di seguito, `products` è un elenco di oggetti di prodotto ognuno dei quali che dispone di molte proprietà.  Il `namePriceQuery` variabile contiene la definizione di una query che, quando viene eseguita, restituisce una raccolta di istanze di un tipo anonimo che ha due proprietà, `Name` e `Price`.  
  
 [!code-vb[VbVbalrAnonymousTypes#2](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_2.vb)]  
  
 Il `nameQuantityQuery` variabile contiene la definizione di una query che, quando viene eseguita, restituisce una raccolta di istanze di un tipo anonimo che ha due proprietà, `Name` e `OnHand`.  
  
 [!code-vb[VbVbalrAnonymousTypes#3](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_3.vb)]  
  
 Per le ulteriori informazioni sul codice creato dal compilatore per un tipo anonimo, vedere [Anonymous Type Definition](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md).  
  
> [!CAUTION]
>  Il nome del tipo anonimo viene generato dal compilatore e può variare da una compilazione a un'altra.  Il codice non deve utilizzare o non deve basarsi sul nome di un tipo anonimo perché il nome potrebbe cambiare quando un progetto viene ricompilato.  
  
## Dichiarare un tipo anonimo  
 La dichiarazione di un'istanza di un tipo anonimo utilizza un elenco di inizializzatori per specificare le proprietà del tipo.  Quando si dichiara un tipo anonimo e possibile specificare solo le proprietà , non altri elementi della classe come metodi o eventi.  Nell'esempio riportato di seguito `product1` è un'istanza di un tipo anonimo che ha due proprietà, `Name` e `Price`.  
  
 [!code-vb[VbVbalrAnonymousTypes#4](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_4.vb)]  
  
 Se si definiscono le proprietà come proprietà chiave, è possibile utilizzarle per verificare l'uguaglianza di due istanze di tipo anonimo.  Tuttavia, i valori delle proprietà chiave non possono essere modificati.  Per ulteriori informazioni, vedere la sezione Proprietà chiave più avanti in questo argomento.  
  
 Si noti che dichiarare un'istanza di un tipo anonimo è come dichiarare un'istanza di un tipo denominato utilizzando un inizializzatore di oggetto:  
  
 [!code-vb[VbVbalrAnonymousTypes#5](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_5.vb)]  
  
 Per ulteriori informazioni sulle altre modalità per specificare le proprietà di un tipo anonimo, vedere [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md).  
  
## Proprietà principali  
 Le proprietà chiave differiscono dalle proprietà non chiave in vari aspetti fondamentali:  
  
-   Per determinare se due istanze sono uguali vengono confrontati solo i valori di proprietà chiave.  
  
-   I valori delle proprietà chiave sono di sola lettura e non possono essere modificati.  
  
-   Solo valori della proprietà chiave vengono inclusi nell'algoritmo di codice hash generato dal compilatore per un tipo anonimo.  
  
### Uguaglianza  
 Istanze di tipi anonimi possono essere uguali solo se sono istanze dello stesso tipo anonimo.  Il compilatore considera due istanze come istanze dello stesso tipo se soddisfano le condizioni seguenti:  
  
-   Sono dichiarate nello stesso assembly.  
  
-   Le rispettive proprietà hanno gli stessi nomi, gli stessi tipi dedotti e vengono dichiarate nello stesso ordine.  Nel confronto tra nomi non viene applicata la distinzione tra maiuscole e minuscole.  
  
-   Vengono indicate come proprietà chiave le stesse proprietà di ognuna .  
  
-   Almeno una proprietà in ogni dichiarazione è una proprietà chiave.  
  
 Un'istanza di tipi anonimi che non ha proprietà chiave è uguale solo a se stessa.  
  
 [!code-vb[VbVbalrAnonymousTypes#6](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_6.vb)]  
  
 Due istanze di tipi anonimi sono uguali solo se i valori delle relative proprietà chiave sono uguali.  Negli esempi riportati di seguito viene illustrato come viene verificata l'uguaglianza.  
  
 [!code-vb[VbVbalrAnonymousTypes#7](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_7.vb)]  
  
### Valori di sola lettura.  
 I valori delle proprietà chiave non possono essere modificati.  Nell'esempio descritto in precedenza, `prod8` i campi `Name` e `Price` sono `read-only`, ma `OnHand` possono venire modificati.  
  
 [!code-vb[VbVbalrAnonymousTypes#8](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_8.vb)]  
  
## Tipi anonimi dalle espressioni di query  
 Le espressioni di query non richiedono sempre la creazione di tipi anonimi.  Quando è possibile, utilizzano un tipo esistente per contenere i dati della colonna.  Questa situazione si verifica quando la query restituisce record interi dall'origine dati, oppure un unico campo da ogni record.  Negli esempi di codice riportati di seguito, `customers` è una raccolta di oggetti di una classe `Customer`.  La classe dispone di molte proprietà ed è possibile includerne una o più nel risultato della query, in qualsiasi ordine.  Nei primi due esempi, non viene richiesto alcun tipo anonimo, perché le query seleziona elementi di tipi denominati:  
  
-   `custs1` contiene una raccolta di stringhe, perché `cust.Name` è una stringa.  
  
     [!code-vb[VbVbalrAnonymousTypes#30](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_9.vb)]  
  
-   `custs2` contiene una raccolta di oggetti `Customer`, perché ogni elemento di `customers` è un oggetto `Customer` e la query seleziona l'intero elemento.  
  
     [!code-vb[VbVbalrAnonymousTypes#31](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_10.vb)]  
  
 Tuttavia, non sempre sono disponibili tipi denominati adatti.  Ad esempio, potrebbe essere necessario selezionare nomi e indirizzi del cliente per un certo scopo, numeri ID e locazioni del cliente per un altro scopo e nomi del cliente, indirizzi e cronologia dell'ordine per un terzo scopo.  I tipi anonimi consentono di selezionare qualsiasi combinazione di proprietà, in qualsiasi ordine, senza prima dichiarare un nuovo tipo denominato per contenere il risultato.  Invece, il compilatore crea un tipo anonimo per ogni compilazione di proprietà.  Nella query seguente vengono selezionati solo il nome del cliente e il numero ID da ogni oggetto `Customer` in `customers`.  Pertanto, il compilatore crea un tipo anonimo che contiene solo quelle due proprietà.  
  
 [!code-vb[VbVbalrAnonymousTYpes#32](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_11.vb)]  
  
 Sia i nomi che i tipi di dati delle proprietà nel tipo anonimo vengono forniti dagli argomenti a `Select`, `cust.Name` e `cust.ID`.  Le proprietà in un tipo anonimo creato da una query sono sempre proprietà chiave.  Quando `custs3` viene eseguito nel seguente ciclo `For Each`, il risultato è una raccolta di istanze di un tipo anonimo con due proprietà chiave, `Name` e `ID`.  
  
 [!code-vb[VbVbalrAnonymousTypes#33](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_12.vb)]  
  
 Gli elementi nella raccolta rappresentata da `custs3` sono fortemente tipizzati ed è possibile utilizzare IntelliSense per spostarsi tra le proprietà disponibili e verificarne i tipi.  
  
 Per ulteriori informazioni, vedere [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  
  
## Decidere se utilizzare tipi anonimi  
 Prima di creare un oggetto come un'istanza di una classe anonima, valutare qual è la migliore opzione.  Ad esempio, se si desidera creare un oggetto temporaneo per contenere dati correlati e non sono necessari gli altri campi e metodi che una classe completa potrebbe contenere, un tipo anonimo è una buona soluzione.  I tipi anonimi sono anche efficaci se si desidera una selezione diversa di proprietà per ogni dichiarazione, o se si vuole modificare l'ordine delle proprietà.  Tuttavia, se il progetto include molti oggetti che hanno le stesse proprietà, in un ordine fisso, è possibile dichiararli più facilmente utilizzando un tipo denominato con un costruttore di classe.  Ad esempio, con un costruttore adeguato, è più facile dichiarare molte istanze di una classe `Product` rispetto a dichiarare molte istanze di un tipo anonimo.  
  
 [!code-vb[VbVbalrAnonymousTypes#9](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_13.vb)]  
  
 Un altro vantaggio dei tipi denominati è che il compilatore può intercettare un errore fortuito di digitazione di un nome della proprietà.  Negli esempi precedenti, `firstProd2`, `secondProd2`e `thirdProd2` devono essere istanze dello stesso tipo anonimo.  Tuttavia, se si volesse dichiarare accidentalmente `thirdProd2` in una delle modalità seguenti, il tipo sarebbe diverso da quello di `firstProd2` e `secondProd2`.  
  
 [!code-vb[VbVbalrAnonymousTypes#10](../../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/anonymous-types_14.vb)]  
  
 Ancora più importante, esistono limitazioni sull'utilizzo dei tipi anonimi che non valgono per le istanze di tipi denominati.  `firstProd2`, `secondProd2`, e `thirdProd2` sono istanze dello stesso tipo anonimo.  Tuttavia, il nome per il tipo anonimo condiviso non è disponibile e non può trovarsi nel codice dove è previsto un nome tipo.  Ad esempio, un tipo anonimo non può essere utilizzato per definire una firma del metodo, per dichiarare un'altra variabile o un campo o in qualsiasi dichiarazione di tipo.  Di conseguenza, i tipi anonimi non sono adatti quando è necessario condividere le informazioni tra i metodi.  
  
## Definizione di un tipo anonimo  
 In risposta alla dichiarazione di un'istanza di un tipo anonimo, il compilatore crea una nuova definizione di classe che contiene le proprietà specificate.  
  
 Se il tipo anonimo contiene almeno una proprietà chiave, la definizione esegue l'override di tre membri ereditati da <xref:System.Object>: <xref:System.Object.Equals%2A>, <xref:System.Object.GetHashCode%2A>e <xref:System.Object.ToString%2A>.  Il codice prodotto per verificare l'uguaglianza e determinare il valore del codice hash considera solo le proprietà chiave.  Se il tipo anonimo non contiene proprietà chiave, viene eseguito l'override solo di <xref:System.Object.ToString%2A>.  Le proprietà denominate in modo esplicito di un tipo anonimo non devono essere in conflitto con questi metodi generati.  Ovvero, non è possibile utilizzare `.Equals`, `.GetHashCode` o `.ToString` per denominare una proprietà.  
  
 Le definizioni di tipo anonimo che includono almeno una proprietà chiave implementano anche l'interfaccia <xref:System.IEquatable%601?displayProperty=fullName>, dove `T` è il tipo del tipo anonimo.  
  
 Per le ulteriori informazioni sul codice creato dal compilatore e le funzionalità dei metodi per eseguire l'override, vedere [Anonymous Type Definition](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md).  
  
## Vedere anche  
 [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [Anonymous Type Definition](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)   
 [Key](../../../../visual-basic/language-reference/modifiers/key.md)