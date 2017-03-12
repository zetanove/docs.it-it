---
title: "Property Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.PropertySet"
  - "vb.Property"
  - "vb.PropertyGet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Property (istruzione)"
  - "modificatore predefinito"
  - "proprietà (routine), istruzioni di proprietà"
  - "Property (parola chiave)"
ms.assetid: 3155edaf-8ebd-45c6-9cef-11d5d2dc8d38
caps.latest.revision: 41
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 41
---
# Property Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Dichiara il nome di una proprietà e le routine della proprietà usate per archiviare e recuperare il valore della proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attributelist> ] [ Default ] [ accessmodifier ]   
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ] [ Iterator ]  
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]  
    [ <attributelist> ] [ accessmodifier ] Get  
        [ statements ]  
    End Get  
    [ <attributelist> ] [ accessmodifier ] Set ( ByVal value As returntype [, parameterlist ] )  
        [ statements ]  
    End Set  
End Property  
- or -  
[ <attributelist> ] [ Default ] [ accessmodifier ]   
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ]   
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]  
  
```  
  
## <a name="parts"></a>Parti  
  
-   `attributelist`  
  
     Facoltativo. Elenco di attributi applicabili a questa proprietà o `Get` o `Set` procedura. Vedere [elenco attributi](../../../visual-basic/language-reference/statements/attribute-list.md).  
  
-   `Default`  
  
     Facoltativo. Specifica che questa proprietà è la proprietà predefinita per la classe o struttura in cui è definito. Valore predefinito deve accettare parametri e possono essere impostare e recuperare proprietà senza specificare il nome della proprietà. Se si dichiara la proprietà come `Default`, non è possibile utilizzare `Private` sulla proprietà né sulle routine della proprietà.  
  
-   `accessmodifier`  
  
     Facoltativo per il `Property` istruzione e almeno uno del `Get` e `Set` istruzioni. Può essere uno dei seguenti:  
  
    -   [Pubblica](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protetto](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Privato](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
-   `propertymodifiers`  
  
     Facoltativo. Può essere uno dei seguenti:  
  
    -   [Overload](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [Esegue l'override](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [Sottoponibili a override](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     Facoltativo. Vedere [condivisi](../../../visual-basic/language-reference/modifiers/shared.md).  
  
-   `Shadows`  
  
     Facoltativo. Vedere [ombreggiature](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
-   `ReadOnly`  
  
     Facoltativo. Vedere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
-   `WriteOnly`  
  
     Facoltativo. Vedere [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md).  
  
-   `Iterator`  
  
     Facoltativo. Vedere [iteratore](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
-   `name`  
  
     Obbligatorio. Nome della proprietà. Vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   `parameterlist`  
  
     Facoltativo. Elenco di nomi di variabili locali che rappresenta i parametri di questa proprietà e gli eventuali parametri aggiuntivi di `Set` procedura. Vedere [elenco parametri](../../../visual-basic/language-reference/statements/parameter-list.md).  
  
-   `returntype`  
  
     Obbligatorio se `Option``Strict` è `On`. Tipo di dati del valore restituito da questa proprietà.  
  
-   `Implements`  
  
     Facoltativo. Indica che questa proprietà implementa una o più proprietà, ognuna definita in un'interfaccia implementata dalla classe o struttura contenente questa proprietà. Vedere [implementa istruzione](../../../visual-basic/language-reference/statements/implements-statement.md).  
  
-   `implementslist`  
  
     Necessario se si fornisce `Implements`. Elenco delle proprietà in fase di implementazione.  
  
     `implementedproperty [ , implementedproperty ... ]`  
  
     Ogni `implementedproperty` presenta la sintassi e le parti seguenti:  
  
     `interface.definedname`  
  
    |||  
    |-|-|  
    |Parte|Descrizione|  
    |`interface`|Obbligatorio. Nome di un'interfaccia implementata da questa proprietà contenente classe o struttura.|  
    |`definedname`|Obbligatorio. Nome con cui la proprietà è definita in `interface`.|  
  
-   `Get`  
  
     Facoltativo. Obbligatorio se la proprietà è contrassegnata `WriteOnly`. Avvia un `Get` routine di proprietà che viene utilizzata per restituire il valore della proprietà.  
  
-   `statements`  
  
     Facoltativo. Blocco di istruzioni da eseguire all'interno di `Get` o `Set` procedura.  
  
-   `End Get`  
  
     Termina la `Get` routine di proprietà.  
  
-   `Set`  
  
     Facoltativo. Obbligatorio se la proprietà è contrassegnata `ReadOnly`. Avvia un `Set` routine di proprietà che viene utilizzata per archiviare il valore della proprietà.  
  
-   `End Set`  
  
     Termina la `Set` routine di proprietà.  
  
-   `End Property`  
  
     Termina la definizione di questa proprietà.  
  
## <a name="remarks"></a>Note  
 Il `Property` istruzione introduce la dichiarazione di una proprietà. Una proprietà può avere un `Get` procedure (sola lettura), un `Set` procedure (sola scrittura) o entrambe (lettura-scrittura). È possibile omettere il `Get` e `Set` procedura quando si utilizza una proprietà implementata automaticamente. Per ulteriori informazioni, vedere [proprietà implementate automaticamente](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md).  
  
 È possibile utilizzare `Property` solo a livello di classe. Ciò significa che il *contesto della dichiarazione* per una proprietà deve essere una classe, struttura, modulo o interfaccia e non può essere un file di origine, lo spazio dei nomi, routine o blocco. Per ulteriori informazioni, vedere [contesti delle dichiarazioni e livelli di accesso predefinito](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Per impostazione predefinita, le proprietà utilizzano l'accesso pubblico. È possibile modificare il livello di accesso della proprietà con un modificatore di accesso nella `Property` istruzione ed è possibile impostare una delle routine della proprietà a un livello di accesso più restrittivo.  
  
 Visual Basic passa un parametro per il `Set` procedura durante le assegnazioni di proprietà. Se non si fornisce un parametro per `Set`, l'ambiente di sviluppo integrato (IDE) utilizza un parametro implicito denominato `value`. Questo parametro contiene il valore da assegnare alla proprietà. In genere questo valore in una variabile locale privata e restituirlo ogni volta che il `Get` routine viene chiamata.  
  
## <a name="rules"></a>Regole  
  
-   **Livelli di accesso misti.** Se si definisce una proprietà di lettura / scrittura, è possibile specificare facoltativamente un livello di accesso diversi per la `Get` o `Set` procedura, ma non entrambi. In questo caso, il livello di accesso procedura deve essere più restrittivo rispetto a livello di accesso della proprietà. Ad esempio, se viene dichiarata la proprietà `Friend`, è possibile dichiarare il `Set` procedura `Private`, ma non `Public`.  
  
     Se si sta definendo un `ReadOnly` o `WriteOnly` proprietà, la procedura singola proprietà (`Get` o `Set`, rispettivamente) rappresenta tutte le proprietà. È possibile dichiarare un livello di accesso diversi per tale procedura, poiché verrebbero specificati due livelli di accesso per la proprietà.  
  
-   **Tipo restituito.** Il `Property` istruzione può dichiarare il tipo di dati del valore restituito. È possibile specificare qualsiasi tipo di dati o il nome di un'enumerazione, struttura, classe o interfaccia.  
  
     Se non si specifica `returntype`, la proprietà restituisce `Object`.  
  
-   **Implementazione.** Se questa proprietà viene utilizzata la `Implements` (parola chiave), classe o struttura deve avere un `Implements` istruzione immediatamente successiva relativo `Class` o `Structure` istruzione. Il `Implements` istruzione deve includere ogni interfaccia specificata in `implementslist`. Tuttavia, il nome con cui l'interfaccia definisce il `Property` (in `definedname`) non deve essere lo stesso nome di questa proprietà (in `name`).  
  
## <a name="behavior"></a>Comportamento  
  
-   **Restituzione da una routine di proprietà.** Quando il `Get` o `Set` procedure restituisce al codice chiamante, l'esecuzione continua con l'istruzione successiva all'istruzione che ha richiamato.  
  
     Il `Exit Property` e `Return` istruzioni di uscire immediatamente da una routine di proprietà. Un numero qualsiasi di `Exit Property` e `Return` istruzioni possono trovarsi in qualsiasi punto della procedura, ed è possibile combinare `Exit Property` e `Return` istruzioni.  
  
-   **Valore restituito.** Per restituire un valore da un `Get` procedura, è possibile assegnare il valore per il nome della proprietà o includerlo in un `Return` istruzione. Nell'esempio seguente assegna il valore restituito per il nome della proprietà `quoteForTheDay` e quindi utilizza il `Exit Property` istruzione per la restituzione.  
  
     [!code-vb[VbVbalrStatements#27](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/property-statement_1.vb)]  
  
     [!code-vb[VbVbalrStatements#28](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/property-statement_2.vb)]  
  
     Se si utilizza `Exit Property` senza assegnare un valore a `name`,  `Get` procedura restituisce il valore predefinito per il tipo di dati della proprietà.  
  
     Il `Return` Assegna istruzione allo stesso tempo la `Get` procedure restituire valore ed esce dalla procedura. Nell'esempio seguente viene illustrata questa operazione.  
  
     [!code-vb[VbVbalrStatements#27](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/property-statement_1.vb)]  
  
     [!code-vb[VbVbalrStatements#29](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/property-statement_3.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente dichiara una proprietà in una classe.  
  
 [!code-vb[VbVbalrStatements#51](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/property-statement_4.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà implementate automaticamente](../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [Oggetti e classi](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Get (istruzione)](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set (istruzione)](../../../visual-basic/language-reference/statements/set-statement.md)   
 [Elenco di parametri](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Default](../../../visual-basic/language-reference/modifiers/default.md)