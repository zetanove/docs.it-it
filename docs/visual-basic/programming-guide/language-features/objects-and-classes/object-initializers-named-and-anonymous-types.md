---
title: 'Inizializzatori di oggetto: Tipi di denominati e anonimi (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ObjectInitializer
dev_langs:
- VB
helpviewer_keywords:
- object initializers [Visual Basic]
- anonymous types [Visual Basic], object initializers
- initializing properties [Visual Basic]
- initializers [Visual Basic]
- named types [Visual Basic]
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
caps.latest.revision: 27
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
ms.openlocfilehash: d684ad4f3dd47dc7400ea401a94660af832ef866
ms.lasthandoff: 03/13/2017

---
# <a name="object-initializers-named-and-anonymous-types-visual-basic"></a>Inizializzatori di oggetto: tipi denominati e tipi anonimi (Visual Basic)
Gli inizializzatori di oggetto consentono di specificare le proprietà di un oggetto complesso utilizzando una singola espressione. Possono essere utilizzati per creare istanze di tipi denominati e tipi anonimi.  
  
## <a name="declarations"></a>Dichiarazioni  
 Dichiarazioni di istanze di tipi denominati e anonimi possono apparire quasi identiche, ma i relativi effetti non sono uguali. Ogni categoria dispone di funzionalità e restrizioni di propri. Nell'esempio seguente viene illustrato un modo pratico per dichiarare e inizializzare un'istanza di una classe denominata `Customer`, utilizzando un elenco di inizializzatori di oggetto. Si noti che dopo la parola chiave viene specificato il nome della classe `New`.  
  
 [!code-vb[VbVbalrObjectInit n.&1;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_1.vb)]  
  
 Un tipo anonimo dispone di un nome utilizzabile. Creazione di un'istanza di un tipo anonimo non può pertanto includere un nome di classe.  
  
 [!code-vb[VbVbalrObjectInit n.&2;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
 I requisiti e risultati delle due dichiarazioni non sono uguali. Per `namedCust`, `Customer` classe che dispone di un `Name` proprietà deve essere già esistente e la dichiarazione crea un'istanza di tale classe. Per `anonymousCust`, il compilatore definisce una nuova classe che contiene una proprietà, una stringa denominata `Name`e crea una nuova istanza della classe.  
  
## <a name="named-types"></a>Tipi denominati  
 Gli inizializzatori di oggetto forniscono un modo semplice per chiamare il costruttore di un tipo e quindi impostare i valori di alcune o tutte le proprietà in un'unica istruzione. Il compilatore richiama il costruttore appropriato per l'istruzione: il costruttore predefinito, se viene presentato alcun argomento o un costruttore con parametri se vengono inviati uno o più argomenti. Successivamente, le proprietà specificate vengono inizializzate nell'ordine in cui vengono presentati nell'elenco di inizializzatori.  
  
 Ogni inizializzazione nell'elenco di inizializzatori è costituita dall'assegnazione di un valore iniziale a un membro della classe. I nomi e tipi di dati dei membri vengono determinati quando la classe è definita. Negli esempi seguenti, il `Customer` classe deve esistere e devono avere membri denominati `Name` e `City` che possono accettare valori stringa.  
  
 [!code-vb[VbVbalrObjectInit n.&3;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_3.vb)]  
  
 In alternativa, è possibile ottenere lo stesso risultato utilizzando il codice seguente:  
  
 [!code-vb[VbVbalrObjectInit n.&4;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_4.vb)]  
  
 Ognuna di queste dichiarazioni è equivalente all'esempio seguente, che consente di creare un `Customer` oggetto utilizzando il costruttore predefinito e specifica i valori iniziali per il `Name` e `City` proprietà utilizzando un `With` istruzione.  
  
 [!code-vb[VbVbalrObjectInit n.&5;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_5.vb)]  
  
 Se il `Customer` classe contiene un costruttore con parametri che consente di inviare un valore per `Name`, ad esempio, è possibile inoltre dichiarare e inizializzare un `Customer` oggetto nei modi seguenti:  
  
 [!code-vb[6 VbVbalrObjectInit](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_6.vb)]  
  
 Non è necessario inizializzare tutte le proprietà, come illustrato nel codice seguente.  
  
 [!code-vb[VbVbalrObjectInit&#7;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_7.vb)]  
  
 Tuttavia, l'elenco di inizializzazione non può essere vuoto. Le proprietà non inizializzate mantengono i valori predefiniti.  
  
### <a name="type-inference-with-named-types"></a>Inferenza del tipo con tipi denominati  
 È possibile ridurre il codice per la dichiarazione di `cust1` combinando gli inizializzatori di oggetto e l'inferenza del tipo locale. In questo modo è possibile omettere il `As` clausola nella dichiarazione di variabile. Il tipo di dati della variabile viene dedotto dal tipo dell'oggetto creato mediante l'assegnazione. Nell'esempio seguente, il tipo di `cust6` è `Customer`.  
  
 [!code-vb[VbVbalrObjectInit n.&8;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_8.vb)]  
  
### <a name="remarks-about-named-types"></a>Note sui tipi denominati  
  
-   Impossibile inizializzare un membro della classe più volte nell'elenco di inizializzatori di oggetto. La dichiarazione di `cust7` provoca un errore.  
  
     [!code-vb[9 VbVbalrObjectInit](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_9.vb)]  
  
-   Un membro può essere utilizzato per inizializzare se stesso o un altro campo. Se si accede a un membro prima che sia stato inizializzato, come illustrato nella seguente dichiarazione per `cust8`, verrà utilizzato il valore predefinito. Tenere presente che quando viene elaborata una dichiarazione che utilizza un inizializzatore di oggetto, la prima cosa che accade se viene richiamato il costruttore appropriato. Successivamente, vengono inizializzati i singoli campi nell'elenco di inizializzatori. Negli esempi seguenti, il valore predefinito per `Name` viene assegnato per `cust8`, e viene assegnato un valore inizializzato `cust9`.  
  
     [!code-vb[VbVbalrObjectInit&#10;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_10.vb)]  
  
     Nell'esempio seguente viene utilizzato il costruttore con parametri da `cust3` e `cust4` per dichiarare e inizializzare `cust10` e `cust11`.  
  
     [!code-vb[VbVbalrObjectInit&#11;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_11.vb)]  
  
-   Gli inizializzatori di oggetto possono essere annidati. Nell'esempio seguente, `AddressClass` è una classe che dispone di due proprietà, `City` e `State`e `Customer` classe dispone di un `Address` proprietà che è un'istanza di `AddressClass`.  
  
     [!code-vb[VbVbalrObjectInit&#12;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_12.vb)]  
  
-   L'elenco di inizializzazione non può essere vuoto.  
  
-   L'istanza da inizializzare non può essere di tipo Object.  
  
-   I membri di classe in fase di inizializzazione non possono essere membri condivisi, i membri di sola lettura, costanti o chiamate al metodo.  
  
-   Membri della classe in fase di inizializzazione non possono essere indicizzati o completo. Negli esempi seguenti vengono generati errori del compilatore:  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## <a name="anonymous-types"></a>Tipi anonimi  
 Tipi anonimi utilizzano gli inizializzatori di oggetto per creare istanze di nuovi tipi che non si definisce in modo esplicito e il nome. Al contrario, il compilatore genera un tipo in base alle proprietà designate nell'elenco di inizializzatori di oggetto. Poiché il nome del tipo viene omesso, viene considerato un *tipo anonimo*. Ad esempio, confrontare la dichiarazione seguente con quella precedente per `cust6`.  
  
 [!code-vb[13 VbVbalrObjectInit](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_13.vb)]  
  
 L'unica differenza è sintatticamente che viene specificato alcun nome dopo `New` per il tipo di dati. Tuttavia, ciò che accade è piuttosto diversa. Il compilatore definisce un nuovo tipo anonimo che ha due proprietà, `Name` e `City`e crea un'istanza con i valori specificati. L'inferenza del tipo determina i tipi di `Name` e `City` nell'esempio sono stringhe.  
  
> [!CAUTION]
>  Il nome del tipo anonimo viene generato dal compilatore e può variare da una compilazione di un'. Il codice non deve utilizzare o basarsi sul nome di un tipo anonimo.  
  
 Poiché il nome del tipo non è disponibile, è possibile utilizzare un `As` clausola per dichiarare `cust13`. Il tipo deve essere dedotto. Senza utilizzare l'associazione tardiva, limita l'utilizzo di tipi anonimi alle variabili locali.  
  
 Tipi anonimi forniscono supporto critico per [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query. Per ulteriori informazioni sull'utilizzo di tipi anonimi nelle query, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) e [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  
  
### <a name="remarks-about-anonymous-types"></a>Note sui tipi anonimi  
  
-   In genere, tutte o la maggior parte delle proprietà nella dichiarazione di un tipo anonimo saranno i proprietà chiave, indicate digitando la parola chiave `Key` davanti al nome di proprietà.  
  
     [!code-vb[VbVbalrObjectInit&#14;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_14.vb)]  
  
     Per ulteriori informazioni sulle proprietà chiave, vedere [chiave](../../../../visual-basic/language-reference/modifiers/key.md).  
  
-   Come i tipi denominati, gli elenchi di inizializzatori per definizioni di tipo anonimo devono dichiarare almeno una proprietà.  
  
     [!code-vb[VbVbalrObjectInit n.&2;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_2.vb)]  
  
-   Quando viene dichiarata un'istanza di un tipo anonimo, il compilatore genera una corrispondente definizione di tipo anonimo. I nomi e tipi di dati delle proprietà provengono dalla dichiarazione dell'istanza e sono inclusi dal compilatore nella definizione. Le proprietà non sono denominate e definite in anticipo, come avviene per un tipo denominato. I tipi inferiti. Non è possibile specificare i tipi di dati delle proprietà utilizzando un `As` clausola.  
  
-   Tipi anonimi possono anche definire i nomi e valori delle relative proprietà in diversi altri modi. Ad esempio, una proprietà di tipo anonimo può richiedere il nome e il valore di una variabile o il nome e il valore di una proprietà di un altro oggetto.  
  
     [!code-vb[VbVbalrObjectInit&#15;](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/object-initializers-named-and-anonymous-types_15.vb)]  
  
     Per ulteriori informazioni sulle opzioni per la definizione delle proprietà nei tipi anonimi, vedere [procedura: dedurre i nomi delle proprietà e i tipi nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)   
 [Chiave](../../../../visual-basic/language-reference/modifiers/key.md)   
 [Procedura: Dichiarare un oggetto usando un inizializzatore di oggetto](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
