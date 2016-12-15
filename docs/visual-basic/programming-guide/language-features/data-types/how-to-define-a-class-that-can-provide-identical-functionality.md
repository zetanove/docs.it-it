---
title: "Procedura: definire una classe in grado di fornire funzionalit&#224; identiche con tipi di dati diversi (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "argomenti del tipo di dati, uso"
  - "parametri di tipo, definizione"
  - "argomenti del tipo di dati, definizione"
  - "argomenti [Visual Basic], tipi di dati"
  - "Of (parola chiave), uso"
  - "vincoli, Visual Basic (tipi generici)"
  - "parametri generici"
  - "parametri del tipo di dati"
  - "parametri del tipo di dati, uso"
  - "generics [Visual Basic], definizione di classi con parametri di tipo"
  - "tipi di dati [Visual Basic], come parametri"
  - "tipi di dati [Visual Basic], come argomenti"
  - "parametri, tipo"
  - "argomenti di tipo"
  - "tipi [Visual Basic], generici"
  - "parametri, generici"
  - "parametri di tipo"
  - "argomenti del tipo di dati"
  - "parametri, tipo di dati"
  - "generics [Visual Basic], definizione di tipi generici"
  - "parametri del tipo di dati, definizione"
  - "argomenti di tipo, definizione"
  - "argomenti [Visual Basic], tipo"
ms.assetid: a914adf8-e68f-4819-a6b1-200d1cf1c21c
caps.latest.revision: 29
caps.handback.revision: 29
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura: definire una classe in grado di fornire funzionalit&#224; identiche con tipi di dati diversi (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile definire una classe dalla quale creare oggetti in grado di fornire funzionalità identiche su tipi di dati diversi. A questo scopo, specificare uno o più *parametri di tipo* nella definizione. La classe potrà quindi servire come modello per gli oggetti che usano tipi di dati diversi. Una classe definita in questo modo viene denominata *classe generica*.  
  
 Il vantaggio della definizione di una classe generica sta nel fatto che viene definita un'unica volta e che può essere usata dal codice per la creazione di molti oggetti che usano una vasta gamma di tipi di dati. Questo comporta prestazioni superiori rispetto alla definizione della classe con il tipo `Object`.  
  
 Oltre alle classi, è possibile definire e usare anche strutture, interfacce, routine e delegati generici.  
  
### Per definire una classe con un parametro di tipo  
  
1.  Definire la classe nel modo normale.  
  
2.  Aggiungere `(Of` *parametrotipo*`)` subito dopo il nome della classe per specificare il parametro di tipo.  
  
3.  Se esiste più di un parametro di tipo, creare un elenco separato da virgole all'interno delle parentesi. Non ripetere la parola chiave `Of`.  
  
4.  Se le operazioni eseguite dal codice su un parametro di tipo sono diverse da una semplice assegnazione, far seguire il parametro di tipo da una clausola `As` per l'aggiunta di uno o più *vincoli*. Un vincolo garantisce che il tipo fornito per tale parametro di tipo soddisfi un requisito, ad esempio:  
  
    -   Supporta un'operazione, quale `>`, eseguita dal codice  
  
    -   Supporta un membro, quale un metodo, a cui accede il codice  
  
    -   Espone un costruttore senza parametri  
  
     Se non si specifica alcun vincolo, le uniche operazioni e gli unici membri usati dal codice sono quelli supportati dal [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md). Per altre informazioni, vedere [Type List](../../../../visual-basic/language-reference/statements/type-list.md).  
  
5.  Identificare ogni membro di classi da dichiarare con un tipo fornito e dichiararlo `As` `typeparameter`.  Questo vale per l'archiviazione interna, i parametri di routine e i valori restituiti.  
  
6.  Accertarsi che il codice usi solo operazioni e metodi supportati da qualsiasi tipo di dati che può fornire a `itemType`.  
  
     Nell'esempio riportato di seguito viene definita una classe che gestisce un elenco molto semplice. L'elenco è contenuto negli `items` della matrice interna e il tipo di dati degli elementi dell'elenco può essere dichiarato dal codice. Un costruttore con parametri consente al codice di impostare il limite superiore di `items`, quindi il costruttore predefinito lo imposta a 9 \(per un totale di 10 elementi\).  
  
     [!code-vb[VbVbalrDataTypes#7](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-define-a-class-that-can-provide-identical-functionality_1.vb)]  
  
     È possibile dichiarare una classe da `simpleList` per contenere un elenco di valori `Integer`, un'altra classe per contenere un elenco di valori `String` e un'altra per contenere valori `Date`. Ad eccezione del tipo di dati dei membri dell'elenco, gli oggetti creati da tutte queste classi si comportano in maniera identica.  
  
     L'argomento di tipo fornito dal codice a `itemType` può essere di tipo intrinseco come `Boolean` o `Double`, una struttura, un'enumerazione o qualsiasi tipo di classe, compresa una di quelle definite dall'applicazione.  
  
     È possibile verificare la classe `simpleList` con il codice seguente.  
  
     [!code-vb[VbVbalrDataTypes#8](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-define-a-class-that-can-provide-identical-functionality_2.vb)]  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md)   
 [Of](../../../../visual-basic/language-reference/statements/of-clause.md)   
 [Type List](../../../../visual-basic/language-reference/statements/type-list.md)   
 [Procedura: utilizzare una classe generica](../../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)