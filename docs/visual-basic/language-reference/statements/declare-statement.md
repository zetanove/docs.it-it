---
title: "Declare Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Declare"
  - "vb.Lib"
  - "vb.Any"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Lib keyword"
  - "declaring procedures, Declare statement"
  - "functions [Visual Basic], function procedures"
  - "declarations, procedures"
  - "procedures, declaration"
  - "procedures, external"
  - "Alias keyword"
  - "external references, Visual Basic"
  - "DLLs, declaring procedures"
  - "Declare statement"
  - "declarations, external"
  - "Visual Basic code, Function procedures"
  - "As keyword, in Declare statement"
  - "resources [Visual Basic], declaring"
  - "Public keyword, Declare statement"
  - "platform invoke, Visual Basic external references"
  - "Sub procedures, declarations"
  - "APIs, declaring API functions"
  - "Visual Basic code, Sub procedures"
  - "Function procedures, declaring"
ms.assetid: d3f21fb0-b804-4c99-97ed-583b23894cf1
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# Declare Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Dichiara un riferimento a una routine implementata in un file esterno.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _  
Declare [ charsetmodifier ] [ Sub ] name Lib "libname" _  
[ Alias "aliasname" ] [ ([ parameterlist ]) ]  
' -or-  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _  
Declare [ charsetmodifier ] [ Function ] name Lib "libname" _  
[ Alias "aliasname" ] [ ([ parameterlist ]) ] [ As returntype ]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attributelist`|Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).|  
|`accessmodifier`|Parametro facoltativo.  ad esempio uno dei seguenti:<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`Shadows`|Parametro facoltativo.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).|  
|`charsetmodifier`|Parametro facoltativo.  Specifica le informazioni sul set di caratteri e la ricerca dei file,  ad esempio uno dei seguenti:<br /><br /> -   [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md) \(impostazione predefinita\)<br />-   [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)<br />-   [Auto](../../../visual-basic/language-reference/modifiers/auto.md)|  
|`Sub`|Facoltativa. È necessario che sia specificato `Sub` o `Function`.  La routine esterna non restituirà alcun valore.|  
|`Function`|Facoltativa. È necessario che sia specificato `Sub` o `Function`.  La routine esterna non restituirà alcun valore.|  
|`name`|Obbligatorio.  Nome del riferimento esterno.  Per ulteriori informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`Lib`|Obbligatorio.  Introduce una clausola `Lib` che identifica il file esterno \(risorsa di codice o DLL\) contenente una routine esterna.|  
|`libname`|Obbligatorio.  Nome del file che contiene la routine dichiarata.|  
|`Alias`|Parametro facoltativo.  Il nome specificato in `name` non consente di identificare la routine che viene dichiarata nel file che la contiene.  Specificarne l'identificazione in `aliasname`.|  
|`aliasname`|Obbligatorio quando si utilizza la parola chiave `Alias`.  Stringa che identifica la routine in uno dei due modi seguenti:<br /><br /> Nome del punto di ingresso della routine contenuta nel file, racchiusa tra virgolette \(`""`\)<br /><br /> In alternativa<br /><br /> Cancelletto \(`#`\) seguito da un Integer che specifica il numero ordinale del punto di ingresso della routine contenuta nel file|  
|`parameterlist`|Obbligatorio se la routine accetta parametri.  Vedere [Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md).|  
|`returntype`|Obbligatorio se `Function` è specificato e `Option Strict` è `On`.  Tipo di dati del valore restituito dalla routine.|  
  
## Note  
 Talvolta è necessario chiamare una routine definita in un file, ad esempio DLL o risorsa codice, all'esterno del progetto.  Quando si esegue questa operazione, il compilatore Visual Basic non può accedere alle informazioni necessarie per chiamare la routine in modo corretto, ad esempio il percorso della routine, la modalità di identificazione, la sequenza di chiamata e il tipo restituito e il set di caratteri stringa utilizzato.  L'istruzione `Declare` crea un riferimento a una routine esterna e fornisce le informazioni necessarie.  
  
 È possibile utilizzare la parola chiave `Declare` solo a livello di modulo.  In altri termini, il *contesto della dichiarazione* per un riferimento esterno deve essere una classe, una struttura o un modulo e non può essere un file di origine, uno spazio dei nomi, un'interfaccia, una routine o un blocco.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 L'impostazione predefinita dei riferimenti esterni è l'accesso [Public](../../../visual-basic/language-reference/modifiers/public.md).  È possibile modificarne i livelli di accesso mediante gli appositi modificatori.  
  
