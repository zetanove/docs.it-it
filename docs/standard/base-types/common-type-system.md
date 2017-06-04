---
title: "Common Type System | Microsoft Docs"
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
  - "assembly [.NET Framework], tipi"
  - "Common Type System"
  - "interoperabilità tra linguaggi diversi"
  - "spazi dei nomi [.NET Framework], tipi"
  - "tipi di riferimento"
  - "type system"
  - "tipi, informazioni"
  - "tipi di valori"
ms.assetid: 53c57c96-83e1-4ee3-9543-9ac832671a89
caps.latest.revision: 25
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Common Type System
Common Type System definisce le modalità di dichiarazione, utilizzo e gestione dei tipi in Common Language Runtime e rappresenta una parte importante del supporto runtime per l'integrazione di più linguaggi.  Le funzioni assolte dal sistema di tipi comuni sono le seguenti:  
  
-   Definire un framework che consenta l'integrazione di più linguaggi, l'indipendenza dai tipi e l'esecuzione di codice con prestazioni elevate.  
  
-   Fornire un modello orientato a oggetti che supporta l'implementazione completa di molti linguaggi di programmazione.  
  
-   Definire le regole che i linguaggi devono seguire, garantendo l'interazione tra oggetti scritti in linguaggi diversi.  
  
-   Fornire una libreria che contiene i tipi di dati primitivi, ad esempio <xref:System.Boolean>, <xref:System.Byte>, <xref:System.Char>, <xref:System.Int32> e <xref:System.UInt64>, utilizzati nello sviluppo delle applicazioni.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Tipi in .NET Framework](#types_in_the_net_framework)  
  
-   [Definizioni dei tipi](#type_definitions)  
  
-   [Membri dei tipi](#type_members)  
  
-   [Caratteristiche dei membri dei tipi](#characteristics_of_type_members)  
  
<a name="types_in_the_net_framework"></a>   
## Tipi in .NET Framework  
 Tutti i tipi in .NET Framework sono tipi di valore o tipi di riferimento.  
  
 I tipi di valore sono tipi di dati i cui oggetti sono rappresentati dal valore effettivo dell'oggetto.  Se un'istanza di un tipo di valore viene assegnata a una variabile, a tale variabile viene fornita una copia aggiornata del valore.  
  
 I tipi di riferimento sono tipi di dati i cui oggetti sono rappresentati da un riferimento \(simile a un puntatore\) al valore effettivo dell'oggetto.  Se un tipo di riferimento viene assegnato a una variabile, tale variabile fa riferimento \(punta\) al valore originale.  Non viene effettuata alcuna copia.  
  
 Common Type System in .NET Framework supporta le cinque categorie di tipi seguenti:  
  
-   [Classi](#Classes)  
  
-   [Strutture](#Structures)  
  
-   [Enumerazioni](#Enumerations)  
  
-   [Interfacce](#Interfaces)  
  
-   [Delegati](#Delegates)  
  
<a name="Classes"></a>   
### Classi  
 Una classe è un tipo di riferimento che è possibile derivare direttamente da un'altra classe e che viene derivato in modo implicito da <xref:System.Object?displayProperty=fullName>.  La classe definisce le operazioni che un oggetto \(un'istanza della classe\) può eseguire \(metodi, eventi o proprietà\) e i dati che l'oggetto contiene \(campi\).  Sebbene una classe includa in genere sia la definizione che l'implementazione, a differenza delle interfacce che contengono, ad esempio, solo la definizione senza l'implementazione, può contenere uno o più membri privi di implementazione.  
  
 Nella tabella seguente vengono descritte alcune delle caratteristiche che una classe può avere.  Ogni linguaggio che supporta il runtime fornisce un modo per indicare che una classe o membro di classe dispone di una o più di queste caratteristiche.  È tuttavia possibile che i singoli linguaggi di programmazione destinati a .NET Framework non rendano disponibili tutte queste caratteristiche.  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|sealed|Specifica che da questo tipo non è possibile derivare un'altra classe.|  
|implementa|Indica che la classe utilizza una o più interfacce fornendo implementazioni dei membri di interfaccia.|  
|abstract|Indica che non è possibile creare un'istanza della classe.  Per utilizzarla è necessario derivare da essa un'altra classe.|  
|eredita|Indica che le istanze della classe possono essere utilizzate ovunque la classe sia specificata.  Una classe derivata che eredita da una classe di base può utilizzare l'implementazione di qualsiasi membro pubblico fornito dalla classe di base oppure la classe derivata può eseguire l'override dell'implementazione dei membri pubblici con la propria implementazione.|  
|exported o not exported|Indica se una classe è visibile all'esterno dell'assembly in cui è definita.  Questa caratteristica è applicabile unicamente alle classi di primo livello e non alle classi annidate.|  
  
> [!NOTE]
>  Una classe può anche essere annidata in una struttura o una classe padre.  Anche le classi annidate possiedono le caratteristiche dei membri.  Per ulteriori informazioni, vedere [Tipi annidati](#NestedTypes).  
  
 I membri di classe privi di implementazione sono membri astratti.  Una classe con uno o più membri astratti è essa stessa astratta e non è possibile crearne nuove istanze.  Con alcuni linguaggi destinati al runtime è possibile contrassegnare una classe come astratta anche se nessuno dei relativi membri è astratto.  È possibile utilizzare una classe astratta quando si desidera incapsulare un set di base di funzionalità che le classi derivate possono ereditare oppure sottoporre a override nelle circostanze appropriate.  Alle classi che non sono astratte viene fatto riferimento come a classi concrete.  
  
 Una classe può implementare un numero qualsiasi di interfacce, ma può ereditare solo da una classe di base, oltre che da <xref:System.Object?displayProperty=fullName>, da cui tutte le classi ereditano in modo implicito.  Tutte le classi devono avere almeno un costruttore, per l'inizializzazione di nuove istanze della classe.  Se non si definisce in modo esplicito un costruttore, la maggior parte dei compilatori fornisce automaticamente un costruttore predefinito \(senza parametri\).  
  
<a name="Structures"></a>   
### Strutture  
 Una struttura è un tipo di valore che deriva in modo implicito da <xref:System.ValueType?displayProperty=fullName>, che a sua volta deriva da <xref:System.Object?displayProperty=fullName>.  Una struttura è molto utile per la rappresentazione di valori con requisiti di memoria piccoli e per passare valori come parametri per valori a metodi che dispongono di parametri fortemente tipizzati.  Nella libreria di classi .NET Framework tutti i tipi di dati primitivi \(<xref:System.Boolean>, <xref:System.Byte>, <xref:System.Char>, <xref:System.DateTime>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.UInt16>, <xref:System.UInt32> e <xref:System.UInt64>\) sono definiti come strutture.  
  
 Analogamente alle classi, le strutture definiscono sia i dati \(i campi della struttura\) che le operazioni che è possibile eseguire s tali dati \(i metodi della struttura\).  Ciò significa che è possibile chiamare metodi nelle strutture, inclusi i metodi virtuali definiti nelle classi <xref:System.Object?displayProperty=fullName> e <xref:System.ValueType?displayProperty=fullName> e qualsiasi metodo definito nel tipo di valore stesso.  In altre parole, le strutture possono disporre di campi, proprietà ed eventi, nonché di metodi statici e non statici.  È possibile creare istanze di strutture, passarle come parametri, archiviarle come variabili locali oppure in un campo di un altro tipo di valore o tipo di riferimento.  Le strutture possono inoltre implementare interfacce.  
  
 I tipi di valore differiscono dalle classi per diversi motivi.  Innanzitutto, anche se ereditano in modo implicito da <xref:System.ValueType?displayProperty=fullName>, non possono ereditare direttamente da nessun tipo.  Analogamente, tutti i tipi di valore sono sealed, ovvero nessun altro tipo può essere derivato da essi.  Non richiedono inoltre costruttori.  
  
 Per ogni tipo di valore, Common Language Runtime fornisce un tipo sottoposto a boxing corrispondente, ovvero una classe avente lo stesso stato e lo stesso comportamento del tipo di valore.  Per un'istanza di un tipo di valore viene eseguita la conversione boxing quando viene passata a un metodo che accetta un parametro di tipo <xref:System.Object?displayProperty=fullName>.  La conversione unboxing, ovvero la conversione da un'istanza di una classe di nuovo in un'istanza di un tipo di valore, viene eseguita quando il controllo viene restituito da una chiamata al metodo che accetta un tipo di valore come parametro per riferimento.  In alcuni linguaggi è richiesto l'utilizzo di una sintassi speciale quando il tipo sottoposto a boxing è obbligatorio, mentre in altri il tipo sottoposto a boxing viene utilizzato automaticamente quando è necessario.  Quando si definisce un tipo di valore si sta definendo sia il tipo boxed che il tipo unboxed.  
  
<a name="Enumerations"></a>   
### Enumerazioni  
 Un'enumerazione \(enum\) è un tipo di valore che eredita direttamente da <xref:System.Enum?displayProperty=fullName> e che fornisce nomi alternativi per i valori di un tipo primitivo sottostante.  Un tipo di enumerazione dispone di un nome, un tipo sottostante che deve essere uno dei tipi Signed Integer o Unsigned Integer predefiniti, ad esempio <xref:System.Byte>, <xref:System.Int32> o <xref:System.UInt64>, e di un set di campi.  I campi sono campi letterali statici, ognuno dei quali rappresenta una costante.  Lo stesso valore può essere assegnato a più campi.  In questo caso, è necessario contrassegnare uno dei valori come valore di enumerazione primario a scopo di reflection e conversione di stringhe.  
  
 È possibile assegnare a un'enumerazione un valore del tipo sottostante e viceversa. Nel runtime non è richiesto alcun cast.  È possibile creare un'istanza di un'enumerazione e chiamare i metodi di <xref:System.Enum?displayProperty=fullName>, nonché qualsiasi metodo definito nel tipo sottostante dell'enumerazione.  In alcuni linguaggi, tuttavia, potrebbe non essere possibile passare un'enumerazione come parametro quando un'istanza del tipo sottostante è obbligatoria \(o viceversa\).  
  
 Alle enumerazioni si applicano le seguenti ulteriori restrizioni:  
  
-   La definizione dei metodi non può essere eseguita direttamente dall'enumerazione.  
  
-   Con un'enumerazione non è possibile implementare un'interfaccia.  
  
-   Con un'enumerazione non è possibile definire proprietà o eventi.  
  
-   Le enumerazioni non possono essere generiche, a meno che non siano generiche solo perché annidate all'interno di un tipo generico.  In altre parole, un'enumerazione non può disporre di parametri dei tipi propri.  
  
    > [!NOTE]
    >  I tipi annidati, incluse le enumerazioni, creati con Visual Basic, C\# e C\+\+ comprendono i parametri di tutti i tipi generici che li comprendono e sono pertanto generici anche se non dispongono di propri parametri di tipi.  Per ulteriori informazioni, vedere "Tipi annidati" nell'argomento di riferimento <xref:System.Type.MakeGenericType%2A?displayProperty=fullName>.  
  
 L'attributo <xref:System.FlagsAttribute> denota un tipo speciale di enumerazione definito campo di bit.  Nel runtime non viene fatta distinzione tra enumerazioni tradizionali e campi di bit, ma è possibile che tale distinzione esista nel linguaggio utilizzato.  Quando tale distinzione viene effettuata, gli operatori bit per bit possono essere utilizzati sui campi di bit, ma non sulle enumerazioni, per generare valori non denominati.  Le enumerazioni sono in genere utilizzate per elenchi di elementi univoci, come giorni della settimana o nomi di paesi o province.  I campi di bit sono normalmente utilizzati per elenchi di qualità o quantità che possono ricorrere in combinazioni, come `Red And Big And Fast`.  
  
 Nell'esempio che segue viene illustrato come utilizzare sia i campi di bit, sia le enumerazioni tradizionali.  
  
 [!code-csharp[Conceptual.Types.Enum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.enum/cs/example.cs#1)]
 [!code-vb[Conceptual.Types.Enum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.enum/vb/example.vb#1)]  
  
<a name="Interfaces"></a>   
### Interfacce  
 Un'interfaccia definisce un contratto che specifica una relazione di tipo "può" o una relazione di tipo "ha".  Le interfacce vengono in genere utilizzate per implementare funzionalità, ad esempio il confronto e l'ordinamento \(interfacce <xref:System.IComparable> e <xref:System.IComparable%601>\), il test di uguaglianza \(interfaccia <xref:System.IEquatable%601>\) o l'enumerazione di elementi in una raccolta \(interfacce <xref:System.Collections.IEnumerable> e <xref:System.Collections.Generic.IEnumerable%601>\).  Le interfacce possono disporre di proprietà, metodi ed eventi, ovvero tutti membri astratti. Per questo motivo, anche se l'interfaccia definisce i membri e le relative firme, il compito di definire le funzionalità di ogni membro dell'interfaccia viene lasciato al tipo che la implementa.  Ciò significa che qualsiasi classe o struttura che implementa un'interfaccia deve fornire le definizioni per i membri astratti dichiarati nell'interfaccia.  Un'interfaccia può richiedere che qualsiasi classe o struttura che la implementa implementi anche una o più altre interfacce.  
  
 Alle interfacce si applicano le seguenti restrizioni:  
  
-   Un'interfaccia può essere dichiarata con qualsiasi accessibilità ma i membri di interfaccia devono tutti avere accessibilità pubblica.  
  
-   Con un'interfaccia non è possibile definire costruttori.  
  
-   Le interfacce non possono definire campi.  
  
-   Le interfacce possono definire solo membri di istanza.  Non possono definire membri statici.  
  
 Ogni linguaggio deve fornire regole per il mapping di un'implementazione all'interfaccia che richiede il membro, in quanto più interfacce possono dichiarare un membro con la stessa firma e i membri possono disporre di implementazioni separate.  
  
<a name="Delegates"></a>   
### Delegati  
 I delegati sono tipi di riferimento che assolvono a una funzione simile a quella dei puntatori a funzione in C\+\+.  Vengono utilizzati per i gestori di eventi e le funzioni di callback in .NET Framework.  Diversamente dai puntatori a funzione, i delegati sono sicuri, verificabili e indipendenti dai tipi.  Un tipo delegato può rappresentare qualsiasi metodo di istanza o metodo statico con una firma compatibile.  
  
 Un parametro di un delegato è compatibile con il parametro di un metodo corrispondente se il tipo del parametro del delegato è più restrittivo rispetto al tipo del parametro del metodo. In questo modo si garantisce che un argomento passato al delegato possa essere passato in modo sicuro al metodo.  
  
 Analogamente, il tipo restituito di un delegato è compatibile con il tipo restituito di un metodo se il tipo restituito del metodo è più restrittivo rispetto al tipo restituito del delegato. In questo modo si garantisce la possibilità di eseguire in modo sicuro il cast del valore restituito del metodo nel tipo restituito del delegato.  
  
 Un delegato con un parametro del tipo <xref:System.Collections.IEnumerable> e un tipo restituito <xref:System.Object> può, ad esempio, rappresentare un metodo con un parametro del tipo <xref:System.Object> e un valore restituito del tipo <xref:System.Collections.IEnumerable>.  Per ulteriori informazioni e un codice di esempio, vedere <xref:System.Delegate.CreateDelegate%28System.Type%2CSystem.Object%2CSystem.Reflection.MethodInfo%29?displayProperty=fullName>.  
  
 Un delegato è associato al metodo che rappresenta.  Oltre a essere associato al metodo, un delegato può essere associato a un oggetto.  L'oggetto rappresenta il primo parametro del metodo e viene passato al metodo ogni volta che viene richiamato il delegato.  Se il metodo è un metodo di istanza, l'oggetto associato viene passato come parametro `this` implicito \(`Me` in Visual Basic\). Se il metodo è statico, l'oggetto viene passato come primo parametro formale del metodo e la firma del delegato deve corrispondere ai parametri rimanenti.  Per ulteriori informazioni e un codice di esempio, vedere <xref:System.Delegate?displayProperty=fullName>.  
  
 Tutti i delegati ereditano da <xref:System.MulticastDelegate?displayProperty=fullName>, che eredita da <xref:System.Delegate?displayProperty=fullName>.  I linguaggi C\#, Visual Basic e C\+\+ non consentono l'ereditarietà da questi tipi.  Forniscono invece parole chiave per la dichiarazione di delegati.  
  
 Dal momento che i delegati ereditano da <xref:System.MulticastDelegate>, un delegato presenta un elenco chiamate, ovvero un elenco di metodi rappresentati dal delegato che vengono eseguiti quando il delegato viene chiamato.  Tutti i metodi dell'elenco ricevono gli argomenti forniti quando viene chiamato il delegato.  
  
> [!NOTE]
>  Il valore restituito non è definito per un delegato il cui elenco chiamate contiene più metodi, anche se il delegato dispone di un tipo restituito.  
  
 In molti casi, ad esempio con i metodi di callback, un delegato rappresenta un solo metodo e le uniche azioni che è necessario eseguire sono la creazione e il richiamo del delegato.  
  
 Per i delegati che rappresentano più metodi, .NET Framework fornisce metodi delle classi di delegati <xref:System.Delegate> e <xref:System.MulticastDelegate> per supportare operazioni quali l'aggiunta di un metodo a un elenco chiamate di un delegato \(il metodo <xref:System.Delegate.Combine%2A?displayProperty=fullName>\), la rimozione di un metodo \(il metodo <xref:System.Delegate.Remove%2A?displayProperty=fullName>\) e il recupero dell'elenco chiamate \(il metodo <xref:System.Delegate.GetInvocationList%2A?displayProperty=fullName>\).  
  
> [!NOTE]
>  Non è necessario utilizzare questi metodi per i delegati dei gestori di eventi nei linguaggi C\#, C\+\+ e Visual Basic perché questi linguaggi forniscono la sintassi per l'aggiunta e la rimozione dei gestori di eventi.  
  
 [Torna all'inizio](#top)  
  
<a name="type_definitions"></a>   
## Definizioni dei tipi  
 Una definizione di tipo include gli elementi seguenti:  
  
-   Gli eventuali attributi definiti per il tipo.  
  
-   Accessibilità del tipo \(visibilità\)  
  
-   Il nome del tipo.  
  
-   Il tipo base del tipo.  
  
-   Le interfacce eventualmente implementate dal tipo.  
  
-   Le definizioni per ciascuno dei membri del tipo.  
  
### Attributi  
 Gli attributi forniscono metadati aggiuntivi definiti dall'utente.  Comunemente vengono utilizzati per archiviare informazioni aggiuntive su un tipo nell'assembly o per modificare il comportamento di un membro del tipo nella fase di progettazione o nell'ambiente di runtime.  
  
 Gli attributi stessi sono classi che ereditano da <xref:System.Attribute?displayProperty=fullName>.  I linguaggi che supportano l'utilizzo di attributi forniscono ognuno la sintassi necessaria per l'applicazione degli attributi a un elemento del linguaggio.  Gli attributi possono essere applicati a quasi tutti gli elementi del linguaggio. Gli elementi specifici a cui è possibile applicare un attributo sono definiti dall'oggetto <xref:System.AttributeUsageAttribute> applicato a tale classe di attributi.  
  
### Accessibilità dei tipi  
 Tutti i tipi dispongono di un modificatore che ne regola l'accessibilità da parte di altri tipi.  Nella tabella che segue si descrive l'accessibilità dei tipi supportata dal runtime.  
  
|Accessibilità|Descrizione|  
|-------------------|-----------------|  
|public|Il tipo è accessibile da tutti gli assembly.|  
|assembly|Il tipo è accessibile solo dall'interno dell'assembly.|  
  
 L'accessibilità di un tipo annidato dipende dal relativo dominio di accessibilità, che è determinato sia dall'accessibilità dichiarata del membro che dal dominio di accessibilità del tipo che lo contiene direttamente.  Tuttavia il dominio di accessibilità di un tipo annidato non può essere superiore a quello del tipo che lo contiene.  
  
 Il dominio di accessibilità di un membro annidato `M` dichiarato in un tipo `T` all'interno di un programma `P` viene definito come riportato di seguito \(si noti che `M` potrebbe essere un tipo\):  
  
-   Se l'accessibilità dichiarata di `M` è `public`, il dominio di accessibilità di `M` è il dominio di accessibilità di `T`.  
  
-   Se l'accessibilità dichiarata di `M` è `protected internal`, il dominio di accessibilità di `M` è l'intersezione del dominio di accessibilità di `T` con il testo di programma di `P` e il testo di programma di qualsiasi tipo derivato da `T` dichiarato esternamente a `P`.  
  
-   Se l'accessibilità dichiarata di `M` è `protected`, il dominio di accessibilità di `M` è l'intersezione del dominio di accessibilità di `T` con il testo di programma di `T` e qualsiasi tipo derivato da `T`.  
  
-   Se l'accessibilità dichiarata di `M` è `internal`, il dominio di accessibilità di `M` è l'intersezione del dominio di accessibilità di `T` con il testo di programma di `P`.  
  
-   Se l'accessibilità dichiarata di `M` è `private`, il dominio di accessibilità di `M` è il testo di programma di `T`.  
  
### Nomi dei tipi  
 Il sistema di tipi comuni impone solo due restrizioni sui nomi:  
  
-   Tutti i nomi sono codificati come stringhe di caratteri Unicode, ovvero a 16 bit.  
  
-   I nomi non possono avere un valore incorporato \(a 16 bit\) pari a 0x0000.  
  
 La maggior parte dei linguaggi impone tuttavia restrizioni aggiuntive per i nomi dei tipi.  Poiché tutti i confronti vengono effettuati byte per byte, sono indipendenti dalle impostazioni locali e fanno distinzione tra maiuscole e minuscole.  
  
 Sebbene un tipo possa fare riferimento a tipi di altri moduli e assembly, deve essere definito completamente all'interno di un modulo .NET Framework.  A seconda del supporto del compilatore, tuttavia, può essere diviso in più file di codice sorgente. I nomi dei tipi devono essere univoci solo all'interno di uno spazio dei nomi.  Per identificare completamente un tipo, il relativo nome deve essere qualificato dallo spazio dei nomi che contiene l'implementazione del tipo.  
  
### Tipi base e interfacce  
 Un tipo può ereditare valori e comportamenti da un altro tipo.  Common Type System non consente ai tipi di ereditare da più di un tipo base.  
  
 Un tipo può implementare un numero indefinito di interfacce.  Per implementare un'interfaccia un tipo deve implementare tutti i membri virtuali di tale interfaccia.  Un metodo virtuale può essere implementato da un tipo derivato e può essere richiamato in modo statico o dinamico.  
  
 [Torna all'inizio](#top)  
  
<a name="type_members"></a>   
## Membri dei tipi  
 Il runtime consente di definire membri del tipo per specificare il comportamento e lo stato di un tipo.  I membri dei tipi includono gli elementi seguenti:  
  
-   [Campi](#Fields)  
  
-   [Proprietà](#Properties)  
  
-   [Metodi](#Methods)  
  
-   [Costruttori](#Constructors)  
  
-   [Eventi](#Events)  
  
-   [Tipi annidati](#NestedTypes)  
  
<a name="Fields"></a>   
### Campi  
 Un campo descrive e contiene parte dello stato del tipo.  I campi possono essere di qualsiasi tipo supportato dal runtime.  Nella maggior parte dei casi, i campi sono `private` o `protected`, in modo che siano accessibili solo dall'interno della classe o da una classe derivata.  Se il valore di un campo può essere modificato dall'esterno del relativo tipo, viene in genere utilizzata una funzione di accesso set della proprietà.  I campi esposti pubblicamente sono in genere di sola lettura e possono essere di due tipi:  
  
-   Costanti, il cui valore viene assegnato durante la fase di progettazione.  Si tratta di membri statici di una classe, sebbene non vengano definiti utilizzando la parola chiave `static` \(`Shared` in Visual Basic\).  
  
-   Variabili di sola lettura, i cui valori possono essere assegnati nel costruttore di classi.  
  
 Nell'esempio seguente vengono illustrati questi due utilizzi di campi di sola lettura.  
  
 [!code-csharp[Conceptual.Types.Members.Fields#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.members.fields/cs/example.cs#1)]
 [!code-vb[Conceptual.Types.Members.Fields#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.members.fields/vb/example.vb#1)]  
  
<a name="Properties"></a>   
### Proprietà  
 Una proprietà consente di denominare un valore o uno stato del tipo e di definire i metodi per ottenere o impostare il valore della proprietà.  Le proprietà possono essere tipi primitivi, raccolte di tipi primitivi, tipi definiti dall'utente, oppure raccolte di tipi definiti dall'utente.  Sono spesso utilizzate per mantenere l'interfaccia pubblica di un tipo indipendente dalla sua effettiva rappresentazione.  In questo modo le proprietà riflettono valori che non sono archiviati direttamente nella classe, ad esempio quando una proprietà restituisce un valore calcolato, oppure eseguono la convalida prima che i valori vengano assegnati a campi privati.  Nell'esempio seguente viene illustrato quest'ultimo caso.  
  
 [!code-csharp[Conceptual.Types.Members.Properties#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.members.properties/cs/example.cs#1)]
 [!code-vb[Conceptual.Types.Members.Properties#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.members.properties/vb/example.vb#1)]  
  
 Oltre a includere la proprietà stessa, nel MSIL \(Microsoft Intermediate Language\) per un tipo contenente una proprietà leggibile è incluso un metodo `get_`*propertyname*, mentre nel MSIL per un tipo contenente una proprietà scrivibile è incluso un metodo `set_`*propertyname*.  
  
<a name="Methods"></a>   
### Metodi  
 Un metodo descrive le operazioni disponibili sul tipo.  Nella firma di un metodo sono specificati i tipi consentiti di tutti i relativi parametri e del relativo valore restituito.  
  
 Sebbene molti metodi definiscono il numero preciso di parametri necessari per le chiamate al metodo, alcuni metodi supportano un numero di parametri variabile.  Il parametro finale dichiarato di questi metodi è contrassegnato con l'attributo <xref:System.ParamArrayAttribute>.  I compilatori di linguaggio forniscono in genere una parola chiave, ad esempio `params` in C\# e `ParamArray` in Visual Basic, che utilizza esplicitamente l'attributo <xref:System.ParamArrayAttribute> non necessario.  
  
<a name="Constructors"></a>   
### Costruttori  
 Un costruttore è un tipo speciale di metodo che consente di creare nuove istanze di una classe o di una struttura.  Analogamente a ogni altro metodo, un costruttore può includere parametri. I costruttori, tuttavia, non restituiscono alcun valore, ovvero restituiscono `void`.  
  
 Se il codice sorgente per una classe non definisce in modo esplicito un costruttore, il compilatore include un costruttore predefinito \(senza parametri\).  Se tuttavia il codice sorgente per una classe definisce solo costruttori con parametri, i compilatori Visual Basic e C\# non generano un costruttore senza parametri.  
  
 Se il codice sorgente per una struttura definisce i costruttori, essi devono essere con parametri. Una struttura non può definire un costruttore predefinito \(senza parametri\) e i compilatori non generano costruttori senza parametri per strutture o altri tipi di valori.  Tutti i tipi di valori hanno un costruttore predefinito implicito.  Questo costruttore viene implementato da Common Language Runtime e inizializza tutti i campi della struttura sui valori predefiniti.  
  
<a name="Events"></a>   
### Eventi  
 Un evento definisce una situazione a cui è possibile fornire risposta e metodi per la sottoscrizione, l'annullamento della sottoscrizione e la generazione dell'evento.  Gli eventi sono spesso utilizzati per indicare modifiche di stato a tipi diversi.  Per altre informazioni, vedere [Eventi](../../../ml/index.xml).  
  
<a name="NestedTypes"></a>   
### Tipi annidati  
 I tipi annidati sono tipi membri di altri tipi.  I tipi annidati devono essere strettamente collegati ai rispettivi tipi contenitori e non devono essere utilizzati come tipi generici.  I tipi annidati risultano utili quando il tipo dichiarante utilizza e crea istanze del tipo annidato e quando il loro utilizzo non viene esposto in membri pubblici.  
  
 Per alcuni sviluppatori i tipi annidati possono generare confusione e dovrebbero essere visibili pubblicamente solo in casi di assoluta necessità.  In una libreria progettata correttamente è improbabile che gli sviluppatori debbano utilizzare tipi annidati per creare istanze di oggetti o dichiarare variabili.  
  
 [Torna all'inizio](#top)  
  
<a name="characteristics_of_type_members"></a>   
## Caratteristiche dei membri dei tipi  
 In Common Type System i membri dei tipi possono disporre di caratteristiche diverse, anche se non è necessario che i linguaggi le supportino tutte.  Nella tabella riportata di seguito vengono descritte le caratteristiche dei membri.  
  
|Caratteristica|Si applica a|Descrizione|  
|--------------------|------------------|-----------------|  
|abstract|Metodi, proprietà ed eventi|Il tipo non fornisce l'implementazione del metodo.  I tipi che ereditano o implementano metodi astratti devono fornire un'implementazione per il metodo.  L'unica eccezione si verifica nel caso in cui il tipo derivato sia esso stesso un tipo astratto.  Tutti i metodi astratti sono virtuali.|  
|private, gruppo, assembly, gruppo e assembly, gruppo o assembly o public|Tutti|Consente di definire l'accessibilità del membro.<br /><br /> private<br /> Accessibile solo dall'interno dello stesso tipo del membro o di un tipo annidato.<br /><br /> family<br /> Accessibile dall'interno dello stesso tipo del membro e dai tipi derivati che ereditano da esso.<br /><br /> assembly<br /> Accessibile solo nell'assembly nel quale il tipo viene definito.<br /><br /> family e assembly<br /> Accessibile solo dai tipi che sono qualificati sia per l'accesso di gruppo che di assembly.<br /><br /> family o assembly<br /> Accessibile solo dai tipi che sono qualificati per l'accesso di gruppo o per quello di assembly.<br /><br /> public<br /> Accessibile da qualsiasi tipo.|  
|final|Metodi, proprietà ed eventi|Il metodo virtuale non può essere sottoposto a override in un tipo derivato.|  
|initialize\-only|Campi|Il valore può essere solo inizializzato e non può essere scritto dopo l'inizializzazione.|  
|istanza|Campi, metodi, proprietà ed eventi|Se un membro non è contrassegnato come `static` \(C\# e C\+\+\), `Shared` \(Visual Basic\), `virtual` \(C\# e C\+\+\) o `Overridable` \(Visual Basic\), è un membro di istanza \(nessuna parola chiave di istanza\).  Ci saranno tante copie di tali membri in memoria quanti sono gli oggetti che li utilizzano.|  
|valore letterale|Campi|Il valore assegnato al campo è un valore fisso, noto in fase di compilazione, di un tipo di valore incorporato.  Ai campi literal viene a volte fatto riferimento come a costanti.|  
|newslot o override|Tutti|Definisce il modo in cui il membro interagisce con membri ereditati aventi la stessa firma:<br /><br /> newslot<br /> Nasconde i membri ereditati aventi la stessa firma.<br /><br /> ignora<br /> Sostituisce la definizione di un metodo virtuale ereditato.<br /><br /> Il valore predefinito è newslot.|  
|statico|Campi, metodi, proprietà ed eventi|Il membro appartiene al tipo sul quale viene definito, non a un'istanza specifica del tipo. Il membro esiste anche se non viene creata un'istanza del tipo ed è condiviso tra tutte le istanze del tipo.|  
|virtuale|Metodi, proprietà ed eventi|Il metodo può essere implementato da un tipo derivato e può essere richiamato in modo statico o dinamico.  Se viene utilizzata la chiamata dinamica, il tipo dell'istanza che effettua la chiamata in fase di esecuzione, e non il tipo noto in fase di compilazione, determina l'implementazione del metodo chiamata.  Per richiamare un metodo virtuale in modo statico, potrebbe essere necessario eseguire il cast della variabile in un tipo che utilizza la versione desiderata del metodo.|  
  
### Overload  
 Ciascun membro di tipo dispone di una firma univoca.  La firma di un metodo è costituita dal nome del metodo e da un elenco di parametri, ovvero l'ordine e i tipi degli argomenti del metodo.  All'interno di un tipo è possibile definire più metodi con lo stesso nome, purché la relativa firma sia diversa.  Quando vengono definiti due o più metodi con lo stesso nome si dice che il metodo è stato sottoposto a overload.  In <xref:System.Char?displayProperty=fullName>, ad esempio, il metodo <xref:System.Char.IsDigit%2A> è sottoposto a overload.  Un metodo accetta un oggetto <xref:System.Char>.  L'altro metodo accetta un oggetto <xref:System.String> e un oggetto <xref:System.Int32>.  
  
> [!NOTE]
>  Il tipo restituito non viene considerato parte della firma del metodo.  Ciò significa che i metodi non possono essere sottoposti a overload se differiscono unicamente per il tipo restituito.  
  
### Eredità, override e membri nascosti  
 Un tipo derivato eredita tutti i membri del relativo tipo di base, ovvero tali membri vengono definiti e resi disponibili nel tipo derivato.  Il comportamento o le qualità dei membri ereditati possono essere modificati in due modi:  
  
-   È possibile nascondere un membro ereditato con un tipo derivato definendo un nuovo membro con la stessa firma.  Questa operazione può essere eseguita per rendere privato un membro precedentemente pubblico oppure per definire un nuovo comportamento per un metodo ereditato contrassegnato come `final`.  
  
-   Con un tipo derivato è possibile eseguire l'override di un metodo virtuale ereditato.  Nel metodo con cui viene eseguito l'override si fornisce una nuova definizione del metodo che sarà richiamato in base al tipo del valore in fase di esecuzione anziché in base al tipo della variabile nota in fase di compilazione.  Un metodo può sottoporre a override un metodo virtuale solo se quest'ultimo non è contrassegnato come `final` e se il nuovo metodo è accessibile almeno quanto il metodo virtuale.  
  
## Vedere anche  
 [Libreria di classi .NET Framework](http://go.microsoft.com/fwlink/?LinkID=217856)   
 [Common Language Runtime](../../../ocs/standard/clr.md)   
 [Conversione di tipi in .NET Framework](../../../docs/standard/base-types/type-conversion.md)