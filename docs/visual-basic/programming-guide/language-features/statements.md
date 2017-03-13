---
title: "Statements in Visual Basic | Microsoft Docs"
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
  - "variables [Visual Basic], declaring"
  - "colons (:)"
  - "constants, defining"
  - "underlines"
  - "constants, statements"
  - "blue underline"
  - "procedures, statements"
  - "variables [Visual Basic], assigning"
  - "line breaks, in code"
  - "executable statements"
  - "variables [Visual Basic], defining"
  - "statements [Visual Basic], about statements"
ms.assetid: fcfdee1a-82b7-4846-98f7-9ca3f5160089
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# Statements in Visual Basic
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le istruzioni in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono istruzioni complete che  possono contenere parole chiave, operatori, variabili, costanti ed espressioni.  Ogni istruzione appartiene a una delle categorie seguenti:  
  
-   **Istruzioni di dichiarazione**, che consentono di assegnare un nome a variabili, costanti o routine e possono specificare anche un tipo di dati.  
  
-   **Istruzioni eseguibili**, che consentono di avviare azioni  e di chiamare un metodo o una funzione, scorrere in ciclo blocchi di codice o creare rami tra di essi.  Sono istruzioni eseguibili anche le **Istruzioni di assegnazione**, che consentono di assegnare un valore o un'espressione a una variabile o costante.  
  
 In questo argomento viene descritta ogni categoria.  Viene inoltre descritto come combinare più istruzioni su una singola riga e come continuare un'istruzione su più righe.  
  
