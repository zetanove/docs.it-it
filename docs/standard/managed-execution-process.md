---
title: "Processo di esecuzione gestita | Microsoft Docs"
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
  - "linguaggio del codice sorgente"
  - "codice, processo di esecuzione gestita"
  - "runtime, processo di esecuzione gestita"
  - "compilazione di codice sorgente, processo di esecuzione gestita"
  - "processo di esecuzione gestita"
  - "Common Language Runtime, processo di esecuzione gestita"
ms.assetid: 476b03dc-2b12-49a7-b067-41caeaa2f533
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Processo di esecuzione gestita
<a name="introduction"></a> Il processo di esecuzione gestita include i passaggi seguenti, descritti in modo dettagliato più avanti in questo argomento:  
  
1.  [Scelta di un compilatore](#choosing_a_compiler).  
  
     Per sfruttare i vantaggi offerti da Common Language Runtime, è necessario usare uno o più compilatori di linguaggio destinati al runtime.  
  
2.  [Compilazione del codice in MSIL](#compiling_to_msil).  
  
     La compilazione converte il codice sorgente in codice MSIL \(Microsoft Intermediate Language\) e genera i metadati necessari.  
  
3.  [Compilazione del codice MSIL in codice nativo](#compiling_msil_to_native_code).  
  
     In fase di esecuzione, un compilatore JIT converte il codice MSIL in codice nativo. Durante questa compilazione, il codice deve superare un processo di verifica che esamina il codice MSIL e i metadati per determinare se può essere considerato indipendente dai tipi.  
  
4.  [Esecuzione del codice](#running_code).  
  
     Common Language Runtime fornisce l'infrastruttura che permette l'esecuzione e i servizi che possono essere usati durante l'esecuzione.  
  
<a name="choosing_a_compiler"></a>   
## Scelta di un compilatore  
 Per sfruttare i vantaggi offerti da Common Language Runtime \(CLR\), è necessario usare uno o più compilatori di linguaggio destinati al runtime, come Visual Basic, C\#, Visual C\+\+, F\# o uno dei molti compilatori di terze parti come Eiffel, Perl o COBOL.  
  
 Poiché si tratta di un ambiente di esecuzione multilinguaggio, il runtime supporta un'ampia gamma di tipi di dati e funzionalità per i linguaggi. Il compilatore di linguaggio usato determina le funzionalità di runtime disponibili, che verranno usate per progettare il codice. È il compilatore, non Common Language Runtime, a determinare la sintassi che deve essere utilizzata dal codice. Per essere completamente utilizzabile dai componenti scritti in altri linguaggi, il componente deve avere tipi esportati che espongono solo le funzionalità per i linguaggi incluse in [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../docs/standard/language-independence-and-language-independent-components.md) \(CLS\). È possibile usare l'attributo <xref:System.CLSCompliantAttribute> per garantire che il codice sia conforme a CLS. Per altre informazioni, vedere [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../docs/standard/language-independence-and-language-independent-components.md).  
  
 [Torna all'inizio](#introduction)  
  
<a name="compiling_to_msil"></a>   
## Compilazione in MSIL  
 Quando si esegue la compilazione in codice gestito, il compilatore converte il codice sorgente in codice MSIL \(Microsoft Intermediate Language\), che è un set di istruzioni indipendente dalla CPU che può essere convertito in modo efficiente in codice nativo. Il codice MSIL include istruzioni per il caricamento, l'archiviazione, l'inizializzazione e la chiamata di metodi su oggetti, nonché per operazioni aritmetiche e logiche, flusso di controllo, accesso diretto alla memoria, gestione delle eccezioni e altre ancora. Prima che sia possibile eseguire il codice, il codice MSIL deve essere convertito in codice specifico della CPU, in genere da un [compilatore JIT \(Just\-In\-Time\)](#compiling_msil_to_native_code). Poiché Common Language Runtime fornisce uno o più compilatori JIT per ogni architettura di computer supportata, lo stesso set di codice MSIL può essere compilato tramite JIT ed eseguito su qualsiasi architettura supportata.  
  
 Quando un compilatore produce codice MSIL, genera anche i metadati. I metadati descrivono i tipi nel codice, con la definizione di ogni tipo, le firme dei membri di ogni tipo, i membri cui fa riferimento il codice e altri dati usati dal runtime in fase di esecuzione. Il codice MSIL e i metadati sono contenuti in un file eseguibile portabile \(PE\) che si basa \(estendendolo\) sul formato Microsoft PE e COFF \(Common Object File Format\) pubblicato, usato tradizionalmente per il contenuto eseguibile. Questo formato di file, che adatta il codice MSIL o il codice nativo e i metadati, permette al sistema operativo di riconoscere le immagini Common Language Runtime. La presenza di metadati nel file insieme a codice MSIL permette al codice di descrivere se stesso, per cui non sono necessari un linguaggio di definizione dell'interfaccia né librerie dei tipi. Il runtime individua ed estrae dal file i metadati al momento necessario durante l'esecuzione.  
  
 [Torna all'inizio](#introduction)  
  
<a name="compiling_msil_to_native_code"></a>   
## Compilazione del codice MSIL in codice nativo  
 Prima di poter essere eseguito, il codice MSIL \(Microsoft Intermediate Language\) deve essere compilato con Common Language Runtime in codice nativo per l'architettura di computer di destinazione.[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] offre due strumenti per eseguire questa conversione:  
  
-   A .NET Framework just\-in\-time \(JIT\) compiler.  
  
-   .NET Framework [Ngen.exe \(Native Image Generator\)](../../docs/framework/tools/ngen-exe-native-image-generator.md).  
  
### Compilazione tramite il compilatore JIT  
 La compilazione JIT converte il codice MSIL in codice nativo su richiesta in fase di esecuzione dell'applicazione, durante il caricamento e l'esecuzione del contenuto di un assembly. Poiché Common Language Runtime fornisce un compilatore JIT per ogni architettura CPU supportata, gli sviluppatori possono compilare un set di assembly MSIL da compilare tramite JIT ed eseguire su più computer con diverse architetture di computer. Tuttavia, se il codice gestito chiama API native specifiche della piattaforma o una libreria di classi specifica della piattaforma, viene eseguito solo su tale sistema operativo.  
  
 La compilazione JIT tiene conto della possibilità che parte del codice non venga mai chiamata durante l'esecuzione. Invece di usare tempo e memoria per convertire tutto il codice MSIL in un file PE in codice nativo, la compilazione converte solo quello necessario durante l'esecuzione e archivia il codice nativo risultante in memoria, perché sia accessibile per le chiamate successive nel contesto del processo. Il caricatore crea e collega uno stub a ogni metodo in un tipo durante il caricamento e l'inizializzazione del tipo. Quando un metodo viene chiamato per la prima volta, lo stub passa il controllo al compilatore JIT, che converte in codice nativo il codice MSIL per il metodo e modifica lo stub in modo da puntare direttamente al codice nativo generato. Di conseguenza, le successive chiamate del metodo compilato tramite JIT passano direttamente al codice nativo.  
  
### Generazione di codice in fase di installazione mediante NGen.exe  
 Poiché il compilatore JIT converte il codice MSIL di un assembly in codice nativo quando vengono chiamati singoli metodi definiti nell'assembly, influisce negativamente sulle prestazioni in fase di esecuzione. Nella maggior parte dei casi, queste prestazioni inferiori sono comunque accettabili. Un aspetto ancora più importante è che il codice generato dal compilatore JIT è associato al processo che ha attivato la compilazione e non può essere condiviso tra più processi. Per permettere la condivisione del codice generato tra più chiamate di un'applicazione o tra più processi che condividono un set di assembly, Common Language Runtime supporta una modalità di compilazione anticipata. Questa modalità di compilazione usa [Ngen.exe \(Native Image Generator\)](../../docs/framework/tools/ngen-exe-native-image-generator.md) per convertire assembly MSIL in codice nativo in modo molto simile al compilatore JIT. Tuttavia, il funzionamento di Ngen.exe differisce da quello del compilatore JIT per tre aspetti:  
  
-   Esegue la conversione da codice MSIL a codice nativo prima di eseguire l'applicazione invece che durante l'esecuzione dell'applicazione.  
  
-   Compila un intero assembly per volta, invece di un metodo per volta.  
  
-   Mantiene il codice generato nella cache delle immagini native come file su disco.  
  
### Verifica del codice  
 Come parte della compilazione in codice nativo, il codice MSIL deve superare un processo di verifica, a meno che un amministratore non abbia definito criteri di sicurezza che permettono di evitare la verifica del codice. La verifica esamina il codice MSIL e i metadati per determinare se il codice è indipendente dai tipi, che significa che accede solo alle posizioni di memoria cui è autorizzato ad accedere. L'indipendenza dai tipi isola gli oggetti gli uni dagli altri e aiuta a proteggerli da danni accidentali o intenzionali. Inoltre, garantisce l'applicazione affidabile delle restrizioni di sicurezza.  
  
 Il runtime si basa sul fatto che le affermazioni seguenti siano vere per il codice verificabile come indipendente dai tipi:  
  
-   Un riferimento a un tipo è strettamente compatibile con il tipo a cui viene fatto riferimento.  
  
-   Vengono richiamate in un oggetto solo le operazioni definite in modo appropriato.  
  
-   Le identità sono quello che sostengono di essere.  
  
 Durante il processo di verifica, il codice MSIL viene esaminato nel tentativo di confermare che possa accedere alle posizioni di memoria e chiamare metodi solo attraverso i tipi definiti in modo appropriato. Ad esempio, il codice non può permettere l'accesso ai campi di un oggetto in un modo che consenta l'overrun delle posizioni di memoria. La verifica esamina inoltre il codice per determinare se il codice MSIL sia stato generato correttamente, perché quello generato in modo non corretto può causare una violazione delle regole di indipendenza dai tipi. Il processo di verifica passa un set di codice indipendente dai tipi ben definito e passa solo il codice indipendente dai tipi. Tuttavia, parte del codice indipendente dai tipi potrebbe non superare la verifica a causa di alcune limitazioni del processo di verifica e alcuni linguaggi, in base alla progettazione, non producono codice verificabile come indipendente dai tipi. Se i criteri di sicurezza richiedono codice indipendente dai tipi ma il codice non supera la verifica, al momento dell'esecuzione verrà generata un'eccezione.  
  
 [Torna all'inizio](#introduction)  
  
<a name="running_code"></a>   
## Esecuzione del codice  
 Common Language Runtime fornisce l'infrastruttura che permette l'esecuzione gestita e i servizi che possono essere usati durante l'esecuzione. Prima che un metodo possa essere eseguito, deve essere compilato in codice specifico del processore. Ogni metodo per cui è stato generato codice MSIL viene compilato tramite JIT quando viene chiamato per la prima volta, quindi viene eseguito. Alla successiva esecuzione del metodo, viene eseguito il codice nativo esistente compilato tramite JIT. Il processo di compilazione JIT e di esecuzione del codice viene ripetuto fino al completamento dell'esecuzione.  
  
 Durante l'esecuzione, il codice gestito riceve servizi come Garbage Collection, sicurezza, interoperabilità con codice non gestito, supporto per il debug tra linguaggi e supporto migliorato per distribuzione e controllo delle versioni.  
  
 In Microsoft [!INCLUDE[winxp](../../includes/winxp-md.md)] e [!INCLUDE[windowsver](../../includes/windowsver-md.md)] il caricatore del sistema operativo controlla la presenza di moduli gestiti esaminando un bit nell'intestazione COFF. Il bit impostato denota un modulo gestito. Se il caricatore rileva moduli gestiti, carica mscoree.dll e `_CorValidateImage` e `_CorImageUnloading` notificano al caricatore l'avvenuto caricamento o scaricamento delle immagini dei moduli gestiti.`_CorValidateImage` esegue le azioni seguenti:  
  
1.  Assicura che il codice sia codice gestito valido.  
  
2.  Modifica il punto di ingresso nell'immagine in un punto di ingresso nel runtime.  
  
 In Windows a 64 bit `_CorValidateImage` modifica l'immagine presente in memoria trasformandola dal formato PE32 al formato PE32\+.  
  
 [Torna all'inizio](#introduction)  
  
## Vedere anche  
 [Panoramica](../../docs/framework/get-started/overview.md)   
 [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../docs/standard/language-independence-and-language-independent-components.md)   
 [Metadati e componenti auto\-descrittivi](../../docs/standard/metadata-and-self-describing-components.md)   
 [Ilasm.exe \(IL Assembler\)](../../docs/framework/tools/ilasm-exe-il-assembler.md)   
 [Security](../../docs/standard/security/index.md)   
 [Interoperating with Unmanaged Code](../../docs/framework/interop/index.md)   
 [Distribuzione](../../docs/framework/deployment/net-framework-and-applications.md)   
 [Assembly in Common Language Runtime](../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [Domini applicazione](../../docs/framework/app-domains/application-domains.md)