---
title: "Istruzione Dim (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Dim"
  - "Dim"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Parola chiave Public, in istruzione Dim"
  - "Dim (istruzione)"
  - "stringhe di lunghezza fissa, dichiarazione"
  - "variabili [Visual Basic], dichiarazione"
  - "WithEvents (parola chiave), Dim (istruzione)"
  - "matrici dinamiche, Dim (istruzione)"
  - "inizializzazione di variabili [Visual Basic]"
  - "{} parentesi graffe"
  - "campi, come variabili membro"
  - "dichiarazioni, matrici dinamiche"
  - "variabili membro"
  - "valori predefiniti"
  - "l'assegnazione di un tipi di dati [Visual Basic]"
  - "parentesi graffe {}"
  - "Come parola chiave, in istruzione Dim"
  - "dichiarazione di matrici [Visual Basic]"
  - "Nuova parola chiave Dim (istruzione)"
  - "Parola chiave, in istruzione Dim"
  - "archiviazione, allocazione"
  - "variabili locali"
  - "istruzioni di dichiarazione"
  - "Dim (istruzione), sintassi"
  - "variabili [Visual Basic], membro e locale"
ms.assetid: fae3eca1-f0b2-4400-994b-7aa58a848448
caps.latest.revision: 72
caps.handback.revision: 72
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Istruzione Dim (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara e alloca spazio di archiviazione per una o più variabili.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [[ Shared ] [ Shadows ] | [ Static ]] [ ReadOnly ]   
Dim [ WithEvents ] variablelist  
```  
  
## <a name="parts"></a>Parti  
  
-   `attributelist`  
  
     Facoltativo. Vedere [elenco attributi](../../../visual-basic/language-reference/statements/attribute-list.md).  
  
-   `accessmodifier`  
  
     Facoltativo. Può essere uno dei seguenti:  
  
    -   [Pubblica](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protetto](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Privato](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
-   `Shared`  
  
     Facoltativo. Vedere [condivisi](../../../visual-basic/language-reference/modifiers/shared.md).  
  
-   `Shadows`  
  
     Facoltativo. Vedere [ombreggiature](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
-   `Static`  
  
     Facoltativo. Vedere [statico](../../../visual-basic/language-reference/modifiers/static.md).  
  
-   `ReadOnly`  
  
     Facoltativo. Vedere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
-   `WithEvents`  
  
     Facoltativo. Specifica che si tratta di variabili oggetto che fa riferimento a istanze di una classe che può generare eventi. Vedere [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md).  
  
-   `variablelist`  
  
     Obbligatorio. Elenco di variabili dichiarate in questa istruzione.  
  
     `variable [ , variable ... ]`  
  
     Ogni `variable` presenta la sintassi e le parti seguenti:  
  
     `variablename [ ( [ boundslist ] ) ] [ As [ New ] datatype [ With`{`[ .propertyname = propinitializer [ , ... ] ] } ] ] [ = initializer ]`  
  
    |||  
    |-|-|  
    |Parte|Descrizione|  
    |`variablename`|Obbligatorio. Nome della variabile. Vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
    |`boundslist`|Facoltativo. Elenco dei limiti di ogni dimensione di una variabile di matrice.|  
    |`New`|Facoltativo. Crea una nuova istanza della classe quando il `Dim` istruzione viene eseguita.|  
    |`datatype`|Facoltativo. Tipo di dati della variabile.|  
    |`With`|Facoltativo. Introduce l'elenco di inizializzatori di oggetto.|  
    |`propertyname`|Facoltativo. Il nome di una proprietà nella classe crei un'istanza di.|  
    |`propinitializer`|Necessari dopo `propertyname` =. L'espressione viene valutata e assegnata al nome della proprietà.|  
    |`initializer`|Facoltativo se `New` non è specificato. Espressione che viene valutata e assegnata alla variabile quando viene creato.|  
  
## <a name="remarks"></a>Note  
 Il compilatore Visual Basic utilizza il `Dim` istruzione per determinare il tipo di dati della variabile e altre informazioni, ad esempio il codice può accedere alla variabile. Nell'esempio seguente viene dichiarata una variabile che contiene un `Integer` valore.  
  
```vb  
Dim numberOfStudents As Integer  
```  
  
 È possibile specificare qualsiasi tipo di dati o il nome di un'enumerazione, struttura, classe o interfaccia.  
  
```vb  
Dim finished As Boolean  
Dim monitorBox As System.Windows.Forms.Form  
```  
  
 Per un tipo di riferimento, utilizzare il `New` (parola chiave) per creare una nuova istanza della classe o una struttura che viene specificato dal tipo di dati. Se si utilizza `New`, non si utilizza un'espressione di inizializzazione. Invece fornire gli argomenti, se sono necessarie, al costruttore della classe da cui si sta creando la variabile.  
  
```vb  
Dim bottomLabel As New System.Windows.Forms.Label  
```  
  
 È possibile dichiarare una variabile in una routine, blocco, classe, struttura o un modulo. È possibile dichiarare una variabile in un file di origine, lo spazio dei nomi o interfaccia. Per ulteriori informazioni, vedere [contesti delle dichiarazioni e livelli di accesso predefinito](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Una variabile viene dichiarata a livello di modulo, all'esterno di qualsiasi routine, è un *variabile membro* o *campo*. Variabili membro rientrano nell'ambito in tutta la classe, struttura o un modulo. Una variabile dichiarata a livello di routine è una *variabile locale*. Le variabili locali sono nell'ambito solo all'interno della routine o blocco.  
  
 I seguenti modificatori di accesso vengono utilizzati per dichiarare le variabili all'esterno di una routine: `Public`, `Protected`, `Friend`, `Protected Friend`, e `Private`. Per ulteriori informazioni, vedere [livelli di accesso in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Il `Dim` parola chiave è facoltativa e in genere omesso se si specifica uno dei seguenti modificatori: `Public`, `Protected`, `Friend`, `Protected Friend`, `Private`, `Shared`, `Shadows`, `Static`, `ReadOnly`, o `WithEvents`.  
  
```vb  
Public maximumAllowed As Double  
Protected Friend currentUserName As String  
Private salary As Decimal  
Static runningTotal As Integer  
```  
  
 Se `Option Explicit` è abilitato (impostazione predefinita), il compilatore richiede una dichiarazione per tutte le variabili utilizzate. Per ulteriori informazioni, vedere [istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md).  
  
## <a name="specifying-an-initial-value"></a>Specificare un valore iniziale  
 È possibile assegnare un valore a una variabile quando viene creato. Per un tipo di valore, utilizzare un *inizializzatore* per fornire un'espressione da assegnare alla variabile. L'espressione deve restituire una costante che può essere calcolato in fase di compilazione.  
  
```vb  
Dim quantity As Integer = 10  
Dim message As String = "Just started"  
```  
  
 Se viene specificato un inizializzatore e non viene specificato un tipo di dati un `As` clausola *inferenza del tipo* viene utilizzato per dedurre il tipo di dati dall'inizializzatore. Nell'esempio seguente, entrambi `num1` e `num2` sono fortemente tipizzati come integer. Nella seconda dichiarazione, l'inferenza del tipo deduce il tipo dal valore 3.  
  
```vb  
' Use explicit typing.  
Dim num1 As Integer = 3  
  
