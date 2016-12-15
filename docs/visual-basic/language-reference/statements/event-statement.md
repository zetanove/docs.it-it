---
title: "Event Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Event"
  - "vb.Custom"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Event statement"
  - "declaring events, syntax"
  - "Public keyword, Event statements"
  - "Custom keyword"
  - "declarations, events"
  - "event keyword [Visual Basic]"
  - "WithEvents keyword, Event statements"
  - "events [Visual Basic], declaring"
  - "ByVal keyword, Event statements"
  - "events [Visual Basic], custom"
  - "ByRef keyword, Event statements"
  - "declaring user-defined events"
ms.assetid: 306ff8ed-74dd-4b6a-bd2f-e91b17474042
caps.latest.revision: 33
caps.handback.revision: 33
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Event Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara un evento definito dall'utente.  
  
## Sintassi  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shared ] [ Shadows ] Event eventname[(parameterlist)] _  
[ Implements implementslist ]  
' -or-  
[ <attrlist> ] [ accessmodifier ] _  
[ Shared ] [ Shadows ] Event eventname As delegatename _  
[ Implements implementslist ]  
' -or-  
 [ <attrlist> ] [ accessmodifier ] _  
[ Shared ] [ Shadows ] Custom Event eventname As delegatename _  
[ Implements implementslist ]  
   [ <attrlist> ] AddHandler(ByVal value As delegatename)  
      [ statements ]  
   End AddHandler  
   [ <attrlist> ] RemoveHandler(ByVal value As delegatename)  
      [ statements ]  
   End RemoveHandler  
   [ <attrlist> ] RaiseEvent(delegatesignature)  
      [ statements ]  
   End RaiseEvent  
