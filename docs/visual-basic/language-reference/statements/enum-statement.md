---
title: "Istruzione Enum (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Enum"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "costanti enumerate"
  - "Enum (istruzione)"
  - "Parola chiave privata, enum (istruzioni)"
  - "Parola chiave Public, in istruzione Enum"
  - "variabili [Visual Basic], enumerazione"
  - "costanti enumerate"
ms.assetid: a45e51f1-65ff-48e1-bf32-79130f137377
caps.latest.revision: 44
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 44
---
# Istruzione Enum (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Dichiara un'enumerazione e definisce i valori dei relativi membri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ]  [ Shadows ]   
Enum enumerationname [ As datatype ]   
   memberlist  
End Enum  
```  
  
## <a name="parts"></a>Parti  
  
-   `attributelist`  
  
     Facoltativo. Elenco di attributi che si applicano a questa enumerazione. È necessario racchiudere il [elenco attributi](../../../visual-basic/language-reference/statements/attribute-list.md) parentesi angolari ("`<`"e"`>`").  
  
     Il <xref:System.FlagsAttribute> attributo indica che il valore di un'istanza di enumerazione può includere più membri di enumerazione, e che ogni membro rappresenta un campo di bit nel valore di enumerazione.  
  
-   `accessmodifier`  
  
     Facoltativo. Specifica il codice può accedere a questa enumerazione. Può essere uno dei seguenti:  
  
    -   [Pubblica](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protetto](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Privato](../../../visual-basic/language-reference/modifiers/private.md)  
  
     È possibile specificare `Protected``Friend` per consentire l'accesso dal codice all'interno dello stesso assembly, una classe derivata o classe dell'enumerazione.  
  
-   `Shadows`  
  
     Facoltativo. Specifica che l'enumerazione ridichiara e nasconde un elemento di programmazione omonimo o un set di elementi in overload, una classe di base. È possibile specificare [ombreggiature](../../../visual-basic/language-reference/modifiers/shadows.md) solo sull'enumerazione, non sui relativi membri.  
  
-   `enumerationname`  
  
     Obbligatorio. Nome dell'enumerazione. Per informazioni sui nomi validi, vedere [nomi di elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   `datatype`  
  
     Facoltativo. Tipo di dati dell'enumerazione e tutti i relativi membri.  
  
-   `memberlist`  
  
     Obbligatorio. Elenco di costanti membro dichiarato nella presente informativa. Più membri vengono visualizzati in righe di codice sorgente singoli.  
  
     Ogni `member` presenta la sintassi e le parti seguenti: `[<attribute list>] member name [ = initializer ]`  
  
    |||  
    |-|-|  
    |Parte|Descrizione|  
    |`membername`|Obbligatorio. Nome del membro.|  
    |`initializer`|Facoltativo. Espressione che viene valutata in fase di compilazione e assegnata al membro.|  
  
-   `End` `Enum`  
  
     Termina il blocco `Enum`.  
  
## <a name="remarks"></a>Note  
 Se si dispone di un set di valori non modificabili logicamente correlati tra loro, è possibile definirli insieme in un'enumerazione. Fornisce nomi significativi per l'enumerazione e i relativi membri, che sono più facili da ricordare rispetto ai relativi valori. È quindi possibile utilizzare i membri di enumerazione in molte posizioni nel codice.  
  
 Di seguito sono indicati i vantaggi dell'utilizzo di enumerazioni:  
  
-   Per ridurre gli errori causati dalla trasposizione o digitazione di numeri.  
  
-   Consente di modificare i valori in futuro.  
  
-   Rende il codice più leggibile, ciò significa che è meno probabile che gli errori verranno introdotte.  
  
-   Garantisce la compatibilità. Se si utilizzano le enumerazioni, il codice è meno probabile che non venga completata se in futuro un utente modifica i valori corrispondenti ai nomi dei membri.  
  
 Un'enumerazione ha un nome, tipo di dati sottostante e un set di membri. Ogni membro rappresenta una costante.  
  
 Un'enumerazione dichiarata a livello di classe, struttura, modulo o interfaccia, all'esterno di qualsiasi routine, è un *enumerazione membro*. È un membro della classe, struttura, modulo o interfaccia che lo dichiara.  
  
 Le enumerazioni di membri è possibile accedere da qualsiasi loro classe, struttura, modulo o interfaccia. Codice esterno di una classe, struttura o un modulo necessario qualificare il nome di un'enumerazione di membri con il nome di tale classe, struttura o un modulo. È possibile evitare la necessità di utilizzare nomi completi mediante l'aggiunta di un [importazioni](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) istruzione per il file di origine.  
  
 Un'enumerazione dichiarata a livello di spazio dei nomi, all'esterno di qualsiasi classe, struttura, modulo o interfaccia, è un membro dello spazio dei nomi in cui è presente.  
  
 Il *contesto della dichiarazione* per un'enumerazione deve essere un file di origine, lo spazio dei nomi, classe, struttura, modulo o interfaccia e non può essere una routine. Per ulteriori informazioni, vedere [contesti delle dichiarazioni e livelli di accesso predefinito](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 È possibile applicare attributi a un'enumerazione nel suo complesso, ma non ai relativi membri singolarmente. Un attributo fornisce informazioni per i metadati dell'assembly.  
  
## <a name="data-type"></a>Tipo di dati  
 Il `Enum` istruzione può dichiarare il tipo di dati di un'enumerazione. Ciascun membro viene attribuito il tipo di dati dell'enumerazione. È possibile specificare `Byte`, `Integer`, `Long`, `SByte`, `Short`, `UInteger`, `ULong`, o `UShort`.  
  
 Se non si specifica `datatype` per l'enumerazione, ogni membro viene attribuito il tipo di dati relativo `initializer`. Se si specificano sia `datatype` e `initializer`, il tipo di dati `initializer` deve essere convertibile in `datatype`. Se né `datatype` né `initializer` è presente, il tipo di dati il valore predefinito è `Integer`.  
  
## <a name="initializing-members"></a>Inizializzazione dei membri  
 Il `Enum` istruzione possibile inizializzare il contenuto di membri selezionati in `memberlist`. Utilizzare `initializer` per fornire un'espressione da assegnare al membro.  
  
 Se non si specifica `initializer` per un membro, Visual Basic inizializzato su zero (se è il primo `member` in `memberlist`), o su un valore maggiore di quello che di immediatamente precedente `member`.  
  
 L'espressione fornita in ciascun `initializer` può essere qualsiasi combinazione di valori letterali, altre costanti che sono già definiti e membri di enumerazione che sono già definiti, incluso un membro precedente di questa enumerazione. È possibile utilizzare gli operatori aritmetici e logici per combinare tali elementi.  
  
 Non è possibile utilizzare variabili o funzioni `initializer`. Tuttavia, è possibile utilizzare parole chiave di conversione, ad esempio `CByte` e `CShort`. È inoltre possibile utilizzare `AscW` Se viene chiamata con una costante `String` o `Char` argomento, dal momento che può essere valutata in fase di compilazione.  
  
 Le enumerazioni non possono avere valori a virgola mobile. Se un membro viene assegnato un valore a virgola mobile e `Option Strict` è impostata su on, si verifica un errore del compilatore. Se `Option Strict` è disattivata, il valore viene convertito automaticamente nel `Enum` tipo.  
  
 Se il valore di un membro supera l'intervallo consentito per il tipo di dati sottostante o se si inizializza un membro del valore massimo consentito dal tipo di dati sottostante, il compilatore segnala un errore.  
  
## <a name="modifiers"></a>Modificatori  
 Classe, struttura, modulo e predefinito enumerazioni membro di interfaccia di accesso pubblico. È possibile regolare i livelli di accesso con i modificatori di accesso. Spazio dei nomi predefinito enumerazioni di membro per l'accesso friend. È possibile regolare i livelli di accesso pubblico, ma non per privati o protetti. Per ulteriori informazioni, vedere [livelli di accesso in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Tutti i membri di enumerazione dispongono di accesso pubblico e non è possibile utilizzare i modificatori di accesso su di essi. Tuttavia, se l'enumerazione dispone di un livello di accesso più limitato, il livello di accesso di enumerazione specificato ha la precedenza.  
  
 Per impostazione predefinita, tutte le enumerazioni sono tipi e i campi sono costanti. Pertanto il `Shared`, `Static`, e `ReadOnly` le parole chiave non possono essere utilizzate quando si dichiara un'enumerazione o i relativi membri.  
  
## <a name="assigning-multiple-values"></a>L'assegnazione di più valori  
 Enumerazioni rappresentano in genere valori si escludono a vicenda. Includendo il <xref:System.FlagsAttribute> attributo il `Enum` dichiarazione, è possibile invece assegnare più valori a un'istanza dell'enumerazione. Il <xref:System.FlagsAttribute> attributo specifica che l'enumerazione vengono considerati come un campo di bit, ovvero un set di flag. Questi sono denominati *bit per bit* enumerazioni.  
  
 Quando si dichiara un'enumerazione tramite il <xref:System.FlagsAttribute> attributo, si consiglia di utilizzare potenze di 2, ovvero, 1, 2, 4, 8, 16 e così via, per i valori. È inoltre consigliabile "None" il nome di un membro il cui valore è 0. Per ulteriori istruzioni, vedere <xref:System.FlagsAttribute> e <xref:System.Enum>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il `Enum` istruzione. Si noti che il membro è detta `EggSizeEnum.Medium`, e non come `Medium`.  
  
 [!code-vb[VbEnumsTask#41](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#41)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente il metodo non è compreso il `Egg` (classe). Di conseguenza, `EggSizeEnum` completo come `Egg.EggSizeEnum`.  
  
 [!code-vb[VbEnumsTask#42](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#42)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `Enum` istruzione per definire un set correlato di valori costanti denominati. In questo caso, i valori sono i colori, che è possibile scegliere di progettare il form di immissione di dati per un database.  
  
 [!code-vb[VbEnumsTask#30](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#30)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono illustrati i valori che includono numeri positivi e negativi.  
  
 [!code-vb[VbEnumsTask#31](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#31)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, un `As` clausola viene utilizzata per specificare il `datatype` di un'enumerazione.  
  
 [!code-vb[VbEnumsTask#6](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#6)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare un'enumerazione bit per bit. Più valori possono essere assegnati a un'istanza di un'enumerazione bit per bit. Il `Enum` dichiarazione include il <xref:System.FlagsAttribute> attributo, che indica che l'enumerazione può essere considerato come un set di flag.  
  
 [!code-vb[VbEnumsTask#61](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#61)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente scorre un'enumerazione. Usa il <xref:System.Enum.GetNames%2A> metodo per recuperare una matrice dei nomi dei membri dell'enumerazione e <xref:System.Enum.GetValues%2A> per recuperare una matrice di valori del membro.  
  
 [!code-vb[VbEnumsTask#51](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#51)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Enum>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 [Const (istruzione)](../../../visual-basic/language-reference/statements/const-statement.md)   
 [Dim (istruzione)](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Conversioni implicite ed esplicite](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Funzioni di conversione del tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Costanti ed enumerazioni](../../../visual-basic/language-reference/constants-and-enumerations.md)