' Use local type inference.  
Dim num2 = 3  
```  
  
 L'inferenza del tipo si applica a livello di routine. Non è applicabile all'esterno di una routine in una classe, struttura, modulo o interfaccia. Per ulteriori informazioni sull'inferenza del tipo, vedere [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md) e [l'inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
 Per informazioni su ciò che accade quando un tipo di dati o un inizializzatore non è specificato, vedere [tipi di dati predefiniti e i valori](../../../visual-basic/language-reference/statements/dim-statement.md#default) più avanti in questo argomento.  
  
 È possibile utilizzare un *inizializzatore dell'oggetto* per dichiarare le istanze di tipi denominati e anonimi. Il codice seguente crea un'istanza di un `Student` classe e utilizza un inizializzatore di oggetto per inizializzare le proprietà.  
  
```vb  
Dim student1 As New Student With {.First = "Michael",   
                                  .Last = "Tucker"}  
```  
  
 Per ulteriori informazioni sugli inizializzatori di oggetto, vedere [procedura: dichiarare un oggetto utilizzando un inizializzatore di oggetto](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md), [gli inizializzatori di oggetto: tipi denominati e anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md), e [tipi anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
## <a name="declaring-multiple-variables"></a>Dichiarare più variabili  
 È possibile dichiarare più variabili in un'istruzione di dichiarazione, specificando il nome della variabile per ognuno di essi e dopo ogni nome di matrice con le parentesi. Nel caso di più variabili, è possibile separarle mediante virgole.  
  
```vb  
Dim lastTime, nextTime, allTimes() As Date  
```  
  
 Se si dichiarano più variabili con uno `As` clausola, non è possibile specificare un inizializzatore per il gruppo di variabili.  
  
 È possibile specificare tipi di dati diversi per diverse variabili utilizzando un oggetto separato `As` clausola per ogni variabile è dichiarata. Ogni variabile accetta il tipo di dati specificato nel primo `As` clausola verificato dopo la `variablename` parte.  
  
```vb  
Dim a, b, c As Single, x, y As Double, i As Integer  
' a, b, and c are all Single; x and y are both Double  
```  
  
## <a name="arrays"></a>Matrici  
 È possibile dichiarare una variabile per contenere un *matrice*, che può contenere più valori. Per specificare che una variabile contiene una matrice, seguire la `variablename` immediatamente con le parentesi. Per ulteriori informazioni sulle matrici, vedere [matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
 È possibile specificare il limite inferiore e superiore di ogni dimensione della matrice. A tale scopo, includere un `boundslist` all'interno delle parentesi. Per ogni dimensione, il `boundslist` Specifica il limite superiore e facoltativamente il limite inferiore. Il limite inferiore è sempre zero, se si specifichi o meno. Ogni indice può variare da zero al valore limite superiore.  
  
 Le due istruzioni seguenti sono equivalenti. Ogni istruzione dichiara una matrice di 21 `Integer` elementi. Quando si accede a matrice, l'indice può variare da 0 a 20.  
  
```vb  
Dim totals(20) As Integer  
Dim totals(0 To 20) As Integer  
```  
  
 L'istruzione seguente dichiara una matrice bidimensionale di tipo `Double`. La matrice è 4 righe (3 + 1) di 6 colonne (5 + 1) ogni. Si noti che il limite superiore rappresenta il valore massimo possibile per l'indice, non la lunghezza della dimensione. La lunghezza della dimensione è il limite superiore più uno.  
  
```vb  
Dim matrix2(3, 5) As Double  
```  
  
 Una matrice può avere da 1 a 32 dimensioni.  
  
 È possibile lasciare vuoto in una dichiarazione di matrice tutti i limiti. In questo caso, la matrice disponga del numero di dimensioni specificato, ma è non inizializzato. Ha un valore di `Nothing` fino a quando non si inizializza almeno alcuni dei suoi elementi. Il `Dim` istruzione deve specificare limiti per tutte le dimensioni o senza quote.  
  
```vb  
' Declare an array with blank array bounds.  
Dim messages() As String  
' Initialize the array.  
ReDim messages(4)  
```  
  
 Se la matrice contiene più di una dimensione, è necessario includere una virgola tra le parentesi per indicare il numero di dimensioni.  
  
```vb  
Dim oneDimension(), twoDimensions(,), threeDimensions(,,) As Byte  
```  
  
 È possibile dichiarare un *matrice di lunghezza zero* dichiarando una delle dimensioni della matrice come -1. Il valore di una variabile che contiene una matrice a lunghezza zero è `Nothing`. Matrici di lunghezza zero sono necessari per alcune funzioni di common language runtime. Se si tenta di accedere a una matrice di questo tipo, si verifica un'eccezione di runtime. Per ulteriori informazioni, vedere [matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
 È possibile inizializzare i valori di una matrice con un valore letterale della matrice. A tale scopo, racchiudere i valori di inizializzazione con parentesi graffe (`{}`).  
  
```vb  
Dim longArray() As Long = {0, 1, 2, 3}  
```  
  
 Per le matrici multidimensionali, l'inizializzazione di ciascuna dimensione separata è racchiusa tra parentesi graffe nella dimensione esterna. Gli elementi vengono specificati in ordine crescente di riga.  
  
```vb  
Dim twoDimensions(,) As Integer = {{0, 1, 2}, {10, 11, 12}}  
```  
  
 Per ulteriori informazioni sui valori letterali di matrici, vedere [matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
##  <a name="a-namedefaulta-default-data-types-and-values"></a><a name="default"></a> Tipi di dati predefiniti e valori  
 Nella tabella seguente vengono descritti i risultati di varie combinazioni della specifica del tipo di dati e dell'inizializzatore in un'istruzione `Dim`.  
  
|||||  
|-|-|-|-|  
|Tipo di dati specificato?|Inizializzatore specificato?|Esempio|Risultato|  
|No|No|`Dim qty`|Se [Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md) è disabilitato (impostazione predefinita), la variabile è impostata su `Nothing`.<br /><br /> Se `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|No|Sì|`Dim qty = 5`|Se [Option Infer](../../../visual-basic/language-reference/statements/option-infer-statement.md) è abilitato (impostazione predefinita), tipo di variabile viene assegnato il tipo di dati dell'inizializzatore. Vedere [inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Se le istruzioni `Option Infer` e `Option Strict` sono disabilitate, il tipo di dati accettato dalla variabile è `Object`.<br /><br /> Se `Option Infer` è disabilitato e `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|Sì|No|`Dim qty As Integer`|La variabile viene inizializzata sul valore predefinito per il tipo di dati. Vedere la tabella più avanti in questa sezione.|  
|Sì|Sì|`Dim qty  As Integer = 5`|Se il tipo di dati dell'inizializzatore non è convertibile nel tipo di dati specificato, si verifica un errore in fase di compilazione.|  
  
 Se si specifica un tipo di dati ma non si specifica un inizializzatore, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Inizializza la variabile sul valore predefinito per il tipo di dati. Nella tabella seguente viene illustrata l'impostazione predefinita i valori di inizializzazione.  
  
