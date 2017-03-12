---
title: "Introduction to the C# Language and the .NET Framework | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# language, about C# language"
  - "Visual C#, about"
ms.assetid: 0a2dff4e-cd84-42ff-8141-e89889b24081
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# Introduction to the C# Language and the .NET Framework
C\# è un linguaggio orientato a oggetti elegante e indipendente dai tipi che consente agli sviluppatori di compilare svariate applicazioni protette e affidabili eseguibili sulla piattaforma [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)].  È possibile utilizzare C\# per creare applicazioni client Windows, servizi Web XML, componenti distribuiti, applicazioni client\-server, applicazioni di database e molto altro ancora.  Visual C\# fornisce un editor di codice avanzato, pratiche finestre di progettazione dell'interfaccia utente, debugger integrato e molti altri strumenti per facilitare lo sviluppo di applicazioni basate sul linguaggio C\# e su [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)].  
  
> [!NOTE]
>  Nella documentazione di [!INCLUDE[csprcs](../../csharp/includes/csprcs-md.md)] si presuppone che l'utente abbia una buona conoscenza dei concetti di base della programmazione.  Se non si dispone di alcuna esperienza di programmazione, si consiglia di iniziare con [!INCLUDE[csprcsxpr](../../csharp/getting-started/includes/csprcsxpr-md.md)], disponibile sul Web.  Sono inoltre disponibili manuali e risorse Web che consentono di acquisire competenze pratiche per la programmazione C\#.  
  
## Linguaggio C\#  
 La sintassi C\# è altamente espressiva, sebbene sia anche molto semplice da imparare.  Inoltre, essendo basata sull'utilizzo delle parentesi graffe, risulterà immediatamente riconoscibile per chiunque abbia familiarità con i linguaggi C, C\+\+ o Java.  In genere, gli sviluppatori che conoscono uno qualsiasi di questi linguaggi saranno in grado di iniziare a lavorare in modo produttivo in C\# dopo un periodo minimo di apprendimento.  La sintassi C\# semplifica molte delle complessità presenti in C\+\+ e fornisce al tempo stesso alcune potenti funzionalità, quali tipi di valore nullable, enumerazioni, delegati, espressioni lambda e accesso diretto alla memoria, non disponibili in Java.  Sono supportati metodi e tipi generici, che garantiscono migliori prestazioni e maggior indipendenza dai tipi, nonché iteratori, che consentono ai responsabili dell'implementazione di classi Collection di definire comportamenti di iterazione personalizzati facilmente utilizzabili nel codice client.  Le espressioni [!INCLUDE[vbteclinqext](../../csharp/getting-started/includes/vbteclinqext-md.md)] rendono la query fortemente tipizzata un costrutto di linguaggio di prima categoria.  
  
 Essendo un linguaggio orientato a oggetti, C\# supporta i concetti di incapsulamento, ereditarietà e polimorfismo.  Tutti i metodi e le variabili, incluso il metodo `Main`, che rappresenta il punto di ingresso dell'applicazione, vengono incapsulati all'interno delle definizioni di classe.  Una classe può ereditare direttamente da un'unica classe padre, ma può implementare un numero qualsiasi di interfacce.  Per evitare una ridefinizione accidentale, i metodi che eseguono l'override di metodi virtuali in una classe padre richiedono la parola chiave `override`.  In C\# una struttura è simile a una classe leggera \(lightweight\). Si tratta di un tipo allocato nello stack che può implementare interfacce ma non supporta l'ereditarietà.  
  
 Oltre a supportare questi principi di base della programmazione orientata a oggetti, in C\# sono disponibili alcuni costrutti di linguaggio innovativi che facilitano lo sviluppo di componenti software, ad esempio i seguenti:  
  
-   Firme del metodo incapsulate, denominate *delegati*, che consentono l'invio di notifiche degli eventi indipendenti dai tipi.  
  
-   Proprietà, che vengono utilizzate come funzioni di accesso per le variabili membro private.  
  
-   Attributi, che forniscono metadati dichiarativi sui tipi in fase di esecuzione.  
  
-   Commenti inline relativi alla documentazione XML.  
  
-   [!INCLUDE[vbteclinqext](../../csharp/getting-started/includes/vbteclinqext-md.md)] che fornisce funzionalità di query incorporate attraverso una varietà di origini dati.  
  
 Se è necessario interagire con altri componenti software Windows quali oggetti COM o DLL Win32 native, in C\# è possibile utilizzare un processo denominato "Interop", che permette ai programmi C\# di eseguire sostanzialmente qualsiasi operazione consentita a un'applicazione C\+\+ nativa.  C\# supporta anche i puntatori e il concetto di codice "non sicuro" per i casi nei quali l'accesso diretto alla memoria è assolutamente critico.  
  
 Il processo di compilazione di C\# è più semplice rispetto a quelli in C e C\+\+ e più flessibile rispetto a quello in Java.  Non sono previsti file di intestazione separati e non è necessario che i metodi e i tipi vengano dichiarati in un ordine specifico.  In un file di origine C\# è possibile definire un numero qualsiasi di classi, strutture, interfacce ed eventi.  
  
 Di seguito sono riportate alcune risorse aggiuntive in cui vengono fornite informazioni sul linguaggio C\#:  
  
