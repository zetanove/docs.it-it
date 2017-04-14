---
title: "Compilazione e .NET Native | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e38ae4f3-3e3d-42c3-a4b8-db1aa9d84f85
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# Compilazione e .NET Native
Le applicazioni Windows 8.1 e Windows Desktop destinate a .NET Framework vengono per lo più scritte in un determinato linguaggio di programmazione e compilate in linguaggio intermedio \(IL\).  In fase di esecuzione, un compilatore JIT è responsabile della compilazione del linguaggio intermedio in codice nativo per il computer locale prima che un metodo venga eseguito per la prima volta.  Al contrario, la catena di strumenti .NET Native converte il codice sorgente in codice nativo in fase di compilazione.  Questo argomento confronta .NET Native con altre tecnologie di compilazione disponibili per le app .NET Framework e fornisce una panoramica pratica del modo in cui .NET Native produce codice nativo, utile a comprendere il motivo per cui le eccezioni che si verificano nel codice compilato con .NET Native non si verificano nel codice con compilazione JIT.  
  
## .NET Native: generazione di file binari nativi  
 Un'applicazione destinata a .NET Framework e non compilata mediante la catena di strumenti .NET Native è costituita dall'assembly dell'applicazione, che include quanto segue:  
  
-   Metadati che descrivono l'assembly, le relative dipendenze, i tipi che contiene e i relativi membri.  Metadati usati per la reflection, l'accesso ad associazione tardiva e in alcuni casi dal compilatore e dagli strumenti di compilazione.  
  
-   Codice di implementazione.  È costituito dai codici operativi del linguaggio intermedio \(IL\).  In fase di esecuzione, il compilatore JIT lo converte in codice nativo per la piattaforma di destinazione.  
  
 Oltre all'assembly principale dell'applicazione, un'app richiede la presenza di quanto segue:  
  
-   Qualsiasi libreria di classi aggiuntiva o assembly di terze parti necessario.  Allo stesso modo, questi assembly includono i metadati che lo descrivono, i relativi tipi e membri, nonché il linguaggio intermedio che implementa tutti i membri del tipo.  
  
-   Libreria di classi .NET Framework.  Si tratta di una raccolta di assembly installata nel sistema locale insieme a .NET Framework.  Gli assembly inclusi nella libreria di classi .NET Framework contengono un set completo di metadati e codice di implementazione.  
  
-   Common Language Runtime  Si tratta di una raccolta di librerie a collegamento dinamico che eseguono servizi quali caricamento di assembly, gestione della memoria e Garbage Collection, gestione delle eccezioni, compilazione JIT, comunicazione remota e interoperabilità.  Come la libreria di classi, il runtime viene installato nel sistema locale come parte dell'installazione di .NET Framework.  
  
 Per l'esecuzione corretta dell'app devono essere presenti l'intero CLR, così come i metadati e il linguaggio intermedio per tutti i tipi in assembly specifici dell'applicazione, assembly di terze parti e assemby di sistema.  
  
## Compilazione .NET Native e JIT  
 L'input per la catena di strumenti .NET Native è l'app di Windows Store generata dal compilatore C\# o Visual Basic.  In altre parole, la catena di strumenti .NET Native inizia l'esecuzione quando il compilatore del linguaggio ha terminato la compilazione di un'app di Windows Store.  
  
> [!TIP]
>  Poiché l'input per .NET Native è rappresentato dal linguaggio intermedio e dai metadati scritti negli assembly gestiti, è comunque possibile eseguire la generazione di codice personalizzato o altre operazioni personalizzate usando gli eventi di pre\-compilazione o post\-compilazione oppure modificando il file di progetto MSBuild.  
>   
>  Tuttavia, le categorie di strumenti che modificano il linguaggio intermedio e dunque impediscono alla catena di strumenti .NET Native di analizzare il linguaggio intermedio dell'app non sono supportati.  Le soluzioni di offuscamento rappresentano i principali strumenti di questo tipo.  
  
 Durante la conversione di un'app dal linguaggio intermedio al codice nativo, la catena di strumenti .NET Native esegue operazioni simili alle seguenti:  
  