|||  
|-|-|  
|Tipo di dati|Valore predefinito|  
|Tutti i tipi numerici (inclusi `Byte` e `SByte`)|0|  
|`Char`|0 binario|  
|I tipi di riferimento (inclusi `Object`, `String`, e tutte le matrici)|`Nothing`|  
|`Boolean`|`False`|  
|`Date`|12:00 AM del 1 ° gennaio dell'anno 1 (01/01/0001 12:00:00 AM)|  
  
 Ogni elemento di una struttura viene inizializzato come se fosse una variabile separata. Se si dichiara la lunghezza di una matrice, ma non si inizializza gli elementi, ogni elemento viene inizializzato come se fosse una variabile separata.  
  
## <a name="static-local-variable-lifetime"></a>Durata della variabile locale statica  
 Oggetto `Static` variabile locale ha una durata maggiore rispetto a quella della routine in cui è dichiarata. La durata della variabile dipende in cui viene dichiarata la routine e se è `Shared`.  
  
||||  
|-|-|-|  
|Dichiarazione di routine|Variabile di inizializzazione|Variabile arresta esistente|  
|In un modulo|La prima volta che viene chiamata la routine|Arresto dell'esecuzione del programma|  
|In una classe o struttura, è procedura `Shared`|La prima volta la procedura viene chiamata su un'istanza specifica o nella classe o struttura stessa|Arresto dell'esecuzione del programma|  
|In una classe o struttura, non è più routine `Shared`|La prima volta che viene chiamata la routine in un'istanza specifica|Quando l'istanza viene rilasciata per la garbage collection (GC)|  
  