-   Per informazioni di carattere generale sul linguaggio, vedere il capitolo 1 di [Specifiche del linguaggio C\#](../../csharp/language-reference/language-specification.md).  
  
-   Per informazioni dettagliate su aspetti specifici del linguaggio C\#, vedere [Riferimenti per C\#](../../csharp/language-reference/index.md).  
  
-   Per ulteriori informazioni su [!INCLUDE[vbteclinq](../../csharp/includes/vbteclinq-md.md)], vedere [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md).  
  
-   Per trovare gli articoli e le risorse più recenti del team di Visual C\#, vedere [Centro per sviluppatori Visual C\#](http://go.microsoft.com/fwlink/?LinkId=47811).  
  
## Architettura della piattaforma .NET Framework  
 I programmi C\# vengono eseguiti sulla piattaforma [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)], un componente interno di Windows contenente un Virtual Execution System denominato CLR \(Common Language Runtime\) e un insieme unificato di librerie di classi.  CLR rappresenta l'implementazione commerciale Microsoft dell'infrastruttura CLI \(Common Language Infrastructure\), uno standard internazionale utilizzato per la creazione di ambienti di esecuzione e sviluppo in cui linguaggi e librerie interagiscono senza problemi.  
  
 Il codice sorgente scritto in C\# viene compilato in un linguaggio intermedio \(IL\) conforme alle specifiche CLI.  Il codice IL e le risorse, quali bitmap e stringhe, vengono archiviati su disco in un file eseguibile denominato assembly, in genere con estensione exe o dll.  Un assembly contiene un manifesto in cui vengono fornite informazioni sui tipi dell'assembly, la versione, le impostazioni cultura e i requisiti di sicurezza.  
  
 Al momento dell'esecuzione di un programma C\#, l'assembly viene caricato nel CLR, che può eseguire diverse azioni in base alle informazioni contenute nel manifesto.  Quindi, se i requisiti di sicurezza sono soddisfatti, il CLR esegue una compilazione JIT \(Just\-In\-Time\) per convertire il codice IL in istruzioni del linguaggio macchina nativo.  Vengono inoltre forniti altri servizi correlati alla procedura automatica di Garbage Collection, alla gestione delle eccezioni e alla gestione delle risorse.  Il codice eseguito dal CLR viene talvolta indicato con il termine "codice gestito" per distinguerlo dal "codice non gestito", che rappresenta il codice compilato nel linguaggio macchina nativo destinato a un sistema specifico.  Nel diagramma riportato di seguito vengono illustrate le relazioni, a livello di fase di compilazione e fase di esecuzione, tra i file di codice sorgente C\#, le librerie di classi di .NET Framework, gli assembly e il CLR.  
  
 ![Dal codice C&#35; all'esecuzione nel computer](../../csharp/getting-started/media/netarchitecture.png "NETarchitecture")  
  
 Una delle funzionalità più importanti di [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] è l'interoperabilità del linguaggio.  Poiché il codice IL prodotto dal compilatore C\# è conforme alle specifiche del sistema di tipi comuni, il codice IL generato da C\# può interagire con il codice generato dalle versioni .NET di Visual Basic, Visual C\+\+ o di uno qualsiasi degli oltre 20 linguaggi conformi alle specifiche del sistema di tipi comuni.  Un singolo assembly può contenere più moduli scritti in linguaggi .NET differenti ed è possibile definire riferimenti incrociati tra i tipi come se tali moduli fossero scritti nello stesso linguaggio.  
  
 Oltre ai servizi di runtime, in [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] è inoltre disponibile una libreria contenente oltre 4000 classi, organizzate in base allo spazio dei nomi, che forniscono un'ampia gamma di utili funzionalità, dalla gestione dell'input e dell'output dei file, alla modifica delle stringhe, l'analisi XML e la gestione dei controlli Windows Form.  Una tipica applicazione C\# utilizza la libreria di classi di [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] per gestire le principali attività di routine.  
  
 Per ulteriori informazioni su .NET Framework, vedere [Overview of the Microsoft .NET Framework](http://msdn.microsoft.com/it-it/d05daf50-00fe-45c7-8383-06fe41697355).  
  
## Capitoli del libro rappresentati  
 [C\# Language Fundamentals](http://go.microsoft.com/fwlink/?LinkId=195416) in [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
 [C\# and .NET Programming](http://go.microsoft.com/fwlink/?LinkId=195413) in [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
 [Introduzione a C\#](http://go.microsoft.com/fwlink/?LinkId=221226) in [Introduzione a Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
 [Visual Studio 2008 and C\# Express 2008](http://go.microsoft.com/fwlink/?LinkId=195414) in [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
## Vedere anche  
 [C\#](../../csharp/csharp.md)   
 [Guida introduttiva a Visual C\# e Visual Basic](/visual-studio/ide/getting-started-with-visual-csharp-and-visual-basic)