## Istruzioni di dichiarazione  
 Le istruzioni di dichiarazione consentono di denominare e definire routine, variabili, proprietà, matrici e costanti.  Quando si dichiara un elemento di programmazione, è anche possibile definirne il tipo di dati, il livello di accesso e l'ambito.  Per ulteriori informazioni, vedere [Declared Element Characteristics](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md).  
  
 L'esempio seguente contiene tre dichiarazioni.  
  
 [!code-vb[VbVbalrStatements#80](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_1.vb)]  
  
 La prima dichiarazione è l'istruzione `Sub`.  Insieme alla sua istruzione corrispondente `End Sub`, dichiara una routine denominata `applyFormat`.  Essa specifica inoltre che la routine `applyFormat` è di tipo `Public` e di conseguenza qualsiasi codice possa farvi riferimento può chiamarla.  
  
 La seconda dichiarazione è l'istruzione `Const` che dichiara la costante `limit`, specificando il tipo di dati `Integer` e un valore pari a 33.  
  
 La terza dichiarazione è l'istruzione `Dim` che dichiara la variabile `thisWidget`.  Il tipo di dati è un oggetto specifico, in particolare un oggetto creato dalla classe `Widget`.  È possibile dichiarare come variabile qualsiasi tipo di dati elementari o qualsiasi tipo di oggetto esposto nell'applicazione in uso.  
  
### Valori iniziali  
 Quando viene eseguito il codice che contiene un'istruzione di dichiarazione, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] riserva la memoria necessaria per l'elemento dichiarato.  Se l'elemento contiene un valore, viene inizializzato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] in base al valore predefinito per il relativo tipo di dati.  Per ulteriori informazioni, vedere la sezione "Comportamento" in [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md).  
  
 È possibile assegnare un valore iniziale a una variabile come parte della sua dichiarazione, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrStatements#81](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_2.vb)]  
  
 Se la variabile è una variabile oggetto, è possibile creare in modo esplicito un'istanza della classe di appartenenza durante la dichiarazione utilizzando la parola chiave [New Operator](../../../visual-basic/language-reference/operators/new-operator.md), come illustrato di seguito:  
  
 [!code-vb[VbVbalrStatements#82](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_3.vb)]  
  
 Tenere presente che il valore iniziale specificato in un'istruzione di dichiarazione non viene assegnato alla variabile finché l'esecuzione non raggiunge la relativa istruzione di dichiarazione.  Fino ad allora, la variabile contiene il valore predefinito per il suo tipo di dati.  
  
## Istruzioni eseguibili  
 Un'istruzione eseguibile esegue un'azione.  Può chiamare una procedura, creare un ramo in un altro punto del codice, far scorrere in ciclo diverse istruzioni o valutare un'espressione.  Un'istruzione di assegnazione è un caso speciale di un'istruzione eseguibile.  
  
 L'esempio illustrato di seguito utilizza una `If...Then...Else` struttura di controllo per eseguire blocchi di codice diversi basati sul valore di una variabile.  Dentro ogni blocco di codice, un ciclo `For...Next` viene eseguito un numero di volte specificato.  
  
 [!code-vb[VbVbalrStatements#83](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_4.vb)]  
  
 L'istruzione `If` nell'esempio precedente verifica il valore del parametro `clockwise`.  Se il valore è `True`, chiama il metodo `spinClockwise` di `aWidget`.  Se il valore è `False`, chiama il metodo `spinCounterClockwise` di `aWidget`.  La struttura di controllo `If...Then...Else` termina con `End If`.  
  
 Il ciclo `For...Next` dentro ogni blocco chiama il metodo appropriato un numero di volte uguale al valore del parametro `revolutions`.  
  
## Istruzioni di assegnazione  
 Le istruzioni di assegnazione consentono di eseguire operazioni di assegnazione, ovvero di ottenere il valore alla destra dell'operatore di assegnazione \(`=`\) e di archiviarlo nell'elemento a sinistra, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrStatements#73](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_5.vb)]  
  
 Nel precedente esempio l'istruzione di assegnazione viene utilizzata per archiviare il valore letterale 42 nella variabile `v`.  
  
### Elementi di programmazione idonei  
 L'elemento di programmazione a sinistra dell'operatore di assegnazione deve essere in grado di accettare e archiviare un valore,  vale a dire una variabile o proprietà non [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md) o un elemento di matrice.  Nel contesto di un'istruzione di assegnazione questo elemento viene a volte definito *lvalue* che sta per "valore sinistro".  
  
 Il valore a destra dell'operatore di assegnazione viene generato da un'espressione che può essere costituita da una combinazione qualsiasi di valori letterali, costanti, variabili, proprietà, elementi matrice, altre espressioni o chiamate di funzione.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrStatements#74](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_6.vb)]  
  
 Nell'esempio precedente viene aggiunto il valore contenuto nella variabile `y` al valore incluso nella variabile `z`, quindi viene aggiunto il valore restituito dalla chiamata alla funzione `findResult`.  Il valore totale dell'espressione viene quindi archiviato nella variabile `x`.  
  
### Tipi di dati nelle istruzioni di assegnazione  
 Oltre ai valori numerici, l'operatore di assegnazione può assegnare i valori `String` come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrStatements#75](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_7.vb)]  
  
 È anche possibile assegnare i valori `Boolean` mediante un valore letterale `Boolean` o un'espressione `Boolean` come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrStatements#76](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_8.vb)]  
  
 In modo simile, è possibile assegnare i valori appropriati agli elementi di programmazione del tipo di dati `Char`, `Date` oppure `Object`.  È infine possibile assegnare un'istanza oggetto a un elemento dichiarato come classe da cui viene creata l'istanza.  
  
### Istruzioni di assegnazione composta  
 Le *istruzioni di assegnazione composta* consentono di eseguire un'operazione su un'espressione prima che questa venga assegnata all'elemento di programmazione.  Nell'esempio seguente viene illustrato uno di questi operatori, `+=`, con il quale il valore della variabile alla sinistra dell'operatore viene incrementato del valore restituito dall'espressione alla destra:  
  
 [!code-vb[VbVbalrStatements#77](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_9.vb)]  
  
 Nell'esempio precedente viene aggiunto 1 al valore di `n`, quindi il nuovo valore viene archiviato in `n`.  È un'abbreviazione equivalente alla seguente istruzione:  
  
 [!code-vb[VbVbalrStatements#78](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_10.vb)]  
  
 Gli operatori di questo tipo consentono di eseguire una serie di operazioni di assegnazione composte.  Per un elenco completo e ulteriori informazioni su questi operatori, vedere [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md).  
  
 Infine, l'operatore di assegnazione di concatenazione \(`&=`\) è utile per aggiungere una stringa alla fine di stringhe già esistenti, come illustrato nell'esempio seguente:  
  
 [!code-vb[VbVbalrStatements#79](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_11.vb)]  
  
### Conversioni di tipi nelle istruzioni di assegnazione  
 A una variabile, proprietà o un elemento matrice è necessario assegnare un valore di un tipo di dati appropriato all'elemento di destinazione.  Generalmente è opportuno provare a generare un valore dello stesso tipo di dati di quello dell'elemento di destinazione.  Tuttavia, durante l'assegnazione, è possibile convertire alcuni tipi in altri tipi.  
  
 Per informazioni sulla conversione tra tipi di dati, vedere [Type Conversions in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md).  In breve, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] un valore di un determinato tipo viene automaticamente convertito in un altro in cui può ampliarsi.  Una *conversione versione un tipo di dati più grande* si verifica sempre in fase di esecuzione e non comporta la perdita di dati.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] un valore `Integer` viene ad esempio convertito in `Double` quando appropriato, in quanto `Integer` può ampliarsi nel tipo `Double`.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
 Le *conversioni verso un tipo di dati più piccolo* comportano rischi di errori in fase di esecuzione oppure di perdita di dati.  Pe eseguire una conversione verso un tipo di dati più piccolo in modo esplicito, è possibile utilizzare una funzione di conversione di tipo, oppure è possibile indicare al compilatore di eseguire tutte le conversioni in modo implicito impostando `Option Strict Off`.  Per ulteriori informazioni, vedere [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md).  
  
## Inserimento di più istruzioni su una riga  
 È possibile inserire sulla stessa riga più istruzioni, separate dal carattere due punti \(:\)`:`.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrStatements#70](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_12.vb)]  
  
 Sebbene in alcune occasioni questa forma di sintassi possa risultare comoda, rende il codice difficile da leggere e gestire.  Si raccomanda pertanto di mantenere una sola istruzione per riga.  
  
## Continuazione di un'istruzione su più righe  
 Un'istruzione generalmente rientra in una sola riga, ma in caso contrario è possibile continuarla sulla riga successiva utilizzando una sequenza di continuazione della riga, costituita da uno spazio seguito da un carattere di sottolineatura \(`_`\) a sua volta seguito da un ritorno a capo.  Nell'esempio seguente, l'istruzione eseguibile `MsgBox` continua su due righe.  
  
 [!code-vb[VbVbalrStatements#71](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_13.vb)]  
  
### Continuazione di riga implicita  
 In molti casi è possibile continuare un'istruzione sulla riga consecutiva successiva senza utilizzare il carattere di sottolineatura \(\_\).  Nella tabella seguente vengono elencati gli elementi della sintassi che consentono di continuare in modo implicito l'istruzione sulla riga di codice successiva.  
  
|||  
|-|-|  
|Elemento della sintassi|Esempio|  
|Dopo una virgola \(`,`\).|[!code-vb[VbVbalrLineContinuation#1](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_14.vb)]|  
|Dopo una parentesi aperta \(`(`\) o prima di una parentesi chiusa \(`)`\).|[!code-vb[VbVbalrLineContinuation#2](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_15.vb)]|  
|Dopo una parentesi graffa aperta \(`{`\) o prima di una parentesi graffa chiusa \(`}`\).|[!code-vb[VbVbalrLineContinuation#3](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_16.vb)]<br /><br /> Per ulteriori informazioni, vedere [Object Initializers: Named and Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md) o [Collection Initializers](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md).|  
|Dopo un'espressione incorporata aperta \(`<%=`\) o prima della chiusura di un'espressione incorporata \(`%>`\) all'interno di un valore letterale XML.|[!code-vb[VbVbalrLineContinuation#4](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_17.vb)]<br /><br /> Per ulteriori informazioni, vedere [Embedded Expressions in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).|  
|Dopo l'operatore di concatenazione \(`&`\).|[!code-vb[VbVbcnConventions#9](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_18.vb)]<br /><br /> Per ulteriori informazioni, vedere [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md).|  
|Dopo gli operatori di assegnazione \(`=`, `&=`, `:=`, `+=`, `-=`, `*=`, `/=`, `\=`, `^=`, `<<=`, `>>=`\).|[!code-vb[VbVbalrLineContinuation#5](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_19.vb)]<br /><br /> Per ulteriori informazioni, vedere [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md).|  
|Dopo gli operatori binari \(`+`, `-`, `/`, `*`, `Mod`, `<>`, `<`, `>`, `<=`, `>=`, `^`, `>>`, `<<`, `And`, `AndAlso`, `Or`, `OrElse`, `Like`, `Xor`\) all'interno di un'espressione.|[!code-vb[VbVbalrLineContinuation#7](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_20.vb)]<br /><br /> Per ulteriori informazioni, vedere [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md).|  
|Dopo gli operatori `Is` e `IsNot`.|[!code-vb[VbVbalrLineContinuation#8](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_21.vb)]<br /><br /> Per ulteriori informazioni, vedere [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md).|  
|Dopo un carattere qualificatore di membro \(`.`\) e prima del nome del membro.  È tuttavia necessario includere un carattere di continuazione di riga \(\_\) dopo un carattere qualificatore di membro quando si utilizza l'istruzione `With` o si forniscono valori nell'elenco di inizializzazione per un tipo.  Prendere in considerazione l'interruzione della riga dopo l'operatore di assegnazione \(ad esempio, `=`\) quando si utilizzano istruzioni `With` o elenchi di inizializzazione degli oggetti.|[!code-vb[VbVbalrLineContinuation#5](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_19.vb)]<br />[!code-vb[VbVbalrLineContinuation#14](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_22.vb)]<br /><br /> Per ulteriori informazioni, vedere [With...End With Statement](../../../visual-basic/language-reference/statements/with-end-with-statement.md) o [Object Initializers: Named and Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).|  
|Dopo un qualificatore della proprietà axis XML \(`.` o `.@` o `...`\).  È tuttavia necessario includere un carattere di continuazione di riga \(\_\) quando si specifica un qualificatore di membro se si utilizza la parola chiave `With`.|[!code-vb[VbVbalrLineContinuation#9](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_23.vb)]<br /><br /> Per ulteriori informazioni, vedere [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md).|  
|Dopo un segno di minore \(\<\) o prima di un segno di maggiore \(`>`\) quando si specifica un attributo.  Anche dopo un segno di maggiore \(`>`\) quando si specifica un attributo.  È tuttavia necessario includere un carattere di continuazione di riga \(\_\) quando si specificano attributi a livello di assembly o di modulo.|[!code-vb[VbVbalrLineContinuation#10](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_24.vb)]<br /><br /> Per ulteriori informazioni, vedere [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md).|  
|Prima e dopo gli operatori di query \(`Aggregate`, `Distinct`, `From`, `Group By`, `Group Join`, `Join`, `Let`, `Order By`, `Select`, `Skip`, `Skip While`, `Take`, `Take While`, `Where`, `In`, `Into`, `On`, `Ascending` e `Descending`\).  Non è possibile interrompere una riga tra le parole chiave degli operatori di query costituiti da più parole chiave \(`Order By`, `Group Join`, `Take While` e `Skip While`\).|[!code-vb[VbVbalrLineContinuation#11](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_25.vb)]<br /><br /> Per ulteriori informazioni, vedere [Queries](../../../visual-basic/language-reference/queries/queries.md).|  
|Dopo la parola chiave `In` in un'istruzione `For Each`.|[!code-vb[VbVbalrLineContinuation#12](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_26.vb)]<br /><br /> Per ulteriori informazioni, vedere [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md).|  
|Dopo la parola chiave `From` in un inizializzatore di raccolta.|[!code-vb[VbVbalrLineContinuation#13](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_27.vb)]<br /><br /> Per ulteriori informazioni, vedere [Collection Initializers](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md).|  
  
## Aggiunta di commenti  
 Il codice sorgente non sempre è di facile interpretazione, persino per il programmatore che lo ha scritto.  Per aiutare a documentare il codice, pertanto, molti programmatori utilizzano deliberatamente commenti incorporati.  I commenti incorporati nel codice possono illustrare una routine o una particolare istruzione agli utenti.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] i commenti vengono ignorati durante la compilazione e non influiscono sul codice compilato.  
  
 Le righe relative ai commenti iniziano con un apostrofo \(`'`\) o un'istruzione `REM` seguita da uno spazio.  È possibile aggiungere i commenti nella posizione desiderata all'interno del codice, eccetto che in una stringa.  Per aggiungere un commento a un'istruzione, inserire un apostrofo o `REM` dopo l'istruzione, seguito dal commento.  I commenti possono essere inseriti anche su una riga separata.  Nell'esempio che segue vengono illustrate queste possibilità.  
  
 [!code-vb[VbVbalrStatements#72](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_28.vb)]  
  
## Controllo degli errori di compilazione  
 Se, dopo aver digitato una riga di codice, essa viene visualizzata in blu con una sottolineatura ondulata, talvolta accompagnata da un messaggio di errore, nell'istruzione è presente un errore di sintassi.  È necessario individuare l'errore, scorrendo ad esempio l'elenco delle attività oppure posizionandosi su di esso con il puntatore del mouse e leggendo il testo del messaggio, e quindi correggerlo.  Il programma potrà essere compilato correttamente solo dopo che gli errori di sintassi del codice saranno stati corretti.  
  
## Sezioni correlate  
  
|||  
|-|-|  
|Termine|Definizione|  
|[Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)|Vengono forniti collegamenti alle pagine di riferimento relativi ad operatori di assegnazione quali `=`, `*=` e `&=`.|  
|[Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)|Viene illustrato come combinare elementi e operatori per produrre nuovi valori.|  
|[Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)|Viene illustrato come suddividere una singola istruzione in più righe e come inserire più istruzioni sulla stessa riga.|  
|[How to: Label Statements](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)|Viene illustrato come etichettare una riga di codice.|