## <a name="attributes-and-modifiers"></a>Gli attributi e modificatori  
 È possibile applicare attributi solo alle variabili membro e non alle variabili locali. Un attributo fornisce informazioni per i metadati dell'assembly, che non è significativo per l'archiviazione temporanea, ad esempio le variabili locali.  
  
 A livello di modulo, è possibile utilizzare il `Static` modificatore per dichiarare le variabili membro. A livello di routine, non è possibile utilizzare `Shared`, `Shadows`, `ReadOnly`, `WithEvents`, o qualsiasi modificatori di accesso per dichiarare le variabili locali.  
  
 È possibile specificare il codice può accedere a una variabile fornendo un `accessmodifier`. Classe e il modulo predefinito di variabili (all'esterno di qualsiasi routine) membro per l'accesso privato e predefinito di variabili membro di struttura per l'accesso pubblico. È possibile regolare i livelli di accesso con i modificatori di accesso. È possibile utilizzare i modificatori di accesso con le variabili locali (all'interno di una procedura).  
  
 È possibile specificare `WithEvents` solo le variabili membro e non le variabili locali all'interno di una routine. Se si specifica `WithEvents`, il tipo di dati della variabile deve essere un tipo di classe specifico, non `Object`. Non è possibile dichiarare una matrice con `WithEvents`. Per ulteriori informazioni sugli eventi, vedere [eventi](../../../visual-basic/programming-guide/language-features/events/events.md).  
  