End Event  
```  
  
## Parti  
  
|||  
|-|-|  
|Parte|Descrizione|  
|`attrlist`|Parametro facoltativo.  Elenco degli attributi applicabili all'evento.  Gli attributi sono separati da una virgola.  È necessario racchiudere l'[Attribute List](../../../visual-basic/language-reference/statements/attribute-list.md) tra parentesi angolari \("`<`" e "`>`"\).|  
|`accessmodifier`|Parametro facoltativo.  Specifica il tipo di codice che può accedere all'evento.  Può essere uno dei seguenti:<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md): può accedere qualsiasi codice che sia in grado di accedere all'elemento che lo dichiara.<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md): può accedere solo il codice incluso nella relativa classe o in una classe derivata.<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md): può accedere solo il codice incluso nello stesso assembly.<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md): può accedere solo il codice incluso nell'elemento che lo dichiara.<br /><br /> Si può specificare `Protected Friend` per abilitare l'accesso dal codice incluso nella classe dell'evento, in una classe derivata o nello stesso assembly.|  
|`Shared`|Parametro facoltativo.  Specifica che l'evento non è associato a una specifica istanza di una classe o di una struttura.|  
|`Shadows`|Parametro facoltativo.  Indica che l'evento ridichiara e nasconde un elemento di programmazione omonimo o un insieme di elementi in overload di una classe base.  È possibile nascondere qualsiasi tipo di elemento dichiarato con qualsiasi altro tipo.<br /><br /> Un elemento nascosto non è disponibile all'interno della classe derivata che lo nasconde, a meno che l'elemento di shadowing sia inaccessibile.  Ad esempio, se un elemento `Private` nasconde un elemento della classe base, il codice che non dispone dell'autorizzazione per accedere all'elemento `Private` accede invece all'elemento della classe base.|  
|`eventname`|Necessario.  Nome dell'evento, conforme alle convenzioni di denominazione standard delle variabili.|  
|`parameterlist`|Parametro facoltativo.  Elenco di variabili locali che rappresentano i parametri dell'evento.  L'[Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md) deve essere racchiuso tra parentesi.|  
|`Implements`|Parametro facoltativo.  Indica che l'evento implementa un evento di un'interfaccia.|  
|`implementslist`|Necessario se si fornisce `Implements`.  Elenco delle routine `Sub` implementate.  Nel caso di più routine, è possibile separarle mediante virgole.<br /><br /> *implementedprocedure* \[ , *implementedprocedure* ...  \]<br /><br /> Ogni `implementedprocedure` presenta la sintassi e le parti seguenti:<br /><br /> `interface`.`definedname`<br /><br /> -   `interface` \- Obbligatorio.  Nome di un'interfaccia implementata dalla classe o dalla struttura che contiene la routine.<br />-   `Definedname` \- Obbligatorio.  Nome mediante il quale la routine viene definita in `interface`.  Non è necessario che questo nome corrisponda al nome usato dalla routine per implementare la routine definita, ossia `name`.|  
|`Custom`|Necessario.  È necessario che gli eventi dichiarati come `Custom` definiscano funzioni di accesso `AddHandler`, `RemoveHandler` e `RaiseEvent` personalizzate.|  
|`delegatename`|Parametro facoltativo.  Nome del delegato che specifica la firma del gestore eventi.|  
|`AddHandler`|Necessario.  Dichiara una funzione di accesso `AddHandler` che specifica le istruzioni da eseguire quando viene aggiunto un gestore eventi, sia in modo esplicito mediante l'istruzione `AddHandler` che in modo implicito mediante la clausola `Handles`|  
|`End AddHandler`|Necessario.  Termina il blocco `AddHandler`.|  
|`value`|Necessario.  Nome parametro.|  
|`RemoveHandler`|Necessario.  Dichiara una funzione di accesso `RemoveHandler`, che specifica le istruzioni da eseguire quando un gestore eventi viene rimosso mediante l'istruzione `RemoveHandler`.|  
|`End RemoveHandler`|Necessario.  Termina il blocco `RemoveHandler`.|  
|`RaiseEvent`|Necessario.  Dichiara una funzione di accesso `RaiseEvent`, che specifica le istruzioni da eseguire quando l'evento viene generato mediante l'istruzione `RaiseEvent`.  In genere, viene richiamato un elenco di delegati gestito dalle funzioni di accesso `AddHandler` e `RemoveHandler`.|  
|`End RaiseEvent`|Necessario.  Termina il blocco `RaiseEvent`.|  
|`delegatesignature`|Necessario.  Elenco di parametri che corrisponde ai parametri richiesti dal delegato `delegatename`.  L'[Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md) deve essere racchiuso tra parentesi.|  
|`statements`|Parametro facoltativo.  Istruzioni che includono i corpi dei metodi `AddHandler`, `RemoveHandler` e `RaiseEvent`.|  
|`End Event`|Necessario.  Termina il blocco `Event`.|  
  
## Note  
 Dopo aver dichiarato l'evento, usare l'istruzione `RaiseEvent` per generarlo.  Nei frammenti seguenti viene mostrato un esempio tipico di dichiarazione e generazione di un evento:  
  
 [!code-vb[VbVbalrEvents#13](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/event-statement_1.vb)]  
  
> [!NOTE]
>  È possibile dichiarare argomenti per gli eventi analogamente a quanto avviene per gli argomenti di routine, tenendo però conto che non è possibile specificare per gli eventi argomenti denominati, argomenti `ParamArray` o argomenti `Optional`,   né ottenere da essi valori restituiti.  
  
 Per gestire un evento è necessario associarlo a una subroutine del gestore eventi mediante l'istruzione `Handles` o `AddHandler`.  Le firme della subroutine e dell'evento devono corrispondere.  Per gestire un evento condiviso è necessario usare l'istruzione `AddHandler`.  
  
 Si può usare `Event` solo a livello di modulo.  In altri termini, il *contesto della dichiarazione* per un evento deve essere una classe, una struttura, un modulo o un'interfaccia e non può essere un file di origine, uno spazio dei nomi, una routine o un blocco.  Per altre informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Nella maggior parte dei casi, per dichiarare un evento è possibile usare la prima sintassi nella sezione relativa alla sintassi di questo argomento.  In alcuni scenari è tuttavia necessario disporre di un controllo maggiore sui dettagli del comportamento dell'evento.  L'ultima sintassi nella sezione relativa alla sintassi di questo argomento, che usa la parola chiave `Custom`, offre questa possibilità consentendo la definizione di eventi personalizzati.  In un evento personalizzato si specifica esattamente ciò che accade quando il codice aggiunge o rimuove un gestore eventi a o dall'evento oppure quando il codice genera l'evento.  Per esempi, vedere [How to: Declare Custom Events To Conserve Memory](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md) e [How to: Declare Custom Events To Avoid Blocking](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md).  
  
## Esempio  
 Negli esempi seguenti, gli eventi vengono usati per il conto alla rovescia dei secondi, da 10 a 0.  Il codice illustra numerosi metodi, proprietà e istruzioni correlati agli eventi,  inclusa l'istruzione `RaiseEvent`.  
  
 La classe che genera un evento viene definita origine e i metodi che lo elaborano vengono definiti gestori eventi.  Un'origine eventi può disporre di più gestori per gli eventi generati.  Quando la classe genera l'evento, lo stesso evento viene generato in tutte le classi per cui è stato scelto di gestire eventi per tale istanza dell'oggetto.  
  
 Nell'esempio vengono usati anche un form \(`Form1`\) con un pulsante \(`Button1`\) e una casella di testo \(`TextBox1`\).  Quando si fa clic sul pulsante, nella prima casella di testo viene visualizzato il conto alla rovescia dei secondi da 10 a 0.  Al termine dei 10 secondi, nella prima casella di testo viene visualizzato "Done".  
  
 Il codice di `Form1` specifica gli stati di inizio e fine del form.  Contiene inoltre il codice eseguito quando vengono generati gli eventi.  
  
 Per usare l'esempio, aprire un nuovo progetto Windows Form.  Aggiungere quindi un pulsante denominato `Button1` e una casella di testo denominata `TextBox1` al form principale, denominato `Form1`.  Quindi, fare quindi clic con il pulsante destro del mouse sul form e scegliere **Visualizza codice** per aprire l'editor di codice.  
  
 Aggiungere una variabile `WithEvents` alla sezione delle dichiarazioni della classe `Form1`:  
  
 [!code-vb[VbVbalrEvents#14](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/event-statement_2.vb)]  
  
 Aggiungere il codice seguente al codice per `Form1`:  Sostituire eventuali routine duplicate, ad esempio `Form_Load` o `Button_Click`.  
  
 [!code-vb[VbVbalrEvents#15](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/event-statement_3.vb)]  
  
 Premere F5 per eseguire l'esempio precedente, quindi fare clic sul pulsante con etichetta **Start** Nella prima casella di testo viene avviato il conto alla rovescia dei secondi.  Al termine dei 10 secondi, nella prima casella di testo viene visualizzato "Done".  
  
> [!NOTE]
>  Il metodo `My.Application.DoEvents` non elabora gli eventi allo stesso modo del form.  Per consentire al form di gestire direttamente gli eventi, si può ricorrere al multithreading.  Per altre informazioni, vedere [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Vedere anche  
 [RaiseEvent Statement](../../../visual-basic/language-reference/statements/raiseevent-statement.md)   
 [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)   
 [AddHandler Statement](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler Statement](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Delegate Statement](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [How to: Declare Custom Events To Conserve Memory](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)   
 [How to: Declare Custom Events To Avoid Blocking](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)   
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)