-   Per alcuni percorsi di codice, sostituisce il codice basato sulla reflection e i metadati con codice nativo statico.  Ad esempio, se un tipo di valore non esegue l'override del metodo <xref:System.ValueType.Equals%2A?displayProperty=fullName>, il test predefinito per verificare l'uguaglianza usa la reflection per recuperare gli oggetti <xref:System.Reflection.FieldInfo> che rappresentano i campi del tipo di valore, quindi confronta i valori di campo di due istanze.  Durante la compilazione in codice nativo, la catena di strumenti .NET Native sostituisce il codice di reflection e i metadati con un confronto statico tra i valori dei campi.  
  
-   Ove possibile, tenta di eliminare tutti i metadati.  
  
-   Include negli assembly finali dell'app solo il codice di implementazione effettivamente richiamato dall'applicazione.  Questo incide in particolare sul codice nelle librerie di terze parti e nella libreria di classi .NET Framework.  Di conseguenza, un'app non dipende più da librerie di terze parti o dall'intera libreria di classi .NET Framework Class; infatti, il codice di terze parti e le librerie di classi .NET Framework sono ora locali rispetto all'app.  
  
-   Sostituisce il CLR completo con un runtime sottoposto a refactoring che contiene principalmente il Garbage Collector.  Il runtime con refactoring si trova in una libreria denominata mrt100\_app.dll, locale dell'app e di dimensioni pari a poche centinaia di KB.  Questo è possibile perché il collegamento statico elimina la necessità di molti dei servizi eseguiti dal CLR.  
  
    > [!NOTE]
    >  .NET Native usa lo stesso Garbage Collector del CLR standard.  Nel Garbage Collector di.NET Native la Garbage Collection in background è abilitata per impostazione predefinita.  Per altre informazioni sulla Garbage Collection, vedere [Fundamentals of Garbage Collection](../../../docs/standard/garbage-collection/fundamentals.md).  
  
> [!IMPORTANT]
>  .NET Native compila un'intera applicazione in un'applicazione nativa.  Non consente di compilare in codice nativo un singolo assembly che contiene una libreria di classi in modo che sia possibile chiamarlo indipendentemente dal codice gestito.  
  
 L'app risultante prodotta dalla catena di strumenti .NET Native viene scritta in una directory denominata ilc.out nella directory Debug o Release del progetto.  È costituita dai file seguenti:  
  
-   *\<nomeapp\>*.exe, un eseguibile stub che trasferisce il controllo a una speciale esportazione `Main` in *\<nomeapp\>*.dll.  
  
-   *\<nomeapp\>*.dll, una libreria Windows a collegamento dinamico che contiene tutto il codice dell'applicazione, il codice della libreria di classi .NET Framework e le eventuali librerie di terze parti con cui esistono dipendenze.  Contiene anche codice di supporto, ad esempio il codice necessario per l'interoperabilità con Windows e per serializzare gli oggetti nell'app.  
  
-   mrt100\_app.dll, un runtime sottoposto a refactoring che fornisce servizi di runtime, ad esempio Garbage Collection.  
  
 Tutte le dipendenze vengono acquisite dal manifesto APPX dell'app.  Oltre al file eseguibile dell'applicazione, alla DLL e a mrt100\_app.dll, che sono inclusi direttamente nel pacchetto appx, include altri due file:  
  
-   msvcr140\_app.dll, la libreria run\-time C \(CRT\) usata da mrt100\_app.dll.  Il file è incluso da un riferimento di framework nel pacchetto.  
  