> [!NOTE]
>  Codice esterno di una classe, struttura o un modulo necessario qualificare il nome di una variabile membro con il nome di tale classe, struttura o un modulo. All'esterno di che una routine o un blocco non può fare riferimento a variabili locali all'interno di tale routine o blocco di codice.  
  
## <a name="releasing-managed-resources"></a>Rilasciare le risorse gestite  
 Il garbage collector di .NET Framework elimina le risorse gestite senza alcuna codifica aggiuntiva da parte dell'utente. Tuttavia, è possibile forzare l'eliminazione di una risorsa gestita anziché attendere che il garbage collector.  
  
 Se una classe mantiene una risorsa particolarmente preziosa e rara (ad esempio un handle di connessione o file di database), è possibile evitare di attendere la successiva operazione di garbage collection per pulire un'istanza della classe che non è più in uso. Una classe può implementare il <xref:System.IDisposable> interfaccia per fornire un modo per rilasciare le risorse prima di una garbage collection. Una classe che implementa l'interfaccia espone un `Dispose` metodo che può essere chiamato per forzare il rilascio immediato delle risorse preziose.  
  
 Il `Using` istruzione automatizza il processo di acquisizione di una risorsa, l'esecuzione di un set di istruzioni e quindi l'eliminazione della risorsa. Tuttavia, è necessario che la risorsa di <xref:System.IDisposable> interfaccia. Per ulteriori informazioni, vedere [istruzione Using](../../../visual-basic/language-reference/statements/using-statement.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente dichiara variabili utilizzando il `Dim` istruzione con varie opzioni.  
  
 [!code-vb[VbVbalrStatements#141](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_1.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono elencati i numeri primi compreso tra 1 e 30. Viene descritto l'ambito delle variabili locali in commenti del codice.  
  
 [!code-vb[VbVbalrStatements#142](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_2.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, il `speedValue` variabile viene dichiarata a livello di classe. Il `Private` parola chiave viene utilizzata per dichiarare la variabile. La variabile è accessibile da qualsiasi routine di `Car` (classe).  
  
 [!code-vb[VbVbalrStatements#144](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_3.vb)]  
  
 [!code-vb[VbVbalrStatements#145](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_4.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Const (istruzione)](../../../visual-basic/language-reference/statements/const-statement.md)   
 [ReDim (istruzione)](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Istruzione Option Infer](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Pagina compilazione, Progettazione progetti (Visual Basic)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)   
 [Dichiarazione di variabile](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Inizializzatori di oggetto: Tipi denominati e anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Tipi anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Inizializzatori di oggetto: Tipi denominati e anonimi](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Procedura: dichiarare un oggetto utilizzando un inizializzatore di oggetto](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)   
 [Inferenza del tipo locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)