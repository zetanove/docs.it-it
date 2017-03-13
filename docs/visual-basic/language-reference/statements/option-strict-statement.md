---
title: "Option Strict Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Strict"
  - "vb.OptionStrict"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Strict keyword"
  - "Option Strict statement"
  - "conversions, implicit"
  - "late binding"
  - "implicit conversions"
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
caps.latest.revision: 49
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 49
---
# Option Strict Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Limita le conversioni dei tipi di dati implicite solo alle conversioni verso un tipo di dati più grande, impedisce l'associazione tardiva e impedisce la tipizzazione implicita risultante in un tipo `Object`.  
  
## Sintassi  
  
```  
Option Strict { On | Off }  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`On`|Parametro facoltativo.  Abilita la verifica dell'istruzione `Option Strict`.|  
|`Off`|Parametro facoltativo.  Disabilita la verifica dell'istruzione `Option Strict`.|  
  
## Note  
 Quando `Option Strict On` o `Option Strict` appaiono in un file, le condizioni riportate di seguito generano un errore in fase di compilazione:  
  
-   Conversioni di restrizione implicite  
  
-   Associazione tardiva  
  
-   Tipizzazione implicita che risulta in un tipo `Object`  
  
> [!NOTE]
>  Nelle configurazioni che è possibile impostare sul [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic), esistono tre impostazioni che corrispondono alle tre condizioni che generano un errore in fase di compilazione.  Per ulteriori informazioni sulla creazione di tali impostazioni, vedere [Per impostare le configurazioni di avvisi nell'IDE](../../../visual-basic/language-reference/statements/option-strict-statement.md#conditions) più avanti in questo argomento.  
  
 L'istruzione `Option Strict Off` disattiva il controllo degli errori e degli avvisi per tutte e tre le condizioni, anche se le impostazioni IDE associate specificano l'attivazione di tali errori o avvisi.  L'istruzione di `Option Strict On` attiva errore e avviso che viene verificata la presenza di tutte e tre le condizioni, anche se le impostazioni associate IDE specificano disattivare tali errori o avvisi.  
  
 Se utilizzato, è necessario includere l'istruzione `Option Strict` in un file prima di tutte le altre istruzioni del codice.  
  
 Quando si `Option Strict` impostato su `On`, controlli di Visual Basic che i tipi di dati specificati per tutti gli elementi di programmazione.  I tipi di dati possono essere specificati in modo esplicito, o essere specificati utilizzando l'inferenza del tipo di variabile locale.  Specificando i tipi di dati per tutti gli elementi di programmazione è consigliabile, per i motivi seguenti:  
  
-   Attiva il supporto IntelliSense per le variabili e i parametri,  Ciò consente di visualizzarne le proprietà e gli altri membri mentre si digita il codice.  
  
-   Consente al compilatore di eseguire la verifica dei tipi.  Il controllo dei tipi consente di trovare istruzioni che possono non riuscire in fase di esecuzione a causa di errori di conversione del tipo.  Vengono inoltre identificate le chiamate a metodi su oggetti che non li supportano.  
  
-   Accelera l'esecuzione del codice.  Una ragione è che se non si specifica un tipo di dati per un elemento di programmazione, il compilatore Visual Basic di assegnare il tipo di `Object` .  Il codice compilato potrebbe essere necessario eseguire avanti e indietro tra `Object` e altri tipi di dati, con conseguente riduzione delle prestazioni.  
  
## Errori di conversione di restrizione implicita  
 Gli errori di conversione di restrizione implicita si verificano quando esiste una conversione di tipo di dati implicita che è una conversione di restrizione.  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente di convertire molti tipi di dati in altri tipi di dati.  Se tuttavia un valore viene convertito da un tipo di dati a un altro caratterizzato da un livello di precisione o da una capacità inferiore, possono verificarsi perdite di dati.  Se la conversione verso un tipo di dati più piccolo non riesce, si verifica un errore di runtime.  Durante la compilazione, con l'istruzione `Option Strict` le conversioni di restrizione vengono notificate in modo che possano essere evitate.  Per ulteriori informazioni, vedere [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md) e [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
 Le conversioni che possono causare errori includono le conversioni implicite che si verificano nelle espressioni.  Per ulteriori informazioni, vedere i seguenti argomenti:  
  
-   [\+ Operator](../../../visual-basic/language-reference/operators/addition-operator.md)  
  
-   [\+\= Operator](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)  
  
-   [\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md)  
  
-   [\/\= Operator](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)  
  
-   [Char Data Type](../../../visual-basic/language-reference/data-types/char-data-type.md)  
  
 Quando si concatenano le stringhe mediante [& Operator](../../../visual-basic/language-reference/operators/concatenation-operator.md), tutte le conversioni alle stringhe sono considerate conversioni verso un tipo di dati più grande.  Tali conversioni pertanto non generano un errore di conversione implicito verso un tipo di dati più piccolo, anche se `Option Strict` è attivato.  
  
 Quando si chiama un metodo con un argomento che dispone di un tipo di dati diverso dal parametro corrispondente, una conversione verso un tipo di dati più piccolo causa un errore in fase di compilazione se `Option Strict` è attivata.  È possibile evitare questo errore in fase di compilazione utilizzando una conversione verso un tipo di dati più grande o una conversione esplicita.  
  
 Gli errori di conversione di restrizione implicita vengono eliminati durante la compilazione per le conversioni dagli elementi di una raccolta `For Each…Next` alla variabile di controllo del ciclo.  Questo accade anche se `Option Strict` è attivata.  Per ulteriori informazioni, vedere la sezione "Conversioni verso tipi di dati più piccoli" di [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
## Errori associazione tardiva  
 Oggetto è associato tardivamente quando è assegnato a una proprietà o a un metodo di una variabile dichiarata di tipo `Object`.  Per ulteriori informazioni, vedere [Early and Late Binding](../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md).  
  
## Errori del tipo di oggetti impliciti  
 Gli errori del tipo di oggetti impliciti si verificano quando non può essere derivato un tipo appropriato per una variabile dichiarata, in modo da derivare un tipo di `Object`.  Ciò principalmente si verifica quando si utilizza un'istruzione `Dim` per dichiarare una variabile senza utilizzare una clausola `As` e `Option Infer` non è attivo.  Per ulteriori informazioni, vedere [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md) e [Visual Basic Language Specification](../../../visual-basic/reference/language-specification.md).  
  
 Per i parametri del metodo, la clausola `As` è facoltativa se `Option Strict` è disattivata.  Se, tuttavia, un parametro utilizza una clausola `As`, dovranno utilizzarla tutti i parametri.  Se `Option Strict` è abilitata, la clausola `As` è obbligatoria per ogni definizione di parametro.  
  
 Se si dichiara una variabile senza utilizzare una clausola `As` e la si imposta su `Nothing`, la variabile dispone di un tipo di `Object`.  Non si verifica nessun errore in fase di compilazione in questo caso, quando `Option Strict` è attivato e anche `Option Infer`.  Un esempio è `Dim something = Nothing`.  
  
### Tipi di dati e valori predefiniti  
 Nella tabella seguente vengono descritti i risultati di varie combinazioni della specifica del tipo di dati e dell'inizializzatore in un'istruzione [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md).  
  
|||||  
|-|-|-|-|  
|Tipo di dati specificato?|Inizializzatore specificato?|Esempio|Risultato|  
|No|No|`Dim qty`|Se `Option Strict` è disabilitato \(impostazione predefinita\), la variabile è impostata su `Nothing`.<br /><br /> Se `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|No|Sì|`Dim qty = 5`|Se `Option Infer` è abilitato \(impostazione predefinita\), alla variabile viene assegnato il tipo di dati dell'inizializzatore.  Vedere [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Se le istruzioni `Option Infer` e `Option Strict` sono disabilitate, il tipo di dati accettato dalla variabile è `Object`.<br /><br /> Se `Option Infer` è disabilitato e `Option Strict` è abilitato, si verifica un errore in fase di compilazione.|  
|Sì|No|`Dim qty As Integer`|La variabile viene inizializzata sul valore predefinito per il tipo di dati.  Per ulteriori informazioni, vedere [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md).|  
|Sì|Sì|`Dim qty  As Integer = 5`|Se il tipo di dati dell'inizializzatore non è convertibile nel tipo di dati specificato, si verifica un errore in fase di compilazione.|  
  
