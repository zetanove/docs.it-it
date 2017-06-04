---
title: "Indipendenza del linguaggio e componenti indipendenti dal linguaggio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CLS (Common Language Specification)"
  - "Common Language Runtime, interoperabilità di linguaggio"
  - "Common Language Specification"
  - "interoperabilità tra linguaggi diversi"
  - "interoperabilità di linguaggio"
  - "runtime, interoperabilità di linguaggio"
ms.assetid: 4f0b77d0-4844-464f-af73-6e06bedeafc6
caps.latest.revision: 35
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 33
---
# Indipendenza del linguaggio e componenti indipendenti dal linguaggio
.NET Framework è indipendente dal linguaggio.  In qualità di sviluppatore, è pertanto possibile usare uno dei numerosi linguaggi destinati a .NET Framework, ad esempio C\#, C\+\+\/CLI, Eiffel, F\#, IronPython, IronRuby, PowerBuilder, Visual Basic, Visual COBOL e Windows PowerShell.  È possibile accedere a tipi e membri di librerie di classi sviluppate per .NET Framework senza dover conoscere il linguaggio in cui sono stati originariamente scritti e senza dover seguire nessuna delle convenzioni del linguaggio originale.  Se si è uno sviluppatore di componenti, l'accesso al componente può essere eseguito da qualsiasi applicazione .NET Framework, indipendentemente dal linguaggio.  
  
