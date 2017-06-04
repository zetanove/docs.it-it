---
title: "Linee guida per le raccolte | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 297b8f1d-b11f-4dc6-960a-8e990817304e
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Linee guida per le raccolte
Qualsiasi tipo progettato specificamente per la modifica di un gruppo di oggetti con alcune caratteristiche comuni può essere considerato una raccolta. È quasi sempre appropriato per questi tipi implementare <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>, pertanto in questa sezione è considerare solo i tipi che implementano una o entrambe le interfacce di raccolte.  
  
 **X non** utilizzare insiemi con tipizzazione delle API pubbliche.  
  
 Il tipo di tutti i valori restituiti e parametri che rappresentano gli elementi della raccolta deve essere il tipo di elemento esatto, non di uno dei tipi di base \(si applica solo ai membri pubblici della raccolta\).  
  
 **X non** utilizzare <xref:System.Collections.ArrayList> o <xref:System.Collections.Generic.List%601> delle API pubbliche.  
  
 Questi tipi sono strutture di dati progettate per essere utilizzato nell'implementazione interna, non nelle API pubbliche.`List<T>` è ottimizzato per le prestazioni e potenza al costo di condizionamento delle API e flessibilità. Ad esempio, se viene restituito `List<T>`, non sempre sarà in grado di ricevere notifiche quando il codice client modifica la raccolta. Inoltre, `List<T>` espone molti membri, ad esempio <xref:System.Collections.Generic.List%601.BinarySearch%2A>, che non sono utili o applicabile in molti scenari. Le due sezioni seguenti vengono descritti i tipi \(astrazioni\) progettati appositamente per l'utilizzo delle API pubbliche.  
  
 **X non** utilizzare `Hashtable` o `Dictionary<TKey,TValue>` delle API pubbliche.  
  
 Questi tipi sono strutture di dati progettate per essere utilizzato nell'implementazione interna. Utilizzano le API pubbliche <xref:System.Collections.IDictionary>, `IDictionary <TKey, TValue>`, o un tipo personalizzato che implementa una o entrambe le interfacce.  
  
 **X non** utilizzare <xref:System.Collections.Generic.IEnumerator%601>, <xref:System.Collections.IEnumerator>, o qualsiasi altro tipo che implementa una di queste interfacce, ad eccezione di come il tipo restituito di un `GetEnumerator` metodo.  
  
 Tipi di restituzione enumeratori da metodi diversi da `GetEnumerator` non può essere utilizzato con il `foreach` istruzione.  
  
 **X non** implementano sia `IEnumerator<T>` e `IEnumerable<T>` sullo stesso tipo. Lo stesso vale per le interfacce non generiche `IEnumerator` e `IEnumerable`.  
  
## Parametri della raccolta  
 **✓ si** utilizzare possibili specializzati meno tipo come tipo di parametro. La maggior parte dei membri come raccolte poiché i parametri vengono utilizzati il `IEnumerable<T>` interfaccia.  
  
 **X evitare** mediante <xref:System.Collections.Generic.ICollection%601> o <xref:System.Collections.ICollection> come parametro per accedere la `Count` proprietà.  
  
 Utilizzare invece `IEnumerable<T>` o `IEnumerable` e il controllo in modo dinamico se l'oggetto implementa `ICollection<T>` o `ICollection`.  
  
