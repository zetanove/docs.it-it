---
title: "Object Initializers: Named and Anonymous Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.ObjectInitializer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "object initializers [Visual Basic]"
  - "anonymous types [Visual Basic], object initializers"
  - "initializing properties [Visual Basic]"
  - "initializers [Visual Basic]"
  - "named types [Visual Basic]"
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Object Initializers: Named and Anonymous Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Gli inizializzatori di oggetto consentono di specificare le proprietà di un oggetto complesso utilizzando una sola espressione.  Possono essere utilizzati anche per creare istanze di tipi anonimi e denominati.  
  
## Dichiarazioni  
 Dichiarazioni di istanze di tipi denominati e anonimi possono apparire quasi identiche, ma gli effetti non sono uguali.  Ogni categoria ha proprie funzionalità e restrizioni.  Nell'esempio seguente viene illustrata una comoda modalità per dichiarare e inizializzare un'istanza di una classe denominata, `Customer`, utilizzando un elenco dell'inizializzatore di oggetto.  Si noti che il nome della classe viene specificato dopo la parola chiave `New`.  
  
 [!code-vb[VbVbalrObjectInit#1](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_1.vb)]  
  
 Un tipo anonimo non ha nome utilizzabile.  Pertanto una creazione di istanze di un tipo anonimo non può includere un nome della classe.  
  
 [!code-vb[VbVbalrObjectInit#2](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
 I requisiti e risultati delle due dichiarazioni non sono gli stessi.  Per `namedCust`, una classe `Customer` che ha una proprietà `Name` deve già esistere e la dichiarazione crea un'istanza di quella classe.  Per `anonymousCust`, il compilatore definisce una nuova classe che dispone di una proprietà, una stringa chiamata `Name`, crea una nuova istanza di tale classe.  
  
## Tipi denominati  
 Gli inizializzatori di oggetto forniscono una semplice modalità per chiamare il costruttore di un tipo e impostare quindi i valori di alcune o tutte le proprietà in una sola istruzione.  Il compilatore richiama il costruttore adatto per l'istruzione: il costruttore predefinito se non viene presentato alcun argomento o un costruttore con parametri se vengono inviati uno o più argomenti.  Successivamente, le proprietà specificate vengono inizializzare nell'ordine in cui vengono presentate nell'elenco di inizializzatori.  
  
 Ogni inizializzazione nell'elenco di inizializzatori è costituita dall'assegnazione di un valore iniziale a un membro della classe.  I tipi di nomi e dati dei membri vengono determinati quando la classe è definita.  Negli esempi seguenti, la classe `Customer` deve esistere e deve avere i membri denominati `Name` e `City` che possono accettare valori stringa.  
  
 [!code-vb[VbVbalrObjectInit#3](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_3.vb)]  
  
 In alternativa, è possibile ottenere lo stesso risultato utilizzando il codice seguente:  
  
 [!code-vb[VbVbalrObjectInit#4](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_4.vb)]  
  
 Ognuna di queste dichiarazioni è equivalente all'esempio seguente, che crea un oggetto `Customer` utilizzando il costruttore predefinito e quindi specifica i valori iniziali per le proprietà `Name` e `City` utilizzando un'istruzione `With`.  
  
 [!code-vb[VbVbalrObjectInit#5](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_5.vb)]  
  
 Se la classe `Customer` contiene un costruttore con parametri che consente di inviare un valore per `Name`, è anche possibile dichiarare e inizializzare un oggetto `Customer` nei seguenti modi:  
  
 [!code-vb[VbVbalrObjectInit#6](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_6.vb)]  
  
 Non è necessario inizializzare tutte le proprietà, come illustrato nel codice seguente.  
  
 [!code-vb[VbVbalrObjectInit#7](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_7.vb)]  
  
 Tuttavia, l'elenco di inizializzazione non può essere vuoto.  Le proprietà non inizializzate mantengono i valori predefiniti.  
  
### Inferenza dei tipi con tipi denominati  
 È possibile abbreviare il codice per la dichiarazione di `cust1` combinando inizializzatori di oggetto e inferenza del tipo di variabile locale.  Ciò consente di omettere la clausola `As` nella dichiarazione di variabile.  Il tipo di dati della variabile viene dedotto dal tipo dell'oggetto creato dall'assegnazione.  Nell'esempio riportato di seguito, il tipo di `cust6` è `Customer`.  
  
 [!code-vb[VbVbalrObjectInit#8](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_8.vb)]  
  
### Osservazioni sui tipi denominati  
  
-   Non è possibile inizializzare un membro della classe più di una volta nell'elenco dell'inizializzatore di oggetto.  La dichiarazione di `cust7` genera un errore.  
  
     [!code-vb[VbVbalrObjectInit#9](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_9.vb)]  
  
-   Un membro può essere utilizzato per inizializzare se stesso o un altro campo.  Se si accede a un membro prima che sia stato inizializzato, come nella seguente dichiarazione per `cust8`, verrà utilizzato il valore predefinito.  Si tenga presente che quando viene elaborata una dichiarazione che utilizza un inizializzatore di oggetto, per prima cosa viene richiamato il costruttore adatto.  Successivamente vengono inizializzati i singoli campi nell'elenco degli inizializzatori.  Nell'esempio riportato di seguito, viene assegnato a `cust8` il valore predefinito per `Name` e viene assegnato un valore inizializzato a `cust9`.  
  
     [!code-vb[VbVbalrObjectInit#10](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_10.vb)]  
  
     Nell'esempio che segue viene utilizzato il costruttore con parametri da `cust3` e `cust4` per dichiarare e inizializzare `cust10` e `cust11`.  
  
     [!code-vb[VbVbalrObjectInit#11](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_11.vb)]  
  
-   Gli inizializzatori di oggetto possono essere annidati.  Nell'esempio riportato di seguito, `AddressClass` è una classe che ha due proprietà, `City` e `State` e la classe `Customer` ha una proprietà `Address` che è un'istanza di `AddressClass`.  
  
     [!code-vb[VbVbalrObjectInit#12](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_12.vb)]  
  
-   L'elenco di inizializzazione non può essere vuoto.  
  
-   L'istanza da inizializzare non può essere di tipo Object.  
  
-   I membri di classe da inizializzare non possono essere membri condivisi, membri di sola lettura, costanti, o chiamate a un metodo.  
  
-   I membri di classe da inizializzare non possono essere indicizzati o qualificati.  Negli esempi riportati di seguito la compilazione genera degli errori.  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## Tipi anonimi  
 I tipi anonimi utilizzano inizializzatori di oggetto per creare istanze di nuovi tipi che non vengono definiti e denominati in modo esplicito.  Il compilatore genera invece un tipo in funzione delle proprietà definite nell'elenco dell'inizializzatore di oggetto.  Poiché il nome del tipo non viene specificato, viene considerato un *tipo anonimo*.  Ad esempio, confrontare la seguente dichiarazione seguente con quella precedente per `cust6`.  
  
 [!code-vb[VbVbalrObjectInit#13](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_13.vb)]  
  
 L'unica differenza di sintassi è che non viene specificato alcun nome dopo `New` per il tipo di dati.  Tuttavia, le azioni che vengono eseguite sono molto diverse.  Il compilatore definisce una nuovo tipo anonimo che ha due proprietà, `Name` e `City`, e crea un'istanza con i valori specificati.  L'inferenza dei tipi determina che i tipi di `Name` e `City` nell'esempio sono stringhe.  
  
> [!CAUTION]
>  Il nome del tipo anonimo viene generato dal compilatore e può variare da una compilazione a un'altra.  Il codice non deve utilizzare o non deve basarsi sul nome di un tipo anonimo.  
  
 Poiché il nome del tipo non è disponibile, non è possibile utilizzare una clausola `As` per dichiarare `cust13`.  Il tipo deve essere dedotto.  Se non si utilizza l'associazione tardiva, questo limita l'utilizzo di tipi anonimi alle variabili locali.  
  
 I tipi anonimi forniscono supporto critico per le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  Per ulteriori informazioni sull'utilizzo dei tipi anonimi nelle query, vedere [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) e [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  
  
### Osservazioni sui tipi anonimi  
  
-   In genere, tutte o quasi le proprietà in una dichiarazione di tipo anonimo saranno proprietà chiave, indicate digitando la parola chiave `Key` prima del nome di proprietà.  
  
     [!code-vb[VbVbalrObjectInit#14](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_14.vb)]  
  
     Per ulteriori informazioni sulle proprietà chiave, vedere [Key](../../../../visual-basic/language-reference/modifiers/key.md).  
  
-   Come i tipi denominati, gli elenchi di inizializzatori per le definizioni di tipo anonimo devono dichiarare almeno una proprietà.  
  
     [!code-vb[VbVbalrObjectInit#2](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
-   Quando viene dichiarata un'istanza di un tipo anonimo, il compilatore genera una corrispondente definizione di tipo anonimo.  I nomi e i tipi di dati delle proprietà vengono derivati dalla dichiarazione dell'istanza e sono inclusi nella definizione dal compilatore.  Le proprietà non vengono denominate e definite in anticipo, come avverrebbe per un tipo denominato.  I relativi tipi vengono dedotti.  Non è possibile specificare i tipi di dati delle proprietà utilizzando una clausola `As`.  
  
-   I tipi anonimi possono anche definire i nomi e valori delle proprietà in molte altre modalità.  Ad esempio, una proprietà del tipo anonimo può prendere sia il nome che il valore di una variabile o nome e valore di una proprietà di un altro oggetto.  
  
     [!code-vb[VbVbalrObjectInit#15](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_15.vb)]  
  
     Per ulteriori informazioni sulle opzioni per la definizione delle proprietà nei tipi anonimi, vedere [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md).  
  
## Vedere anche  
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [Key](../../../../visual-basic/language-reference/modifiers/key.md)   
 [How to: Declare an Object by Using an Object Initializer](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)