## Regole  
  
-   **Attributi.** È possibile applicare attributi a un riferimento esterno.  Tutti gli attributi applicati hanno effetto solo nel progetto e non nel file esterno.  
  
-   **Modificatori.** Le routine esterne sono implicitamente di tipo [Shared](../../../visual-basic/language-reference/modifiers/shared.md).  Non è possibile utilizzare la parola chiave `Shared` durante la dichiarazione di un riferimento esterno e nemmeno modificarne lo stato condiviso.  
  
     Non è possibile utilizzare una routine esterna per l'esecuzione di override, l'implementazione di membri di interfaccia o la gestione di eventi.  Di conseguenza, non è possibile utilizzare la parola chiave `Overrides`, `Overridable`, `NotOverridable`, `MustOverride`, `Implements` o `Handles` in un'istruzione `Declare`.  
  
-   **Nome di una routine esterna.** Non è necessario assegnare al riferimento esterno lo stesso nome \(in `name`\) del punto di ingresso della routine nel relativo file esterno \(`aliasname`\).  Per specificare il nome del punto di ingresso, è possibile utilizzare una clausola `Alias`.  Questa operazione può essere utile se la routine esterna presenta lo stesso nome di un modificatore riservato in Visual Basic oppure di una variabile, una routine o un altro elemento di programmazione appartenente allo stesso ambito.  
  
    > [!NOTE]
    >  per i nomi dei punti di ingresso di quasi tutte le DLL viene applicata la distinzione tra lettere maiuscole e minuscole.  
  
-   **Numero di una routine esterna.** In alternativa, è possibile utilizzare una clausola `Alias` per specificare il numero ordinale del punto di ingresso nella tabella di esportazione del file esterno.  Per eseguire questa operazione, aggiungere un cancelletto \(`#`\) prima di `aliasname`.  Questa operazione può essere utile se il nome della routine esterna include un carattere non consentito in Visual Basic, oppure se la routine viene esportata nel file esterno senza nome.  
  
## Regole per tipi di dati  
  
-   **Tipi di dati dei parametri.** Se `Option Strict` è `On`, è necessario specificare il tipo di dati di ogni parametro in `parameterlist`.  È possibile specificare un tipo di dati qualsiasi oppure il nome di un'enumerazione, struttura, classe o interfaccia.  In `parameterlist`, è possibile utilizzare una clausola `As` per specificare il tipo di dati dell'argomento da passare a ciascun parametro.  
  
    > [!NOTE]
    >  se la routine esterna non è stata scritta per .NET Framework, accertarsi che i tipi di dati corrispondano.  Se ad esempio si dichiara un riferimento esterno a una routine Visual Basic 6.0 con un parametro `Integer` \(16 bit in Visual Basic 6.0\), è necessario identificare l'argomento corrispondente come `Short` nell'istruzione `Declare`, che corrisponde al tipo Integer a 16 bit in Visual Basic.  In modo simile, il tipo `Long` dispone di una diversa ampiezza di dati in Visual Basic 6.0, pertanto `Date` viene implementato in modo differente.  
  
-   **Tipo di dati restituito.** Se la routine esterna è di tipo `Function` e `Option Strict` è `On`, è necessario specificare il tipo di dati del valore restituito al codice chiamante.  È possibile specificare un tipo di dati qualsiasi oppure il nome di un'enumerazione, struttura, classe o interfaccia.  
  
    > [!NOTE]
    >  il compilatore Visual Basic non verifica che i tipi di dati siano compatibili con quelli della routine esterna.  In caso di mancata corrispondenza, Common Language Runtime genera un'eccezione <xref:System.Runtime.InteropServices.MarshalDirectiveException> in fase di esecuzione.  
  
-   **Tipi di dati predefiniti.** Se `Option Strict` è `Off` e non si specifica il tipo di dati di un parametro in `parameterlist`, il compilatore Visual Basic converte l'argomento corrispondente nel [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md).  In modo simile, se non si specifica `returntype`, il compilatore accetta `Object` come tipo di dati restituito.  
  
    > [!NOTE]
    >  è possibile che la routine esterna sia stata scritta in un'altra piattaforma, quindi eventuali ipotesi sui tipi di dati o il relativo utilizzo come valori predefiniti può essere rischioso.  È molto più sicuro specificare il tipo di dati di ogni parametro e dell'eventuale valore restituito  per migliorare anche la leggibilità del programma.  
  
## Comportamento  
  