## Proprietà di raccolta e i valori restituiti  
 **X non** forniscono proprietà impostabili insieme.  
  
 Gli utenti possono sostituire il contenuto della raccolta deselezionando innanzitutto la raccolta e quindi aggiungere il nuovo contenuto. Se la sostituzione dell'intero insieme è uno scenario comune, si consiglia di fornire il `AddRange` metodo per la raccolta.  
  
 **✓ si** utilizzare `Collection<T>` o una sottoclasse di `Collection<T>` per raccolte di lettura\/scrittura che rappresentano i valori di proprietà o a capo.  
  
 Se `Collection<T>` non soddisfa un requisito \(ad esempio, la raccolta non è necessario implementare <xref:System.Collections.IList>\), utilizzare un insieme personalizzato implementando `IEnumerable<T>`, `ICollection<T>`, o <xref:System.Collections.Generic.IList%601>.  
  
 **✓ si** utilizzare <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>, una sottoclasse di `ReadOnlyCollection<T>`, o, in casi rari `IEnumerable<T>` per le raccolte di sola lettura che rappresenta i valori di proprietà o a capo.  
  
 In generale, preferire `ReadOnlyCollection<T>`. Se non vengono soddisfatti alcuni requisiti \(ad esempio, la raccolta non è necessario implementare `IList`\), utilizzare un insieme personalizzato implementando `IEnumerable<T>`, `ICollection<T>`, o `IList<T>`. Se si implementa una raccolta di sola lettura personalizzata, implementare `ICollection<T>.ReadOnly` restituirà false.  
  
 Nei casi in cui si è certi che l'unico scenario si desidera supportare mai iterazione forward\-only, è possibile utilizzare semplicemente `IEnumerable<T>`.  
  
 **✓ PROVARE** tramite sottoclassi di raccolte generiche di base invece di utilizzare direttamente le raccolte.  
  
 In questo modo per un nome più significativo e per aggiungere i membri di supporto che non sono presenti i tipi di raccolta di base. Questo vale soprattutto per le API di alto livello.  
  
 **✓ PROVARE** restituzione di una sottoclasse di `Collection<T>` o `ReadOnlyCollection<T>` dalla proprietà e metodi comunemente utilizzati.  
  
 Questo modo è possibile aggiungere metodi helper o modificare l'implementazione di raccolta in futuro.  
  
 **✓ PROVARE** utilizzando una raccolta con chiave se gli elementi archiviati nella raccolta dispongono di chiavi univoche \(nomi, ID, ecc.\). Le raccolte con chiave sono che può essere indicizzato da un numero intero e una chiave e vengono in genere implementati ereditando da `KeyedCollection<TKey,TItem>`.  
  
 Raccolte con chiave in genere hanno maggiore footprint di memoria e non devono essere utilizzate se il sovraccarico della memoria supera i vantaggi di avere le chiavi.  
  
 **X non** restituiranno valori null da una proprietà di raccolta o da metodi che restituiscono raccolte. Restituisce una raccolta vuota o una matrice vuota.  
  
 La regola generale è che devono essere null e vuote raccolte \(elemento 0\) o matrici trattato.  
  
### Snapshot e raccolte Live  
 Le raccolte che rappresenta uno stato a un certo punto nel tempo sono definite insiemi di snapshot. Ad esempio, una raccolta contenente le righe restituite da una query di database sarà uno snapshot. Le raccolte che rappresentano sempre lo stato corrente sono definite insiemi live. Ad esempio, una raccolta di `ComboBox` elementi è una raccolta live.  
  
 **X non** restituiscono raccolte di snapshot da proprietà. Le proprietà devono restituire raccolte live.  
  
 Metodi get di proprietà devono essere operazioni molto semplici. Restituzione di uno snapshot, è necessario creare una copia di una raccolta interna in un'operazione o \(n\).  
  
 **✓ si** utilizzare attivo o un insieme di snapshot `IEnumerable<T>` \(o i relativi sottotipi\) per rappresentare le raccolte sono volatili \(ad esempio, che possono modificare senza modificare in modo esplicito la raccolta\).  
  
 In generale, tutte le raccolte che rappresenta una risorsa condivisa \(ad esempio, i file in una directory\) sono volatili. Tali raccolte sono estremamente difficili o impossibili da implementare come raccolte live, a meno che l'implementazione è semplicemente un enumeratore forward\-only.  
  
## Scelta tra matrici e raccolte  
 **✓ si** preferisce raccolte nelle matrici.  
  
 Le raccolte forniscono maggiore controllo sul contenuto, possono evolversi nel tempo e sono più utilizzabili. Inoltre, l'utilizzo delle matrici per gli scenari di sola lettura è sconsigliato perché il costo della clonazione la matrice è troppo elevato. Studi di usabilità hanno dimostrato che alcuni sviluppatori preferisce tramite API basate su raccolta.  
  
 Tuttavia, se si siano sviluppando API di basso livello, potrebbe essere preferibile utilizzare matrici per gli scenari di lettura \/ scrittura. Le matrici dispongono di un footprint di memoria più piccolo, che consente di ridurre il working set, e l'accesso agli elementi in una matrice è più veloce perché è ottimizzato per il runtime.  
  
 **✓ PROVARE** utilizzo delle matrici nelle API di basso livello per ridurre il consumo di memoria e ottimizzare le prestazioni.  
  
 **✓ si** utilizzare matrici di byte anziché raccolte di byte.  
  
 **X non** utilizzare matrici per le proprietà se la proprietà sarebbe necessario restituire una nuova matrice \(ad esempio, una copia di una matrice interna\) ogni volta che viene chiamato il metodo Get della proprietà.  
  