> [!NOTE]
>  La prima parte di questo articolo illustra la creazione di componenti indipendenti dal linguaggio, vale a dire componenti che possono essere usati da applicazioni scritte in qualsiasi linguaggio.  È anche possibile creare un singolo componente o applicazione dal codice sorgente scritto in più linguaggi. Vedere [Interoperabilità tra linguaggi diversi](#CrossLang) nella seconda parte di questo articolo.  
  
 È necessario che gli oggetti espongano ai chiamanti solo le funzionalità comuni a tutti i linguaggi, affinché sia garantita un'interazione completa con altri oggetti scritti in uno qualsiasi dei linguaggi.  Questo set comune di funzionalità è definito dalle specifiche CLS \(Common Language Specification\), un set di regole che si applicano agli assembly generati.  La specifica CLS \(Common Language Specification\) è definita nella partizione I, clausole da 7 a 11 di [Standard ECMA\-335: Common Language Infrastructure](http://go.microsoft.com/fwlink/?LinkID=116487).  
  
 Se il componente è conforme alle specifiche CLS \(Common Language Specification\), ne è garantita la conformità a CLS ed è possibile accedervi dal codice negli assembly scritti in qualsiasi linguaggio di programmazione che supporti CLS.  È possibile determinare se il componente è conforme alle specifiche CLS \(Common Language Specification\) in fase di compilazione applicando l'attributo <xref:System.CLSCompliantAttribute> al codice sorgente.  Per altre informazioni, vedere [Attributo CLSCompliantAttribute](#CLSAttribute).  
  
 Contenuto dell'articolo:  
  
-   [Regole di conformità a CLS](#Rules)  
  
    -   [Tipi e firme dei membri di tipo](#Types)  
  
    -   [Convenzioni di denominazione](#naming)  
  
    -   [Conversione di tipi](#conversion)  
  
    -   [Matrici](#arrays)  
  
    -   [Interfacce](#Interfaces)  
  
    -   [Enumerazioni](#enums)  
  
    -   [Membri dei tipi in generale](#members)  
  
    -   [Accessibilità del membro](#MemberAccess)  
  
    -   [Tipi e membri generici](#Generics)  
  
    -   [Costruttori](#ctors)  
  
    -   [Proprietà](#properties)  
  
    -   [Eventi](#events)  
  
    -   [Overloads](#overloads)  
  
    -   [Eccezioni](#exceptions)  
  
    -   [Attributi](#attributes)  
  
-   [Attributo CLSCompliantAttribute](#CLSAttribute)  
  
-   [Interoperabilità tra linguaggi diversi](#CrossLang)  
  
<a name="Rules"></a>   
## Regole di conformità a CLS  
 In questa sezione vengono illustrate le regole per creare un componente conforme a CLS.  Per un elenco completo di regole, vedere la partizione I, clausola 11 di [ECMA\-335 Standard: Common Language Infrastructure](http://go.microsoft.com/fwlink/?LinkID=116487).  
  
> [!NOTE]
>  Nelle specifiche CLS \(Common Language Specification\) viene illustrata ciascuna regola per la conformità a CLS applicata ai consumer \(sviluppatori che accedono a livello di codice a un componente conforme a CLS\), ai framework \(sviluppatori che usano un compilatore di linguaggio per creare librerie conformi a CLS\) e alle estensioni \(sviluppatori che creano uno strumento quale un compilatore di linguaggio o un parser di codice per la creazione di componenti conformi a CLS\).  Questo articolo è incentrato sulle regole che si applicano ai framework.  Si noti, tuttavia, che alcune delle regole applicate alle estensioni possono essere applicate anche agli assembly creati usando Reflection.Emit.  
  
 Per progettare un componente indipendente dal linguaggio, è necessario applicare le regole per la conformità a CLS solo all'interfaccia pubblica del componente.  L'implementazione privata non deve essere conforme alla specifica.  
  
> [!IMPORTANT]
>  Le regole per la conformità a CLS si applicano solo all'interfaccia pubblica di un componente, non alla relativa implementazione privata.  
  
 Ad esempio, Unsigned Integer diversi da <xref:System.Byte> non sono conformi a CLS.  Poiché tramite la classe `Person` nell'esempio seguente viene esposta una proprietà `Age` di tipo <xref:System.UInt16>, nel codice riportato di seguito viene visualizzato un avviso del compilatore.  
  
 [!code-csharp[Conceptual.CLSCompliant#1](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/public1.cs#1)]
 [!code-vb[Conceptual.CLSCompliant#1](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/public1.vb#1)]  
  
 È possibile rendere la classe `Person` conforme a CLS modificando il tipo di proprietà `Age` da <xref:System.UInt16> a <xref:System.> Int16?qualifyHint=False&autoUpgrade=True, vale a dire un Signed Integer a 16 bit conforme a CLS.  Non è necessario modificare il tipo del campo `personAge` privato.  
  
 [!code-csharp[Conceptual.CLSCompliant#2](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/public2.cs#2)]
 [!code-vb[Conceptual.CLSCompliant#2](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/public2.vb#2)]  
  
 L'interfaccia pubblica di una libreria è costituita dagli elementi seguenti:  
  
-   Definizioni di classi pubbliche.  
  
-   Definizioni dei membri pubblici di classi pubbliche e definizioni di membri accessibili alle classi derivate, cioè membri protetti.  
  
-   Parametri e tipi restituiti di metodi pubblici di classi pubbliche e parametri e tipi restituiti di metodi accessibili alle classi derivate.  
  
 Le regole per la conformità a CLS sono elencate nella tabella riportata di seguito.  Il testo delle regole è stato preso testualmente da [ECMA\-335 Standard: Common Language Infrastructure](http://go.microsoft.com/fwlink/?LinkID=116487), Copyright 2012 di Ecma International.  Nelle sezioni seguenti sono disponibili informazioni più dettagliate su queste regole.  
  
|Categoria|Vedere|Regola|Numero regola|  
|---------------|------------|------------|-------------------|  
|Accessibilità|[Accessibilità del membro](#MemberAccess)|L'accessibilità non sarà modificata quando si esegue l'override di metodi ereditati, tranne nel caso in cui si esegue l'override di un metodo ereditato da un assembly diverso con accessibilità `family-or-assembly`.  In questo caso, l'override disporrà dell'accessibilità `family`.|10|  
|Accessibilità|[Accessibilità del membro](#MemberAccess)|La visibilità e l'accessibilità di tipi e membri saranno tali che i tipi nella firma di qualsiasi membro saranno visibili e accessibili ogni volta che il membro stesso è visibile e accessibile.  Ad esempio, in un metodo pubblico che è visibile all'esterno del relativo assembly non deve essere presente un argomento il cui tipo è visibile solo nell'assembly.  La visibilità e l'accessibilità di tipi che compongono un tipo generico con istanze usato nella firma di qualsiasi membro saranno visibili e accessibili ogni volta che il membro stesso è visibile e accessibile.  Ad esempio, in un tipo generico con istanze presente nella firma di un membro visibile all'esterno del relativo assembly non deve essere disponibile un argomento generico il cui tipo è visibile solo nell'assembly.|12|  
|Matrici|[Matrici](#arrays)|Le matrici devono disporre di elementi con un tipo conforme a CLS e i limiti inferiori di tutte le dimensioni della matrice devono essere pari a zero.  Solo per il fatto che un elemento sia una matrice, il tipo di elemento della matrice sarà richiesto per eseguire una distinzione tra gli overload.  Quando l'overload è basato su due o più i tipi di matrice, i tipi di elemento vengono denominati tipi.|16|  
|Attributi|[Attributi](#attributes)|Gli attributi devono essere di tipo <xref:System.Attribute?displayProperty=fullName> o di un tipo che eredita da esso.|41|  
|Attributi|[Attributi](#attributes)|La specifica CLS consente solo un subset delle codifiche di attributi personalizzati.  Gli unici tipi che verranno visualizzati in queste codifiche sono \(vedere la partizione IV\): <xref:System.Type?displayProperty=fullName>, <xref:System.String?displayProperty=fullName>, <xref:System.Char?displayProperty=fullName>, <xref:System.Boolean?displayProperty=fullName>, <xref:System.Byte?displayProperty=fullName>, <xref:System.Int16?displayProperty=fullName>, <xref:System.Int32?displayProperty=fullName>, <xref:System.Int64?displayProperty=fullName>, <xref:System.Single?displayProperty=fullName>, <xref:System.Double?displayProperty=fullName> e qualsiasi tipo di enumerazione basato su un tipo Integer di base conforme a CLS.|34|  
|Attributi|[Attributi](#attributes)|La specifica CLS non consente i modificatori necessari visibili pubblicamente \(`modreq`, vedere la partizione II\), ma consente i modificatori facoltativi \(`modopt`, vedere la partizione II\) che non riconosce.|35|  
|Costruttori|[Costruttori](#ctors)|Prima di un eventuale accesso ai dati di istanza ereditati, tramite un costruttore di oggetti deve essere effettuata una chiamata a un costruttore di istanze della relativa classe di base.  Ciò non si applica ai tipi di valore, che non devono disporre di costruttori.|21|  
|Costruttori|[Costruttori](#ctors)|Un costruttore di oggetti non deve essere chiamato se non come parte della creazione di un oggetto e un oggetto non deve essere inizializzato due volte.|22|  
|Enumerazioni|[Enumerazioni](#enums)|Il tipo sottostante di un'enumerazione deve essere un tipo Integer CLS incorporato, il nome del campo deve essere "value\_\_" e il campo deve essere contrassegnato come `RTSpecialName`.|7|  
|Enumerazioni|[Enumerazioni](#enums)|Sono disponibili due tipi distinti di enumerazioni, indicati dalla presenza o dall'assenza dell'attributo personalizzato <xref:System.FlagsAttribute?displayProperty=fullName> \(vedere la libreria nella partizione IV\).  Una rappresenta Integer denominati, l'altra flag di bit denominati che possono essere combinati per generare un valore senza nome.  Il valore di un oggetto `enum` non è limitato ai valori specifici.|8|  
|Enumerazioni|[Enumerazioni](#enums)|Il tipo dei campi statici con valori letterali di un'enumerazione deve essere uguale a quello dell'enumerazione stessa.|9|  
|Eventi|[Eventi](#events)|I metodi tramite cui viene implementato un evento devono essere contrassegnati come `SpecialName` nei metadati.|29|  
|Eventi|[Eventi](#events)|L'accessibilità di un evento e le relative funzioni di accesso devono essere identiche.|30|  
|Eventi|[Eventi](#events)|I metodi `add` e `remove` per un evento devono essere entrambi presenti o entrambi assenti.|31|  
|Eventi|[Eventi](#events)|I metodi `add` e `remove` per un evento devono entrambi accettare un parametro tramite il cui tipo viene definito il tipo dell'evento e il tipo in questione deve essere derivato da <xref:System.Delegate?displayProperty=fullName>.|32|  
|Eventi|[Eventi](#events)|Gli eventi devono essere conformi a un pattern di nome specifico.  L'attributo `SpecialName` indicato nella regola CLS 29 deve essere ignorato nei confronti tra nomi appropriati e deve essere conforme alle regole dell'identificatore.|33|  
|Eccezioni|[Eccezioni](#exceptions)|Gli oggetti generati devono essere di tipo <xref:System.Exception?displayProperty=fullName> o di un tipo che eredita da esso.  Ciononostante, i metodi conformi a CLS non sono necessari per bloccare la propagazione di altri tipi di eccezioni.|40|  
|Generale|[Conformità a CLS: le regole](#Rules)|Le regole CLS sono valide solo per quelle parti di un tipo che sono accessibili o visibili all'esterno dell'assembly di definizione.|1|  
|Generale|[Conformità a CLS: le regole](#Rules)|I membri di tipi non conformi a CLS non saranno contrassegnati come conformi a CLS.|2|  
|Generics|[Tipi e membri generici](#Generics)|I tipi annidati disporranno di un numero di parametri generici almeno pari a quelli del tipo di inclusione.  I parametri generici di un tipo annidato corrispondono per posizione ai parametri generici del rispettivo tipo di inclusione.|42|  
|Generics|[Tipi e membri generici](#Generics)|Con il nome di un tipo generico verrà codificato il numero di parametri del tipo dichiarati nel tipo non annidato o appena introdotti nel tipo se annidato, in base alle regole definite sopra.|43|  
|Generics|[Tipi e membri generici](#Generics)|Tramite un tipo generico deve essere dichiarato nuovamente un numero di vincoli sufficiente a garantire che qualsiasi vincolo delle interfacce o del tipo base venga soddisfatto dai vincoli del tipo generico.|4444|  
|Generics|[Tipi e membri generici](#Generics)|I tipi usati come vincoli sui parametri generici dovranno essere essi stessi conformi a CLS.|45|  
|Generics|[Tipi e membri generici](#Generics)|La visibilità e l'accessibilità di membri \(compresi i tipi annidati\) in un tipo generico con istanze devono essere considerate come limitate all'ambito della creazione di un'istanza specifica, anziché come dichiarazione del tipo generico nel suo complesso.  Partendo da questo presupposto, valgono ancora le regole di visibilità e accessibilità della regola CLS 12.|46|  
|Generics|[Tipi e membri generici](#Generics)|Per ogni metodo generico astratto o virtuale sarà necessaria un'implementazione concreta \(non astratta\) predefinita.|47|  
|Interfacce|[Interfacce](#interfaces)|Per l'implementazione delle interfacce conformi a CLS non sarà necessaria la definizione di metodi non conformi a CLS.|18|  
|Interfacce|[Interfacce](#interfaces)|Tramite le interfacce conformi a CLS non verranno definiti i metodi statici, né verranno definiti i campi.|19|  
|Membri|[Membri dei tipi in generale](#members)|I metodi e i campi static globali non sono conformi a CLS.|36|  
|Membri|\-\-|Il valore di un valore statico letterale viene specificato attraverso l'uso dei metadati di inizializzazione del campo.  Un valore letterale conforme a CLS deve disporre di un valore specificato nei metadati di inizializzazione del campo che sia esattamente dello stesso tipo del valore letterale, o del tipo sottostante, se questo valore letterale è un oggetto `enum`.|13|  
|Membri|[Membri dei tipi in generale](#members)|Il vincolo vararg non fa parte delle specifiche CLS e l'unica convenzione di chiamata supportata da CLS è la convenzione di chiamata gestita standard.|15|  
|Convenzioni di denominazione|[Convenzioni di denominazione](#naming)|Gli assembly seguiranno l'allegato 7 del rapporto tecnico 15 di Unicode Standard 3.0 con cui viene controllato il set di caratteri che possono essere usati all'inizio e all'interno degli identificatori, disponibili online all'indirizzo http:\/\/www.unicode.org\/unicode\/reports\/tr15\/tr15\-18.html.  Gli identificatori dovranno essere nel formato canonico definito dal formato di normalizzazione Unicode C.  Per fini CLS, due identificatori sono identici se i relativi mapping di minuscole \(come specificato dai mapping di minuscole di tipo uno a uno, senza distinzione tra le impostazioni internazionali Unicode\) sono uguali.  Vale a dire, affinché due identificatori vengano considerati differenti nella specifica CLS, devono presentare differenze che vanno oltre la semplice distinzione tra maiuscole e minuscole.  Tuttavia, per eseguire l'override di una definizione non ereditata, per CLI è necessario l'uso della codifica precisa della dichiarazione originale.|4|  
|Overload|[Convenzioni di denominazione](#naming)|Tutti i nomi introdotti in un ambito conforme a CLS devono essere di tipo indipendente e distinto, fatta eccezione per i casi in cui i nomi sono identici e vengono risolti tramite l'overload.  Laddove, ad esempio, CTS consente a un unico tipo di usare lo stesso nome per un metodo e per un campo, CLS non lo consente.|5|  
|Overload|[Convenzioni di denominazione](#naming)|I campi e i tipi annidati devono risultare distinti in base al solo confronto tra identificatori, anche se CTS consente la distinzione di firme distinte.  I metodi, le proprietà e gli eventi che hanno lo stesso nome \(in base al confronto degli identificatori\) dovranno presentare differenze che vanno oltre il tipo restituito, a eccezione di quanto specificato nella regola CLS 39.|6|  
|Overload|[Overloads](#overloads)|È possibile eseguire l'overload solo di proprietà e metodi.|37|  
|Overload|[Overloads](#overloads)|Le proprietà e i metodi possono essere sottoposti a overload solo in base al numero e ai tipi dei relativi parametri, a eccezione degli operatori di conversione denominati `op_Implicit` e `op_Explicit`, i quali possono essere anche sottoposti a overload in base al relativo tipo restituito.|38|  
|Overload|\-\-|Se due o più metodi conformi a CLS dichiarati in un tipo hanno lo stesso nome e, per un set specifico di creazioni di istanze del tipo, dispongono dello stesso parametro e dei tipi restituiti, tutti questi metodi saranno semanticamente equivalenti alle creazioni di istanze del tipo.|48|  
|Tipi|[Tipo e firme dei membri di tipo](#Types)|<xref:System.Object?displayProperty=fullName> è conforme a CLS.  Qualsiasi altra classe conforme a CLS deve ereditare da una classe conforme a CLS.|23|  
|Proprietà|[Proprietà](#properties)|I metodi tramite cui vengono implementati i metodi Get e Set di una proprietà devono essere contrassegnati come `SpecialName` nei metadati.|24|  
|Proprietà|[Proprietà](#properties)|Le funzioni di accesso di una proprietà devono essere tutte statiche, tutte virtuali o tutte istanze.|26|  
|Proprietà|[Proprietà](#properties)|Il tipo di una proprietà deve essere il tipo restituito del metodo Get e il tipo dell'ultimo argomento del metodo Set.  I tipi dei parametri della proprietà devono essere i tipi dei parametri per il metodo Get e i tipi di tutti i parametri del metodo Set tranne l'ultimo.  Tutti questi tipi devono essere conformi a CLS e non devono essere puntatori gestiti, cioè non devono essere passati per riferimento.|27|  
|Proprietà|[Proprietà](#properties)|Le proprietà devono essere conformi a un pattern di nome specifico.  L'attributo `SpecialName` indicato nella regola CLS 24 deve essere ignorato nei confronti tra nomi appropriati e deve essere conforme alle regole dell'identificatore.  Una proprietà deve disporre di un metodo Get, un metodo Set o di entrambi.|28|  
|Conversione di tipi|[Conversione di tipi](#conversion)|Se viene specificato `op_Implicit` oppure `op_Explicit`, sarà necessario fornire un metodo alternativo di coercizione.|39|  
|Tipi|[Tipo e firme dei membri di tipo](#Types)|I tipi di valore boxed non sono conformi a CLS.|3|  
|Tipi|[Tipo e firme dei membri di tipo](#Types)|Tutti i tipi visualizzati in una firma devono essere conformi a CLS.  Tutti i tipi che costituiscono un tipo generico con istanze devono essere conformi a CLS.|11|  
|Tipi|[Tipo e firme dei membri di tipo](#Types)|I riferimenti tipizzati non sono conformi a CLS.|14|  
|Tipi|[Tipo e firme dei membri di tipo](#Types)|I tipi di puntatore non gestiti non sono conformi a CLS.|17|  
|Tipi|[Tipo e firme dei membri di tipo](#Types)|Per le classi, i tipi di valore e le interfacce conformi a CLS non è necessaria l'implementazione di membri non conformi a CLS.|20|  
  
<a name="Types"></a>   
### Tipi e firme dei membri di tipo  
 Il tipo <xref:System.Object?displayProperty=fullName> è conforme a CLS ed è il tipo di base di tutti i tipi di oggetto nel sistema di tipo .NET Framework.  L'ereditarietà in .NET Framework è implicita \(ad esempio la classe <xref:System.String> eredita in modo implicito dalla classe <xref:System.Object>\) o esplicita \(ad esempio la classe <xref:System.Globalization.CultureNotFoundException> eredita in modo esplicito dalla classe <xref:System.ArgumentException>, che eredita in modo esplicito dalla classe <xref:System.SystemException>, che eredita in modo esplicito dalla classe <xref:System.Exception>\).  Affinché un tipo derivato sia conforme a CLS, anche il tipo di base deve essere conforme a CLS.  
  
 Nell'esempio seguente viene illustrato un tipo derivato il cui tipo di base non è conforme a CLS.  Viene definita una classe `Counter` base tramite in cui viene usato un Unsigned Integer a 32 bit come contatore.  Poiché la classe fornisce la funzionalità contatore eseguendo il wrapping di un Unsigned Integer, la classe viene contrassegnata come non conforme a CLS.  Di conseguenza, anche una classe derivata, `NonZeroCounter`, non è conforme a CLS.  
  
 [!code-csharp[Conceptual.CLSCompliant#12](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/type3.cs#12)]
 [!code-vb[Conceptual.CLSCompliant#12](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/type3.vb#12)]  
  
 Tutti i tipi visualizzati nelle firme dei membri, incluso il tipo restituito di un metodo o un tipo di proprietà, devono essere conformi a CLS.  Inoltre, per i tipi generici:  
  
-   Tutti i tipi che costituiscono un tipo generico con istanze devono essere conformi a CLS.  
  
-   Tutti i tipi usati come vincoli sui parametri generici devono essere conformi a CLS.  
  
 In [Common Type System](../../docs/standard/base-types/common-type-system.md) di .NET Framework è incluso un numero di tipi incorporati supportati direttamente da Common Language Runtime, codificati in particolare nei metadati di un assembly.  Di questi tipi intrinseci, i tipi elencati nella tabella seguente sono conformi a CLS.  
  
|Tipo conforme a CLS|Descrizione|  
|-------------------------|-----------------|  
|<xref:System.Byte>|Unsigned Integer a 8 bit|  
|<xref:System.Int16>|Signed Integer a 16 bit|  
|<xref:System.Int32>|Intero con segno a 32 bit|  
|<xref:System.Int64>|Intero con segno a 64 bit|  
|<xref:System.Single>|Valore a virgola mobile e precisione singola|  
|<xref:System.Double>|Valore a virgola mobile e precisione doppia|  
|<xref:System.Boolean>|Tipo di valore `true` o `false`|  
|<xref:System.Char>|Unità di codice codificata UTF\-16|  
|<xref:System.Decimal>|Numero decimale non a virgola mobile|  
|<xref:System.IntPtr>|Puntatore o handle di una dimensione definita dalla piattaforma|  
|<xref:System.String>|Raccolta di zero, uno o più oggetti <xref:System.Char>.|  
  
 I tipi intrinseci elencati nella tabella seguente non sono conformi a CLS.  
  
|Tipo non conforme|Descrizione|Alternativa alla conformità a CLS|  
|-----------------------|-----------------|---------------------------------------|  
|<xref:System.SByte>|Tipo di dati Signed Integer a 8 bit|<xref:System.Int16>|  
|<xref:System.TypedReference>|Puntatore a un oggetto e relativo tipo di runtime|nessuno|  
|<xref:System.UInt16>|Intero senza segno a 16 bit|<xref:System.Int32>|  
|<xref:System.UInt32>|Intero senza segno a 32 bit|<xref:System.Int64>|  
|<xref:System.UInt64>|Intero senza segno a 64 bit|<xref:System.Int64> \(possibile overflow\), <xref:System.Numerics.BigInteger> o <xref:System.Double>|  
|<xref:System.UIntPtr>|Puntatore o handle senza segno|<xref:System.IntPtr>|  
  
 Nella libreria di classi .NET Framework o in qualsiasi altra libreria di classi possono essere inclusi altri tipi non conformi a CLS; ad esempio:  
  
-   Tipi di valore boxed.  Nell'esempio C\# seguente viene creata una classe con una proprietà pubblica di tipo `int*` denominata `Value`.  Poiché `int*` è un tipo di valore boxed, viene contrassegnato come non conforme a CLS dal compilatore.  
  
     [!code-csharp[Conceptual.CLSCompliant#26](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/box2.cs#26)]  
  
-   Riferimenti tipizzati, che sono costrutti speciali contenenti un riferimento a un oggetto e un riferimento a un tipo.  I riferimenti tipizzati sono rappresentati in .NET Framework dalla classe <xref:System.TypedReference>.  
  
 Se un tipo non è conforme a CLS, è necessario applicarvi l'attributo <xref:System.CLSCompliantAttribute> con un valore `isCompliant` `false`.  Per altre informazioni, vedere la sezione [Attributo CLSCompliantAttribute](#CLSAttribute).  
  
 Nell'esempio seguente viene illustrato il problema della conformità a CLS in una firma di metodo e nella creazione di un'istanza di tipo generico.  Viene definita una classe `InvoiceItem` con una proprietà di tipo <xref:System.UInt32>, una proprietà di tipo `Nullable(Of UInt32)` e un costruttore con parametri di tipo <xref:System.UInt32> e `Nullable(Of UInt32)`.  Vengono visualizzati quattro avvisi del compilatore quando si tenta di compilare l'esempio.  
  
 [!code-csharp[Conceptual.CLSCompliant#3](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/type1.cs#3)]
 [!code-vb[Conceptual.CLSCompliant#3](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/type1.vb#3)]  
  
 Per eliminare gli avvisi del compilatore, sostituire i tipi non conformi a CLS nell'interfaccia pubblica `InvoiceItem` con tipi conformi:  
  
 [!code-csharp[Conceptual.CLSCompliant#4](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/type2.cs#4)]
 [!code-vb[Conceptual.CLSCompliant#4](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/type2.vb#4)]  
  
 Oltre ai tipi specifici elencati, alcune categorie di tipi non sono conformi a CLS,  tra cui, tipi di puntatore non gestiti e tipi di puntatore a funzione.  Nell'esempio seguente viene generato un avviso del compilatore perché viene usato un puntatore a un Integer per creare una matrice di Integer.  
  
 [!code-csharp[Conceptual.CLSCompliant#5](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/unmanagedptr1.cs#5)]  
  
 Per le classi astratte conformi a CLS \(cioè quelle contrassegnate come `abstract` in C\# o come `MustInherit` in Visual Basic\), anche tutti i membri della classe devono essere conformi a CLS.  
  
<a name="naming"></a>   
### Convenzioni di denominazione  
 Poiché per alcuni linguaggi di programmazione non viene fatta distinzione tra maiuscole e minuscole, gli identificatori, ad esempio i nomi degli spazi dei nomi, i tipi e i membri, occorre che non differiscano solo per la combinazione di caratteri maiuscoli o minuscoli.  Due identificatori sono considerati equivalenti se i relativi mapping di minuscole sono uguali.  Nell'esempio di C\# seguente vengono definite due classi pubbliche, `Person` e `person`.  Poiché si differenziano solo per le maiuscole e le minuscole, dal compilatore C\# vengono contrassegnate come non conformi a CLS.  
  
 [!code-csharp[Conceptual.CLSCompliant#16](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/naming1.cs#16)]  
  
 Gli identificatori del linguaggio di programmazione, ad esempio i nomi degli spazi dei nomi, i tipi e i membri, devono essere conformi allo [standard Unicode 3.0, rapporto tecnico 15, allegato 7](http://www.unicode.org/reports/tr15/tr15-18.html).  Vale a dire che:  
  
-   Il primo carattere di un identificatore può essere qualsiasi carattere Unicode, una lettera maiuscola, una lettera minuscola, tutte iniziali maiuscole, una lettera di modificatore, un'altra lettera o un numero rappresentato dalla lettera.  Per informazioni sulle categorie di caratteri Unicode, vedere l'enumerazione <xref:System.Globalization.UnicodeCategory?displayProperty=fullName>.  
  
-   I caratteri successivi possono provenire da una qualsiasi delle categorie come primo carattere e in essi possono anche essere inclusi contrassegni senza spaziatura, contrassegni di combinazioni di spazi, numeri decimali, punteggiature del connettore e codici di formattazione.  
  
 Prima di confrontare gli identificatori, è necessario filtrare i codici di formattazione e convertire gli identificatori nel formato di normalizzazione Unicode C, poiché un singolo carattere può essere rappresentato da più unità di codice codificate UTF\-16.  Le sequenze di caratteri che producono le stesse unità di codice nel formato di normalizzazione Unicode C non sono conformi a CLS.  L'esempio seguente definisce una proprietà denominata `Å`, costituita dal carattere SEGNO di ANGSTROM \(U\+212B\) e una seconda proprietà denominata `Å`, costituita dal carattere LETTERA LATINA A MAIUSCOLA CON UN CERCHIO SOPRA \(U\+00C5\).  Sia dai compilatori C\# sia da quelli Visual Basic il codice sorgente viene contrassegnato come non conforme a CLS.  
  
 [!code-csharp[Conceptual.CLSCompliant#17](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/naming1.cs#17)]
 [!code-vb[Conceptual.CLSCompliant#17](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/naming1.vb#17)]  
  
 I nomi dei membri all'interno di un ambito specifico \(ad esempio gli spazi dei nomi in un assembly, i tipi in uno spazio dei nomi o i membri in un tipo\) devono essere univoci ad eccezione dei nomi che vengono risolti tramite l'overload.  Questo requisito è più rigido di quello di Common Type System, che consente a più membri all'interno di un ambito di disporre di nomi identici purché siano tipi diversi di membri \(ad esempio, uno è un metodo e uno è un campo\).  In particolare, per i membri di tipo:  
  
-   I campi e i tipi annidati vengono distinti solo in base al nome.  
  
-   I metodi, le proprietà e gli eventi che hanno lo stesso nome devono presentare differenze che vanno oltre il solo tipo restituito.  
  
 Nell'esempio seguente viene illustrato il requisito in base al quale i nomi dei membri devono essere univoci all'interno del relativo ambito.  Viene definita una classe denominata `Converter` in cui sono inclusi quattro membri denominati `Conversion`.  Tre sono metodi e uno è una proprietà.  Il metodo che prevede un parametro <xref:System.Int64> è denominato in modo univoco, ma i due metodi con un parametro <xref:System.Int32> non lo sono, poiché il valore restituito non è considerato parte della firma di un membro.  Questo requisito viene violato anche dalla proprietà `Conversion`, poiché le proprietà non possono disporre dello stesso nome dei metodi di overload.  
  
 [!code-csharp[Conceptual.CLSCompliant#19](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/naming3.cs#19)]
 [!code-vb[Conceptual.CLSCompliant#19](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/naming3.vb#19)]  
  
 Nei singoli linguaggi sono incluse parole chiave univoche, pertanto i linguaggi destinati a Common Language Runtime devono fornire anche un meccanismo di riferimento agli identificatori \(ad esempio nomi di tipi\) che coincidono con le parole chiave.  Ad esempio, `case` è una parola chiave sia in C\# sia in Visual Basic.  Tuttavia, nell'esempio di Visual Basic seguente è possibile evitare ambiguità relative a una classe denominata `case` dalla parola chiave `case` usando le parentesi graffe di apertura e chiusura.  In caso contrario, nell'esempio verrà generato il messaggio di errore "Parola chiave non valida come identificatore" e la compilazione non verrà completata.  
  
 [!code-vb[Conceptual.CLSCompliant#22](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/keyword1.vb#22)]  
  
 Nell'esempio di C\# seguente è possibile creare un'istanza della classe `case` usando il simbolo `@` per evitare ambiguità nell'identificatore della parola chiave del linguaggio.  Senza, tramite il compilatore C\# verrebbero visualizzati due messaggi di errore, "È previsto un tipo" e "'case' è un termine non valido nell'espressione".  
  
 [!code-csharp[Conceptual.CLSCompliant#23](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/keyword2.cs#23)]  
  
<a name="conversion"></a>   
### Conversione di tipi  
 Tramite le specifiche CLS \(Common Language Specification\) vengono definiti due operatori di conversione:  
  
-   `op_Implicit`, che viene usato per le conversioni verso un tipo di dati più grande che non comportano la perdita di dati o di precisione.  Ad esempio, nella struttura <xref:System.Decimal> è incluso un operatore `op_Implicit` di overload per convertire i valori di tipi integrali e i valori <xref:System.Char> in valori <xref:System.Decimal>.  
  
-   `op_Explicit`, che viene usato per le conversioni verso un tipo di dati più piccolo che possono comportare la perdita di grandezza \(un valore viene convertito in un altro a cui è associato un intervallo inferiore\) o di precisione.  Ad esempio, nella struttura <xref:System.Decimal> è incluso un operatore `op_Explicit` di overload per convertire i valori <xref:System.Double> e <xref:System.Single> in <xref:System.Decimal> e per convertire i valori <xref:System.Decimal> in valori integrali <xref:System.Double>, <xref:System.Single> e <xref:System.Char>.  
  
 Tuttavia, non tutti i linguaggi supportano l'overload degli operatori o la definizione di operatori personalizzati.  Se si sceglie di implementare questi operatori di conversione, è necessario fornire anche un modo alternativo per eseguire la conversione.  È consigliabile fornire i metodi `From`*Xxx* e `To`*Xxx*.  
  
 Nell'esempio seguente vengono definite le convenzioni esplicite e implicite conformi a CLS.  Viene creata una classe `UDouble` che rappresenta un numero a virgola mobile e precisione doppia con segno.  Viene usato per le conversioni implicite da `UDouble` a <xref:System.Double> e per le conversioni esplicite da `UDouble` a <xref:System.Single>, da <xref:System.Double> a `UDouble` e da <xref:System.Single> a `UDouble`.  Vengono anche definiti un metodo `ToDouble` come alternativa all'operatore di conversione implicito e i metodi `ToSingle`, `FromDouble` e `FromSingle` come alternative agli operatori di conversione espliciti.  
  
 [!code-csharp[Conceptual.CLSCompliant#15](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/convert1.cs#15)]
 [!code-vb[Conceptual.CLSCompliant#15](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/convert1.vb#15)]  
  
<a name="arrays"></a>   
### Matrici  
 Le matrici conformi a CLS sono conformi alle regole seguenti:  
  
-   Il limite inferiore di tutte le dimensioni di una matrice deve essere uguale a zero.  Nell'esempio seguente viene creata una matrice non conforme a CLS con un limite inferiore pari a uno.  Si noti che, nonostante la presenza dell'attributo <xref:System.CLSCompliantAttribute>, tramite il compilatore non viene rilevato che la matrice restituita dal metodo `Numbers.GetTenPrimes` non è conforme a CLS.  
  
     [!code-csharp[Conceptual.CLSCompliant#8](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/array1.cs#8)]
     [!code-vb[Conceptual.CLSCompliant#8](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/array1.vb#8)]  
  
-   Tutti gli elementi delle matrici devono essere costituiti da tipi conformi a CLS.  Nell'esempio seguente vengono definiti due metodi tramite cui vengono restituite matrici non conformi a CLS.  Tramite il primo viene restituita una matrice di valori <xref:System.UInt32>.  Tramite il secondo viene restituita una matrice <xref:System.Object> in cui sono inclusi i valori <xref:System.Int32> e <xref:System.UInt32>.  Anche se il compilatore consente di identificare la prima matrice come non conforme a causa del relativo tipo <xref:System.UInt32>, non è in grado di riconoscere che nella seconda matrice sono inclusi elementi non conformi a CLS.  
  
     [!code-csharp[Conceptual.CLSCompliant#9](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/array2.cs#9)]
     [!code-vb[Conceptual.CLSCompliant#9](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/array2.vb#9)]  
  
-   La risoluzione dell'overload per i metodi a cui sono associati parametri di matrice è basata sul fatto che si tratta di matrici e sul relativo tipo di elemento.  Per questo motivo, la seguente definizione di un metodo `GetSquares` di overload è conforme a CLS.  
  
     [!code-csharp[Conceptual.CLSCompliant#10](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/array3.cs#10)]
     [!code-vb[Conceptual.CLSCompliant#10](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/array3.vb#10)]  
  
<a name="Interfaces"></a>   
### Interfacce  
 Tramite interfacce conformi a CLS è possibile definire proprietà, eventi e metodi virtuali \(metodi senza l'implementazione\).  Un'interfaccia conforme a CLS non può disporre di uno dei seguenti valori:  
  
-   Metodi o campi statici.  Sia tramite i compilatori C\# sia tramite quelli Visual Basic vengono generati errori del compilatore se si definisce un membro statico in un'interfaccia.  
  
-   Campi.  Sia tramite i compilatori C\# sia tramite quelli Visual Basic vengono generati errori del compilatore se si definisce un campo in un'interfaccia.  
  
-   Metodi non conformi a CLS.  Ad esempio, nella definizione dell'interfaccia seguente è incluso un metodo, `INumber.GetUnsigned`, che è contrassegnato come non conforme a CLS.  In questo esempio verrà generato un avviso del compilatore.  
  
     [!code-csharp[Conceptual.CLSCompliant#6](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/interface2.cs#6)]
     [!code-vb[Conceptual.CLSCompliant#6](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/interface2.vb#6)]  
  
     A causa di questa regola, i tipi conformi a CLS non sono necessari per l'implementazione di membri non conformi a CLS.  Se tramite un framework conforme a CLS viene esposta una classe mediante la quale viene implementata un'interfaccia non conforme a CLS, è anche consigliabile fornire implementazioni concrete di tutti i membri non conformi a CLS.  
  
 I compilatori di linguaggi conformi a CLS devono anche consentire a una classe di fornire implementazioni separate di membri con lo stesso nome e la stessa firma in più interfacce.  Sia C\# sia Visual Basic supportano [implementazioni di interfacce esplicite](../Topic/Explicit%20Interface%20Implementation%20\(C%23%20Programming%20Guide\).md) per fornire diverse implementazioni di metodi denominati in modo identico.  Visual Basic supporta anche la parola chiave `Implements`, che consente di definire in modo esplicito l'interfaccia e il membro tramite cui viene implementato un particolare membro.  Nell'esempio seguente viene illustrato questo scenario definendo una classe `Temperature` mediante la quale vengono implementate le interfacce `ICelsius` e `IFahrenheit` come implementazioni di interfacce esplicite.  
  
 [!code-csharp[Conceptual.CLSCompliant#24](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/eii1.cs#24)]
 [!code-vb[Conceptual.CLSCompliant#24](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/eii1.vb#24)]  
  
<a name="enums"></a>   
### Enumerazioni  
 Le enumerazioni conformi a CLS devono rispettare queste regole:  
  
-   Il tipo sottostante dell'enumerazione deve essere un Integer intrinseco conforme a CLS \(<xref:System.Byte>, <xref:System.Int16>, <xref:System.Int32> o <xref:System.Int64>\).  Ad esempio, tramite il codice seguente viene eseguito il tentativo di definizione di un'enumerazione il cui tipo sottostante è <xref:System.UInt32> e viene generato un avviso del compilatore.  
  
     [!code-csharp[Conceptual.CLSCompliant#7](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/enum3.cs#7)]
     [!code-vb[Conceptual.CLSCompliant#7](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/enum3.vb#7)]  
  
-   Un tipo di enumerazione deve avere un singolo campo di istanza denominato `Value__` contrassegnato con l'attributo <xref:System.Reflection.FieldAttributes?displayProperty=fullName>.  Ciò consente di fare riferimento al valore del campo in modo implicito.  
  
-   Un'enumerazione prevede campi statici con valori letterali i cui tipi corrispondono al tipo dell'enumerazione stessa.  Ad esempio, se si definisce un'enumerazione `State` con valori `State.On` e `State.Off`, `State.On` e `State.Off` sono entrambi campi statici con valori letterali il cui tipo è `State`.  
  
-   Vi sono due tipi di enumerazioni:  
  
    -   Enumerazione che rappresenta un set di Integer denominati che si escludono a vicenda.  Questo tipo di enumerazione è indicato dall'assenza dell'attributo personalizzato <xref:System.FlagsAttribute?displayProperty=fullName>.  
  
    -   Enumerazione che rappresenta un set di flag di bit che possono essere combinati per generare un valore senza nome.  Questo tipo di enumerazione è indicato dalla presenza dell'attributo personalizzato <xref:System.FlagsAttribute?displayProperty=fullName>.  
  
     Per altre informazioni, vedere la documentazione relativa alla struttura <xref:System.Enum>.  
  
-   Il valore di un'enumerazione non è limitato all'intervallo dei relativi valori specificati.  In altre parole, l'intervallo di valori in una enumerazione è l'intervallo del relativo valore sottostante.  È possibile usare il metodo <xref:System.Enum.IsDefined%2A?displayProperty=fullName> per determinare se un valore specificato è un membro di un'enumerazione.  
  
<a name="members"></a>   
### Membri dei tipi in generale  
 In base alle specifiche CLS \(Common Language Specification\), l'accesso a tutti i campi e metodi deve essere effettuato come membri di una classe particolare.  Pertanto, i campi e i metodi statici globali, vale a dire campi o metodi statici definiti oltre a un tipo, non sono conformi a CLS.  Se si tenta di includere un campo o un metodo globale nel codice sorgente, viene generato un errore del compilatore sia dai compilatori C\# sia da quelli Visual Basic.  
  
 Le specifiche CLS \(Common Language Specification\) supportano solo la convenzione di chiamata gestita standard.  Non supportano le convenzioni di chiamata non gestite né i metodi con elenchi di argomenti variabili contrassegnati con la parola chiave `varargs`.  Per gli elenchi di argomenti variabili compatibili con la convenzione di chiamata gestita standard, usare l'attributo <xref:System.ParamArrayAttribute> o l'implementazione del singolo linguaggio, ad esempio la parola chiave `params` in C\# e la parola chiave `ParamArray` in Visual Basic.  
  
<a name="MemberAccess"></a>   
### Accessibilità del membro  
 Tramite l'override di un membro ereditato non è possibile modificare l'accessibilità del membro in questione.  Ad esempio, un metodo pubblico in una classe di base non può essere sottoposto a override da un metodo privato in una classe derivata.  Vi è un'eccezione: un membro `protected internal` \(in C\#\) o `Protected Friend` \(in Visual Basic\) in un assembly sottoposto a override da un tipo in un assembly diverso.  In questo caso, l'accessibilità dell'override è `Protected`.  
  
 Nell'esempio seguente viene illustrato l'errore generato quando l'attributo <xref:System.CLSCompliantAttribute> è impostato su `true` e tramite `Person`, cioè una classe derivata da `Animal`, si tenta di modificare l'accessibilità della proprietà `Species` da pubblica a privata.  L'esempio viene compilato correttamente se la relativa accessibilità è stata modificata in pubblica.  
  
 [!code-csharp[Conceptual.CLSCompliant#28](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/accessibility1.cs#28)]
 [!code-vb[Conceptual.CLSCompliant#28](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/accessibility1.vb#28)]  
  
 I tipi nella firma di un membro devono essere accessibili ogni volta che il membro è accessibile.  Ciò significa, ad esempio, che in un membro pubblico non può essere incluso un parametro il cui tipo è privato, protetto o interno.  Nell'esempio seguente viene illustrato l'errore del compilatore generato quando tramite un costruttore di classe `StringWrapper` viene esposto un valore di enumerazione `StringOperationType` interno con cui si determina la modalità di esecuzione del wrapping di un valore stringa.  
  
 [!code-csharp[Conceptual.CLSCompliant#27](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/accessibility3.cs#27)]
 [!code-vb[Conceptual.CLSCompliant#27](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/accessibility3.vb#27)]  
  
<a name="Generics"></a>   
### Tipi e membri generici  
 I tipi annidati dispongono sempre di un numero di parametri generici almeno pari a quelli del relativo tipo di inclusione.  Questi corrispondono per posizione ai parametri generici del tipo di inclusione.  Il tipo generico può anche prevedere nuovi parametri generici.  
  
 La relazione tra i parametri di tipo generico di un tipo contenitore e i relativi tipi annidati può essere nascosta dalla sintassi dei singoli linguaggi.  Nell'esempio seguente in un tipo generico `Outer<T>` sono contenute due classi annidate, `Inner1A` e `Inner1B<U>`.  Con le chiamate al metodo `ToString`, che ogni classe eredita da <xref:System.Object.ToString%2A?displayProperty=fullName>, viene mostrato che in ogni classe annidata sono inclusi i parametri di tipo della relativa classe che li contiene.  
  
 [!code-csharp[Conceptual.CLSCompliant#29](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/nestedgenerics2.cs#29)]
 [!code-vb[Conceptual.CLSCompliant#29](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/nestedgenerics2.vb#29)]  
  
 I nomi di tipo generico sono codificati nel formato *name*```*n*, dove *name* è il nome del tipo, ``` è un valore letterale del carattere e *n* è il numero di parametri dichiarati nel tipo oppure, per i tipi generici annidati, il numero di parametri del tipo appena introdotti.  Questa codifica dei nomi di tipo generico è principalmente di interesse per gli sviluppatori che usano la reflection per accedere ai tipi generici conformi a CLS in una libreria.  
  
 Se i vincoli vengono applicati a un tipo generico, anche tutti i tipi usati come vincoli devono essere conformi a CLS.  Nell'esempio seguente viene definita una classe denominata `BaseClass` che non è conforme a CLS e una classe generica denominata `BaseCollection` il cui parametro di tipo deve derivare da `BaseClass`.  Tuttavia, poiché `BaseClass` non è conforme a CLS, viene generato un avviso dal compilatore.  
  
 [!code-csharp[Conceptual.CLSCompliant#34](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics5.cs#34)]
 [!code-vb[Conceptual.CLSCompliant#34](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics5.vb#34)]  
  
 Se un tipo generico è derivato da un tipo base generico, è necessario dichiarare nuovamente tutti i vincoli in modo che sia possibile garantire che vengano soddisfatti anche i vincoli sul tipo base.  Nell'esempio riportato di seguito viene definito un oggetto `Number<T>` che può rappresentare qualsiasi tipo numerico.  Viene anche definita una classe `FloatingPoint<T>` che rappresenta un valore a virgola mobile.  Tuttavia, il codice sorgente non viene compilato, perché non viene applicato il vincolo su `Number<T>` \(che T deve essere un tipo di valore\) a `FloatingPoint<T>`.  
  
 [!code-csharp[Conceptual.CLSCompliant#30](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics2a.cs#30)]
 [!code-vb[Conceptual.CLSCompliant#30](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics2a.vb#30)]  
  
 L'esempio viene compilato correttamente se il vincolo viene aggiunto alla classe `FloatingPoint<T>`.  
  
 [!code-csharp[Conceptual.CLSCompliant#31](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics2.cs#31)]
 [!code-vb[Conceptual.CLSCompliant#31](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics2.vb#31)]  
  
 Le specifiche CLS \(Common Language Specification\) impongono un modello conservativo per creazione di istanze per tipi annidati e membri protetti.  Tramite i tipi generici aperti non è possibile esporre campi o membri con firme contenenti la creazione di un'istanza specifica di un tipo generico annidato e protetto.  Tramite i tipi non generici, mediante i quali viene estesa la creazione di un'istanza specifica di un'interfaccia o di una classe di base generica, non è possibile esporre i campi o i membri con firme contenenti la creazione di un'istanza differente di un tipo generico annidato e protetto.  
  
 Nell'esempio seguente vengono definiti un tipo generico, `C1<T>` \(o `C1(Of T)` in Visual Basic\) e una classe protetta, `C1<T>.N` \(o `C1(Of T).N` in Visual Basic\).  L'oggetto `C1<T>` dispone di due metodi: `M1` e `M2`.  Tuttavia, `M1` non è conforme a CLS poiché tramite esso si tenta di restituire un oggetto `C1<int>.N` \(o `C1(Of Integer).N`\) da C1\<T\> \(o `C1(Of T)`\).  Una seconda classe, `C2`, viene derivata da `C1<long>` \(o `C1(Of Long)`\).  Dispone di due metodi, `M3` e `M4`.  `M3` non è conforme a CLS poiché viene eseguito il tentativo di restituzione di un oggetto `C1<int>.N` \(o `C1(Of Integer).N`\) da una sottoclasse di `C1<long>`.  Si noti che i compilatori di linguaggio possono essere anche più restrittivi.  In questo esempio in Visual Basic viene visualizzato un errore quando viene eseguito un tentativo di compilazione di `M4`.  
  
 [!code-csharp[Conceptual.CLSCompliant#32](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/generics4.cs#32)]
 [!code-vb[Conceptual.CLSCompliant#32](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/generics4.vb#32)]  
  
<a name="ctors"></a>   
### Costruttori  
 I costruttori nelle classi e strutture conformi a CLS devono rispettare queste regole:  
  
-   Prima di accedere ai dati di istanza ereditati, un costruttore di una classe derivata deve chiamare il costruttore di istanze della relativa classe di base.  Questo requisito è dovuto al fatto che i costruttori della classe di base non vengono ereditati dalle classi derivate.  Questa regola non si applica alle strutture, che non supportano l'ereditarietà diretta.  
  
     In genere, questa regola viene applicata dai compilatori indipendentemente dalla conformità a CLS, come illustrato dall'esempio riportato di seguito.  Viene creata una classe `Doctor` derivata da una classe `Person`, ma la classe `Doctor` non riuscirà a chiamare il costruttore della classe `Person` per inizializzare i campi di istanza ereditati.  
  
     [!code-csharp[Conceptual.CLSCompliant#11](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/ctor1.cs#11)]
     [!code-vb[Conceptual.CLSCompliant#11](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/ctor1.vb#11)]  
  
-   Il costruttore di un oggetto non può essere chiamato tranne che per creare un oggetto.  Inoltre, un oggetto non può essere inizializzato due volte.  Ciò significa, ad esempio, che tramite i metodi <xref:System.Object.MemberwiseClone%2A?displayProperty=fullName> e di deserializzazione come <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=fullName> non devono essere chiamati i costruttori.  
  
<a name="properties"></a>   
### Proprietà  
 Le proprietà nei tipi conformi a CLS devono rispettare queste regole:  
  
-   Una proprietà deve disporre di un metodo Set, un metodo Get o di entrambi.  In un assembly questi vengono implementati come metodi speciali, ovvero vengono visualizzati come metodi separati \(getter è denominato `get_`*nomeproprietà* e setter è `set_`*nomeproprietà*\) contrassegnati come `SpecialName` nei metadati dell'assembly.  Tramite i compilatori C\# e Visual Basic questa regola viene applicata automaticamente senza la necessità di usare l'attributo <xref:System.CLSCompliantAttribute>.  
  
-   Un tipo di proprietà è il tipo restituito del metodo Get della proprietà e l'ultimo argomento del metodo Set.  È necessario che questi tipi siano conformi a CLS e gli argomenti non possono essere assegnati alla proprietà per riferimento, cioè non possono essere puntatori gestiti.  
  
-   Se una proprietà dispone dei metodi Get e Set, essi devono essere entrambi virtuali, statici o istanze.  Dai compilatori C\# e Visual Basic questa regola viene applicata automaticamente tramite la relativa sintassi di definizione della proprietà.  
  
<a name="events"></a>   
### Eventi  
 Un evento viene definito in base al nome e al relativo tipo.  Il tipo di evento è un delegato che viene usato per indicare l'evento.  Ad esempio, l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> è di tipo <xref:System.ResolveEventHandler>.  Oltre all'evento stesso, vi sono tre metodi con nomi basati sul nome di evento che forniscono l'implementazione dell'evento e sono contrassegnati come `SpecialName` nei metadati dell'assembly:  
  
-   Un metodo per l'aggiunta di un gestore eventi, denominato `add_`*EventName*.  Ad esempio, il metodo di sottoscrizione evento per l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> è denominato `add_AssemblyResolve`.  
  
-   Un metodo per la rimozione di un gestore eventi, denominato `remove_`*EventName*.  Ad esempio, il metodo di rimozione per l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> è denominato `remove_AssemblyResolve`.  
  
-   Un metodo per indicare che si è verificato l'evento, denominato `raise_`*EventName*.  
  
> [!NOTE]
>  La maggior parte delle regole di Common Language Specification relative agli eventi viene implementata dai compilatori di linguaggi e risulta trasparente agli sviluppatori di componenti.  
  
 I metodi per l'aggiunta, la rimozione e la generazione di eventi devono avere la stessa accessibilità.  Devono anche essere tutti statici, istanze o virtuali.  I metodi per l'aggiunta e la rimozione di un evento dispongono di un parametro il cui tipo è il tipo delegato di evento.  I metodi di aggiunta e rimozione devono essere entrambi presenti o entrambi assenti.  
  
 Nell'esempio seguente viene definita una classe conforme a CLS denominata `Temperature` tramite cui viene generato un evento `TemperatureChanged` se la modifica nella temperatura tra due letture è uguale o maggiore di un valore soglia.  Tramite la classe `Temperature` viene definito in modo esplicito un metodo `raise_TemperatureChanged` in modo che tramite esso sia possibile eseguire selettivamente i gestori eventi.  
  
 [!code-csharp[Conceptual.CLSCompliant#20](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/event1.cs#20)]
 [!code-vb[Conceptual.CLSCompliant#20](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/event1.vb#20)]  
  
<a name="overloads"></a>   
### Overloads  
 Le specifiche CLS \(Common Language Specification\) impongono i requisiti seguenti sui membri di overload:  
  
-   I membri possono essere sottoposti a overload in base al numero di parametri e al tipo di qualsiasi parametro.  La convenzione di chiamata, il tipo restituito, i modificatori personalizzati applicati al metodo o al relativo parametro e se i parametri vengono passati per valore o per riferimento vengono ignorati quando viene fatta distinzione tra gli overload.  Per un esempio, vedere il codice per il requisito in cui viene richiesto che i nomi siano univoci all'interno di un ambito nella sezione [Convenzioni di denominazione](#naming).  
  
-   È possibile eseguire l'overload solo di proprietà e metodi.  Non è possibile eseguire l'overload di campi ed eventi.  
  
-   I metodi generici possono essere sottoposti a overload in base al numero dei relativi parametri generici.  
  
> [!NOTE]
>  Gli operatori `op_Explicit` e `op_Implicit` sono eccezioni alla regola che il valore restituito non viene considerato parte di una firma del metodo per risoluzione dell'overload.  Questi due operatori possono essere sottoposti a overload in base ai relativi parametri e al relativo valore restituito.  
  
<a name="exceptions"></a>   
### Eccezioni  
 Gli oggetti eccezione devono derivare da <xref:System.Exception?displayProperty=fullName> o da un altro tipo derivato da <xref:System.Exception?displayProperty=fullName>.  Nell'esempio seguente viene illustrato l'errore del compilatore generato quando una classe personalizzata denominata `ErrorClass` viene usata per la gestione delle eccezioni.  
  
 [!code-csharp[Conceptual.CLSCompliant#13](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/exceptions1.cs#13)]
 [!code-vb[Conceptual.CLSCompliant#13](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/exceptions1.vb#13)]  
  
 Per correggere questo errore, la classe `ErrorClass` deve ereditare da <xref:System.Exception?displayProperty=fullName>.  Inoltre, la proprietà `Message` deve essere sottoposta a override.  Nell'esempio riportato di seguito questi errori vengono corretti per definire una classe `ErrorClass` che è conforme a CLS.  
  
 [!code-csharp[Conceptual.CLSCompliant#14](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/exceptions2.cs#14)]
 [!code-vb[Conceptual.CLSCompliant#14](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/exceptions2.vb#14)]  
  
<a name="attributes"></a>   
### Attributi  
 Negli assembly .NET Framework, gli attributi personalizzati forniscono un meccanismo estensibile per archiviare gli attributi personalizzati e recuperare i metadati sugli oggetti di programmazione, ad esempio assembly, tipi, membri e parametri di metodo.  Gli attributi personalizzati devono derivare da <xref:System.Attribute?displayProperty=fullName> o da un tipo derivato da <xref:System.Attribute?displayProperty=fullName>.  
  
 Nell'esempio riportato di seguito viene violata questa regola.  Viene definita una classe `NumericAttribute` che non deriva da <xref:System.Attribute?displayProperty=fullName>.  Si noti che un errore del compilatore viene visualizzato solo quando viene applicato l'attributo non conforme a CLS, non quando la classe è definita.  
  
 [!code-csharp[Conceptual.CLSCompliant#18](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/attribute1.cs#18)]
 [!code-vb[Conceptual.CLSCompliant#18](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/attribute1.vb#18)]  
  
 Tramite il costruttore o le proprietà di un attributo conforme a CLS possono essere esposti solo i tipi seguenti:  
  
-   <xref:System.Boolean>  
  
-   <xref:System.Byte>  
  
-   <xref:System.Char>  
  
-   <xref:System.Double>  
  
-   <xref:System.Int16>  
  
-   <xref:System.Int32>  
  
-   <xref:System.Int64>  
  
-   <xref:System.Single>  
  
-   <xref:System.String>  
  
-   <xref:System.Type>  
  
-   Qualsiasi tipo di enumerazione il cui tipo sottostante è <xref:System.Byte>, <xref:System.Int16>, <xref:System.Int32> o <xref:System.Int64>.  
  
 Nell'esempio seguente viene definita una `DescriptionAttribute` classe che deriva da <xref:System.Attribute>.  Il costruttore di classe dispone di un parametro di tipo `Descriptor`, pertanto la classe non è conforme a CLS.  Si noti che tramite il compilatore C\# viene generato un avviso ma l'operazione di compilazione viene eseguita correttamente, mentre tramite il compilatore Visual Basic non vengono generati né avvisi, né errori.  
  
 [!code-csharp[Conceptual.CLSCompliant#33](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/attribute2.cs#33)]
 [!code-vb[Conceptual.CLSCompliant#33](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/attribute2.vb#33)]  
  
<a name="CLSAttribute"></a>   
## Attributo CLSCompliantAttribute  
 L'attributo <xref:System.CLSCompliantAttribute> è usato per indicare se un elemento del programma è conforme a CLS \(Common Language Specification\).  Nel costruttore <xref:System.CLSCompliantAttribute.%23ctor%28System.Boolean%29?displayProperty=fullName> è incluso un solo parametro obbligatorio, `isCompliant`, che indica se l'elemento del programma è conforme a CLS.  
  
 In fase di compilazione, tramite il compilatore vengono rilevati gli elementi non conformi che si presuppone siano conformi a CLS e viene generato un avviso.  Tramite il compilatore non vengono generati avvisi per i tipi o i membri che vengono dichiarati esplicitamente come non conformi.  
  
 Gli sviluppatori di componenti possono usare l'attributo <xref:System.CLSCompliantAttribute> in due modi:  
  
-   Per definire le parti dell'interfaccia pubblica esposte da un componente che sono conformi a CLS e le parti che non sono conformi a CLS.  Quando l'attributo viene usato per contrassegnare determinati elementi del programma come conformi a CLS, il relativo uso garantisce che gli elementi sono accessibili da tutti i linguaggi e strumenti destinati a .NET Framework.  
  
-   Per assicurarsi che tramite l'interfaccia pubblica della libreria componenti vengano esposti solo elementi del programma che sono conformi a CLS.  Se gli elementi non sono conformi a CLS, tramite i compilatori viene di solito generato un avviso.  
  
> [!WARNING]
>  In alcuni casi, dai compilatori di linguaggio vengono applicate regole conformi a CLS indipendentemente dal fatto che l'attributo <xref:System.CLSCompliantAttribute> venga usato.  Ad esempio, con la definizione di un membro statico in un'interfaccia viene violata una regola CLS.  Tuttavia, se si definisce un membro `static` \(in C\#\) o `Shared` \(in Visual Basic\) in un'interfaccia, tramite i compilatori C\# e Visual Basic viene visualizzato un messaggio di errore e l'applicazione non viene compilata.  
  
 L'attributo <xref:System.CLSCompliantAttribute> è contrassegnato con un attributo <xref:System.AttributeUsageAttribute> con un valore pari a <xref:System.AttributeTargets?displayProperty=fullName>.  Con questo valore è possibile applicare l'attributo <xref:System.CLSCompliantAttribute> a qualsiasi elemento del programma, tra cui assembly, moduli, tipi \(classi, strutture, enumerazioni, interfacce e delegati\), membri di tipo \(costruttori, metodi, proprietà, campi ed eventi\), parametri, parametri generici e valori restituiti.  Tuttavia, in pratica, è consigliabile applicare l'attributo solo agli assembly, ai tipi e ai membri di tipo.  In caso contrario, tramite i compilatori viene ignorato l'attributo e viene continuata la generazione di avvisi del compilatore ogni volta che viene rilevato un parametro non conforme, un parametro generico o un valore restituito nell'interfaccia pubblica della libreria.  
  
 Il valore dell'attributo <xref:System.CLSCompliantAttribute> viene ereditato dagli elementi del programma contenuti.  Ad esempio, se un assembly è contrassegnato come conforme a CLS, anche i relativi tipi sono conformi a CLS.  Se un tipo è contrassegnato come conforme a CLS, anche i relativi membri e tipi annidati sono conformi a CLS.  
  
 È possibile eseguire l'override in modo esplicito della conformità ereditata applicando l'attributo <xref:System.CLSCompliantAttribute> a un elemento del programma contenuto.  Ad esempio, è possibile usare l'attributo <xref:System.CLSCompliantAttribute> con un valore `isCompliant` `false` per definire un tipo non conforme in un assembly conforme e l'attributo con un valore `isCompliant` `true` per definire un tipo conforme in un assembly non conforme.  È anche possibile definire i membri non conformi in un tipo conforme.  Tuttavia, in un tipo non conforme non possono essere inclusi membri conformi, pertanto non è possibile usare l'attributo con un valore `isCompliant` `true` per eseguire l'override dell'ereditarietà da un tipo non conforme.  
  
 Quando si sviluppano componenti, è sempre consigliabile usare l'attributo <xref:System.CLSCompliantAttribute> per indicare se l'assembly e i relativi tipi e membri sono conformi a CLS.  
  
 Per creare componenti conformi a CLS:  
  
1.  Usare l'oggetto <xref:System.CLSCompliantAttribute> per contrassegnare l'assembly come conforme a CLS.  
  
2.  Contrassegnare tutti i tipi esposti pubblicamente nell'assembly che non sono conformi a CLS come non conformi.  
  
3.  Contrassegnare tutti i membri esposti pubblicamente in tipi conformi a CLS come non conformi.  
  
4.  Fornire un'alternativa conforme a CLS per i membri non conformi a CLS.  
  
 Se sono stati contrassegnati correttamente tutti i tipi e i membri non conformi, tramite il compilatore non vengono generati avvisi di mancata conformità.  Tuttavia, è consigliabile indicare i membri che non sono conformi a CLS ed elencare le alternative conformi a CLS nella documentazione del prodotto.  
  
 Nell'esempio seguente viene usato l'attributo <xref:System.CLSCompliantAttribute> per definire un assembly conforme a CLS e un tipo, `CharacterUtilities`, contenente due membri non conformi a CLS.  Poiché entrambi i membri sono contrassegnati con l'attributo `CLSCompliant(false)`, non vengono generati avvisi dal compilatore.  La classe fornisce anche un'alternativa conforme a CLS per entrambi i metodi.  In genere, si aggiungono solo due overload al metodo `ToUTF16` per fornire alternative conformi a CLS.  Tuttavia, poiché i metodi non possono essere sottoposti a overload in base al valore restituito, i nomi dei metodi conformi a CLS sono diversi da quelli dei metodi non conformi.  
  
 [!code-csharp[Conceptual.CLSCompliant#35](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.clscompliant/cs/indicator3.cs#35)]
 [!code-vb[Conceptual.CLSCompliant#35](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.clscompliant/vb/indicator3.vb#35)]  
  
 Se si sta sviluppando un'applicazione anziché una libreria \(cioè se non si stanno esponendo tipi o membri che possono essere usati da altri sviluppatori dell'applicazione\), la conformità a CLS degli elementi del programma usati dall'applicazione è importante solo se il linguaggio non li supporta.  In questo caso, tramite il compilatore di linguaggio verrà generato un errore quando si tenta di usare un elemento non conforme a CLS.  
  
<a name="CrossLang"></a>   
## Interoperabilità tra linguaggi diversi  
 L'indipendenza del linguaggio ha numerosi significati possibili.  Un significato, illustrato nell'articolo [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../docs/standard/language-independence-and-language-independent-components.md), riguarda l'utilizzo semplice dei tipi scritti in un linguaggio da parte di un'applicazione scritta in un linguaggio diverso.  Un secondo significato, che è il fulcro di questo articolo, riguarda la combinazione di codice scritto in più linguaggi in un unico assembly .NET Framework.  
  
 L'esempio seguente illustra l'interoperabilità tra linguaggi mediante la creazione di una libreria di classi denominata Utilities.dll che comprende due classi, `NumericLib` e `StringLib`.  La classe `NumericLib` è scritta in C\# e la classe `StringLib` in Visual Basic.  Di seguito è riportato il codice sorgente per StringUtil.vb in cui è incluso un singolo membro, `ToTitleCase`, nella classe `StringLib`.  
  
 [!code-vb[Conceptual.CrossLanguage#1](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.crosslanguage/vb/stringutil.vb#1)]  
  
 Di seguito è riportato il codice sorgente per NumberUtil.cs tramite cui viene definita una classe `NumericLib` in cui sono contenuti due membri, `IsEven` e `NearZero`.  
  
 [!code-csharp[Conceptual.CrossLanguage#2](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.crosslanguage/cs/numberutil.cs#2)]  
  
 Per includere le due classi in un singolo assembly, è necessario compilarle in moduli.  Per compilare il file di codice sorgente di Visual Basic in un modulo, usare il comando seguente:  
  
```  
vbc /t:module StringUtil.vb   
```  
  
 Per altre informazioni sulla sintassi della riga di comando del compilatore Visual Basic, vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md).  
  
 Per compilare il file di codice sorgente di C\# in un modulo, usare il comando seguente:  
  
```  
csc /t:module NumberUtil.cs  
```  
  
 Per altre informazioni sulla sintassi della riga di comando del compilatore C\#, vedere [Compilazione dalla riga di comando con csc.exe](../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  
  
 Usare quindi lo [strumento Link \(Link.exe\)](../Topic/Linker%20Options.md) per compilare i due moduli in un assembly:  
  
```  
link numberutil.netmodule stringutil.netmodule /out:UtilityLib.dll /dll   
```  
  
 L'esempio seguente chiama quindi i metodi `NumericLib.NearZero` e `StringLib.ToTitleCase`.  Sia il codice Visual Basic che il codice C\# sono in grado di accedere ai metodi in entrambe le classi.  
  
 [!code-csharp[Conceptual.CrossLanguage#3](../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.crosslanguage/cs/useutilities1.cs#3)]
 [!code-vb[Conceptual.CrossLanguage#3](../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.crosslanguage/vb/useutilities1.vb#3)]  
  
 Per compilare il codice Visual Basic, usare il comando seguente:  
  
```  
vbc example.vb /r:UtilityLib.dll  
```  
  
 Per compilare con C\#, modificare il nome del compilatore da **vbc** a **csc** e modificare l'estensione del file da VB a CS:  
  
```  
csc example.cs /r:UtilityLib.dll  
```  
  
## Vedere anche  
 <xref:System.CLSCompliantAttribute>