-   **Ambito.** Un riferimento esterno appartiene all'ambito della classe, della struttura o del modulo in cui viene dichiarato.  
  
-   **Durata.** Un riferimento esterno presenta la stessa durata della classe, della struttura o del modulo in cui è stato dichiarato.  
  
-   **Chiamata di una routine esterna.** Una routine esterna viene chiamata nello stesso modo di una routine `Function` o `Sub`, ovvero utilizzandola in un'espressione se restituisce un valore oppure specificandola in un'[Call Statement](../../../visual-basic/language-reference/statements/call-statement.md) se non restituisce alcun valore.  
  
     Gli argomenti vengono passati alla routine esterna esattamente come specificato da `parameterlist` nell'istruzione `Declare`,  senza tenere in considerazione il modo in cui sono stati originariamente dichiarati i parametri nel file esterno.  In modo simile, l'eventuale valore restituito deve essere utilizzato esattamente come specificato da `returntype` nell'istruzione `Declare`.  
  
-   **Set di caratteri.** In `charsetmodifier` è possibile specificare la modalità di marshalling da applicare alle stringhe quando in Visual Basic viene chiamata la routine esterna.  Il modificatore `Ansi` indica di effettuare il marshalling di tutte le stringhe in valori ANSI mentre il modificatore `Unicode` specifica il marshalling in valori Unicode.  Il modificatore `Auto` indica di effettuare il marshalling delle stringhe secondo le regole di .NET Framework, in base al `name` del riferimento esterno, oppure all'eventuale `aliasname` specificato.  Il valore predefinito è `Ansi`.  
  
     `charsetmodifier` specifica inoltre la modalità di ricerca in Visual Basic della routine esterna contenuta nel file esterno.  `Ansi` e `Unicode` indicano di effettuare la ricerca senza modificare il nome della routine.  `Auto` richiede la definizione del set di caratteri base della piattaforma runtime ed eventualmente di modificare il nome della routine esterna nel modo seguente:  
  
    -   in una piattaforma ANSI, quale Windows 95, Windows 98 o Windows Millennium Edition, cercare innanzitutto la routine esterna senza modificarne il nome.  Se la ricerca non riesce, aggiungere una "A" alla fine del nome della routine esterna e riprovare.  
  
    -   In una piattaforma Unicode, quale Windows NT, Windows 2000 o Windows XP, cercare innanzitutto la routine esterna senza modificarne il nome.  Se la ricerca non riesce, aggiungere una "W" alla fine del nome della routine esterna e riprovare.  
  
-   **Meccanismo.** Per risolvere le routine esterne e accedervi, in Visual Basic viene utilizzato il meccanismo *platform invoke* \(PInvoke\) di .NET Framework.  Sia l'istruzione `Declare` sia la classe <xref:System.Runtime.InteropServices.DllImportAttribute> utilizzano questo meccanismo automaticamente, pertanto non è richiesta la conoscenza di PInvoke.  Per ulteriori informazioni, vedere [Walkthrough: Calling Windows APIs](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md).  
  
> [!IMPORTANT]
>  se la routine esterna viene eseguita all'esterno di Common Language Runtime \(CLR\), viene definita *codice non gestito*.  Una chiamata a questo tipo di routine, ad esempio a una funzione API Win32 o a un metodo COM, può esporre l'applicazione a problemi di sicurezza.  Per ulteriori informazioni, vedere [Secure Coding Guidelines for Unmanaged Code](../Topic/Secure%20Coding%20Guidelines%20for%20Unmanaged%20Code.md).  
  
## Esempio  
 Nell'esempio seguente viene dichiarato un riferimento esterno a una routine `Function` che restituisce il nome dell'utente corrente.  Viene quindi chiamata la routine esterna `GetUserNameA` come parte della routine `getUser`.  
  
 [!code-vb[VbVbalrStatements#15](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/declare-statement_1.vb)]  
  
## Esempio  
 La classe <xref:System.Runtime.InteropServices.DllImportAttribute> rappresenta un'alternativa all'utilizzo di funzioni nel codice non gestito.  Nell'esempio seguente viene dichiarata una funzione importata senza l'utilizzo di un'istruzione `Declare`.  
  
 [!code-vb[VbVbalrStatements#16](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/declare-statement_2.vb)]  
  
 [!code-vb[VbVbalrStatements#1](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/declare-statement_3.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>   
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [AddressOf Operator](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Call Statement](../../../visual-basic/language-reference/statements/call-statement.md)   
 [Walkthrough: Calling Windows APIs](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)