## Quando non è presente un'istruzione Option Strict  
 Se nel codice sorgente non è presente un'istruzione `Option Strict`, si utilizza l'impostazione **Option strict** disponibile in [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  La pagina **Compila** ha impostazioni che forniscono il controllo aggiuntivo sulle condizioni che generano un errore.  
  
 Se la compilazione viene eseguita tramite il compilatore della riga di comando, è possibile utilizzare l'opzione del compilatore [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md) per specificare un'impostazione per `Option Strict`.  
  
### Per impostare Option Strict nell'IDE  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Nella scheda **Compila**, impostare il valore nella casella **Option Strict**.  
  
###  <a name="conditions"></a> Per impostare le configurazioni di avvisi nell'IDE  
 Quando si utilizza [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic) anziché un istruzione di `Option Strict`, si dispone di un'ulteriore controllo sulle condizioni che generano errori.  La sezione **Configurazioni avvisi** della pagina **Compilazione** ha impostazioni che corrispondono alle tre condizioni che generano un errore in fase di compilazione quando `Option Strict` è attivata.  Di seguito sono riportate queste impostazioni:  
  
-   **Conversione implicita**  
  
-   **Associazione tardiva; la chiamata potrebbe avere esito negativo in fase di esecuzione**  
  
-   **Tipo implicito: presunto oggetto**  
  
 Quando si imposta **Option Strict** su **On**, le tre impostazioni di configurazione di avviso vengono impostate su **Error**.  Quando si imposta **Option Strict** su **Off**, tutte e tre le impostazioni vengono impostate su **None**.  
  
 È possibile modificare singolarmente ogni impostazione di configurazione dell'avviso su **None**, **Warning**, o **Error**.  Se tutte e tre le impostazioni di configurazione di avviso sono impostate su **Errore**, `On` verrà visualizzato nella casella `Option strict`.  Se tutti e tre sono impostati su **Nessuno**, `Off` sarà visualizzato in questa casella.  Per qualsiasi altra combinazione di queste impostazioni, **\(custom\)** è visualizzata.  
  
### Per impostare il valore predefinito di Option Strict per nuovi progetti  
 Quando si crea un progetto, l'impostazione **Option Strict** nella scheda **Compila** viene impostata con il valore dell'impostazione **Option Strict** della finestra di dialogo **Opzioni**.  
  
 Per impostare `Option Strict` in questa finestra di dialogo dal menu **Strumenti**, scegliere **Opzioni**.  Nella finestra di dialogo **Opzioni** espandere **Progetti e soluzioni**, quindi fare clic su **Impostazioni predefinite di Visual Basic**.  L'impostazione predefinita iniziale in **Impostazioni predefinite di Visual Basic** è `Off`.  
  
### Per impostare l'istruzione Option Strict nella riga di comando  
 Includere l'opzione del compilatore [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md) nel comando **vbc**.  
  
## Esempio  
 Negli esempi seguenti vengono illustrati gli errori in fase di compilazione causati dalle conversioni dei tipi impliciti che sono conversioni verso un tipo di dati più piccolo.  Questa categoria di errore corrisponde alla condizione di **Conversione implicita** nella pagina **Compilazione**.  
  
 [!code-vb[VbVbalrStatements#161](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_1.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato un errore in fase di compilazione causato dall'associazione tardiva.  Questa categoria di errore corrisponde alla condizione di **Associazione tardiva. La chiamata potrebbe non riuscire in fase di esecuzione.** nella pagina **Compilazione**.  
  
 [!code-vb[VbVbalrStatements#162](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_2.vb)]  
  
## Esempio  
 Negli esempi seguenti vengono illustrati gli errori causati dalle variabili che vengono dichiarate con un tipo implicito di `Object`.  Questa categoria di errore corrisponde alla condizione di **Tipo implicito: presunto oggetto** nella pagina **Compilazione**.  
  
 [!code-vb[VbVbalrStatements#163](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_3.vb)]  
  
 [!code-vb[VbVbalrStatements#164](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_4.vb)]  
  
## Vedere anche  
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)   
 [Option Explicit Statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [How to: Access Members of an Object](../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [Embedded Expressions in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Associazione tardiva nelle soluzioni Office](/office-dev/office-dev/late-binding-in-office-solutions)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)