-   mrt100.dll.  Questa libreria include funzioni che consentono di migliorare le prestazioni di mrt100\_app.dll, anche se la sua assenza non impedisce il funzionamento di mrt100\_app.dll.  Viene caricata dalla directory system32 sul computer locale, se presente.  
  
 Poiché la catena di strumenti .NET Native collega il codice di implementazione nell'app solo se sa che l'applicazione richiama effettivamente tale codice, è possibile non includere nell'applicazione i metadati o il codice di implementazione necessari negli scenari seguenti:  
  
-   Reflection.  
  
-   Chiamata dinamica o ad associazione tardiva.  
  
-   Serializzazione e deserializzazione.  
  
-   Interoperabilità COM.  
  
 In mancanza del codice di implementazione o dei metadati necessari, il runtime .NET Native genera un'eccezione.  È possibile evitare queste eccezioni e assicurarsi che la catena di strumenti .NET Native includa i metadati e il codice di implementazione necessari usando un [file di direttive di runtime](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md). Si tratta di un file XML che specifica gli elementi di programma il cui codice di implementazione e i cui metadati devono essere disponibili in fase di esecuzione e assegna loro criteri di runtime.  Di seguito è riportato il file delle direttive di runtime predefinito che viene aggiunto a un progetto Windows Store compilato dalla catena di strumenti .NET Native:  
  
```  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
  </Application>  
</Directives>  
  
```  
  
 Questo abilita per la reflection e la chiamata dinamica tutti i tipi, nonché i relativi membri, in tutti gli assembly nel pacchetto dell'app.  Non abilita però la reflection o l'attivazione dinamica dei tipi negli assembly della libreria di classi .NET Framework.  In molti casi, questo è sufficiente.  
  
## .NET Native e NGEN  
 Il [generatore di immagini native](../../../docs/framework/tools/ngen-exe-native-image-generator.md) \(NGEN\) compila gli assembly in codice nativo e li installa nella cache delle immagini native nel computer locale.  Tuttavia, anche se NGEN, come .NET Native, produce codice nativo, presenta alcune differenze significative rispetto a quest'ultimo:  
  
-   Se per un particolare metodo non sono disponibili immagini native, NGEN ricorre alla compilazione JIT del codice.  Questo vuol dire che le immagini native devono continuare a includere i metadati e il linguaggio intermedio nel caso in cui NGEN debba eseguire il fallback alla compilazione JIT.  .NET Native produce solo immagini native e non esegue il fallback alla compilazione JIT.  Di conseguenza, è necessario mantenere solo i metadati necessari per alcuni scenari di interoperabilità, serializzazione e reflection.  
  
-   NGEN continua a basarsi sul CLR completo per servizi quali caricamento degli assembly, comunicazione remota, interoperabilità, gestione della memoria, Garbage Collection e, se necessario, compilazione JIT.  In .NET Native molti di questi servizi non sono necessari \(compilazione JIT\) o vengono risolti in fase di compilazione e incorporati nell'assembly dell'app.  Gli altri servizi, il più importante dei quali è la Garbage Collection, sono inclusi in un runtime molto più piccolo, sottoposto a refactoring, denominato mrt100\_app.dll.  
  
-   Le immagini NGEN tendono a essere fragili.  Ad esempio, in seguito all'applicazione di una patch o alla modifica di una dipendenza, in genere è necessario ripetere la generazione di immagini native per gli assembly che se ne servono.  Ciò è particolarmente vero per gli assembly di sistema nella libreria di classi .NET Framework.  Al contrario, .NET Native consente alle applicazioni di essere servite indipendentemente le une dalle altre.  
  
## Vedere anche  
 [All'interno di .NET Native \(video su Channel 9\)](http://channel9.msdn.com/Shows/Going+Deep/Inside-NET-Native)   
 [Reflection e .NET Native](../../../docs/framework/net-native/reflection-and-net-native.md)   
 [Risoluzione dei problemi generale per .NET Native](../../../docs/framework/net-native/net-native-general-troubleshooting.md)