## Implementazione di insiemi personalizzati  
 **✓ PROVARE** che eredita da `Collection<T>`, `ReadOnlyCollection<T>`, o `KeyedCollection<TKey,TItem>` durante la progettazione di nuove raccolte.  
  
 **✓ si** implementare `IEnumerable<T>` durante la progettazione di nuove raccolte. Si consiglia di implementare `ICollection<T>` o addirittura `IList<T>` dove risulta più appropriato.  
  
 Quando si implementa questo insieme personalizzato, seguono il modello API istituito `Collection<T>` e `ReadOnlyCollection<T>` quanto più possibile. Ovvero, implementare in modo esplicito gli stessi membri, denominare i parametri come nome di questi due insiemi utilizzarli e così via.  
  
 **✓ PROVARE** implementazione di interfacce di raccolta non generica \(`IList` e `ICollection`\) se la raccolta verrà spesso passata alle API che queste interfacce come input.  
  
 **X evitare** implementare interfacce di raccolta su tipi con API complesse non correlate al concetto di una raccolta.  
  
 **X non** ereditare le raccolte non generiche di base, ad esempio `CollectionBase`. Utilizzare `Collection<T>`, `ReadOnlyCollection<T>`, e `KeyedCollection<TKey,TItem>` invece.  
  
### Denominazione di raccolte personalizzate  
 Raccolte \(tipi che implementano `IEnumerable`\) vengono creati principalmente per due ragioni: \(1\) per creare una nuova struttura di dati con le operazioni specifiche della struttura e spesso le caratteristiche di prestazioni differenti rispetto alle strutture di dati esistente \(ad esempio,  <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.LinkedList%601>, <xref:System.Collections.Generic.Stack%601>\) e \(2\) per creare un insieme specifico per contenere un set specifico di elementi \(ad esempio,  <xref:System.Collections.Specialized.StringCollection>\). Strutture di dati vengono spesso utilizzate nell'implementazione interna di librerie e applicazioni. Raccolte specializzate sono principalmente a essere esposte dalle API \(come proprietà e tipi di parametro\).  
  
 **✓ si** utilizzare il suffisso "Dizionario" nei nomi di implementazione di astrazioni `IDictionary` o `IDictionary<TKey,TValue>`.  
  
 **✓ si** utilizzare il suffisso "Raccolta" nei nomi di tipi che implementano `IEnumerable` \(o dei relativi discendenti\) e che rappresenta un elenco di elementi.  
  
 **✓ si** utilizzare il nome della struttura di dati appropriato per le strutture di dati personalizzati.  
  
 **X evitare** utilizzando eventuali suffissi implicando particolare implementazione, ad esempio "LinkedList" o "Hashtable," nei nomi delle astrazioni di raccolta.  
  
 **✓ PROVARE** facendolo precedere i nomi di raccolta con il nome del tipo di elemento. Ad esempio, un insieme di archiviazione di elementi di tipo `Address` \(implementazione `IEnumerable<Address>`\) deve essere denominato `AddressCollection`. Se il tipo di elemento è un'interfaccia, "I" prefisso dell'elemento di tipo può essere omessa. Pertanto, una raccolta di <xref:System.IDisposable> elementi possono essere chiamati `DisposableCollection`.  
  
 **✓ PROVARE** utilizzando il prefisso "ReadOnly" nei nomi di raccolte di sola lettura se una raccolta modificabile corrispondente potrebbe essere aggiunti o esiste già nel framework.  
  
 Ad esempio, una raccolta di sola lettura di stringhe deve essere chiamata `ReadOnlyStringCollection`.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Linee guida di utilizzo](../../../docs/standard/design-guidelines/usage-guidelines.md)