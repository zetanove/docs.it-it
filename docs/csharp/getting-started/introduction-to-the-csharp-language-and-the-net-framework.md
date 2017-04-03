---
title: Introduzione al linguaggio C# e a .NET Framework | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, about C# language
- Visual C#, about
ms.assetid: 0a2dff4e-cd84-42ff-8141-e89889b24081
caps.latest.revision: 32
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bfd3c08f69461d65140ef948672774a7435c326d
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-the-c-language-and-the-net-framework"></a>Introduzione al linguaggio C# e a .NET Framework
C# è un linguaggio elegante, orientato a oggetti e indipendente dai tipi che consente agli sviluppatori di creare una vasta gamma di applicazioni protette e affidabili per [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)]. È possibile usare C# per creare applicazioni client Windows, servizi Web XML, componenti distribuiti, applicazioni client-server, applicazioni di database e molto altro ancora. Visual C# fornisce un editor di codice avanzato, pratiche finestre di progettazione dell'interfaccia utente, debugger integrato e molti altri strumenti per facilitare lo sviluppo di applicazioni basate sul linguaggio C# e su [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
> [!NOTE]
>  Nella documentazione di [!INCLUDE[csprcs](../../csharp/includes/csprcs_md.md)] si presuppone che l'utente abbia una buona conoscenza dei concetti di base di programmazione. Se non si ha alcuna esperienza, può essere opportuno iniziare con [!INCLUDE[csprcsxpr](../../csharp/getting-started/includes/csprcsxpr_md.md)], che è disponibile sul Web. Sono inoltre disponibili manuali e risorse Web su C# che consentono di acquisire competenze pratiche per la programmazione.  
  
## <a name="c-language"></a>Linguaggio C#  
 La sintassi di C# è altamente espressiva, ma è anche semplice e facile da imparare. La sintassi basata sulle parentesi graffe di C# risulterà immediatamente riconoscibile per chiunque abbia familiarità con i linguaggi C, C++ o Java. Gli sviluppatori che conoscono uno di questi linguaggi di solito sono in grado di iniziare a lavorare in modo produttivo in C# dopo un breve periodo di tempo. La sintassi di C# semplifica molte delle complessità presenti in C++ e include potenti funzionalità, come tipi valore nullable, enumerazioni, delegati, espressioni lambda e accesso diretto alla memoria, che non sono disponibili in Java. C# supporta metodi e tipi generici, che garantiscono migliori prestazioni e maggior indipendenza dai tipi, nonché iteratori, che consentono ai responsabili dell'implementazione di classi Collection di definire comportamenti di iterazione personalizzati facili da usare con il codice client. Le espressioni [!INCLUDE[vbteclinqext](../../csharp/getting-started/includes/vbteclinqext_md.md)] trasformano la query fortemente tipizzata in un costrutto di linguaggio di prima classe.  
  
 Essendo un linguaggio orientato a oggetti, C# supporta i concetti di incapsulamento, ereditarietà e polimorfismo. Tutti i metodi e le variabili, incluso il metodo `Main`, ovvero il punto di ingresso dell'applicazione, vengono incapsulati all'interno delle definizioni di classe. Una classe può ereditare direttamente da un'unica classe padre, ma può implementare un numero qualsiasi di interfacce. Per evitare una ridefinizione accidentale, i metodi che eseguono l'override di metodi virtuali in una classe padre richiedono la parola chiave `override`. In C# un tipo struct è simile a una classe leggera. Si tratta di un tipo allocato nello stack che può implementare interfacce, ma non supporta l'ereditarietà.  
  
 Oltre a questi principi di base orientati a oggetti, in C# lo sviluppo di componenti software è facilitato da alcuni costrutti di linguaggio innovativi, inclusi i seguenti:  
  
-   Firme del metodo incapsulate, denominate *delegati*, che consentono le notifiche degli eventi indipendenti dai tipi.  
  
-   Proprietà, che fungono da funzioni di accesso per le variabili membro private.  
  
-   Attributi, che forniscono metadati dichiarativi sui tipi in fase di esecuzione.  
  
-   Commenti inline relativi alla documentazione XML.  
  
-   [!INCLUDE[vbteclinqext](../../csharp/getting-started/includes/vbteclinqext_md.md)] che fornisce funzionalità di query incorporate attraverso una varietà di origini dati.  
  
 Se è necessario interagire con altri componenti software Windows come oggetti COM o DLL Win32 native, in C# è possibile usare un processo denominato "Interop". Interop permette ai programmi C# di eseguire sostanzialmente qualsiasi operazione consentita a un'applicazione C++ nativa. C# supporta anche i puntatori e il concetto di codice "non sicuro" per i casi in cui l'accesso diretto alla memoria è assolutamente critico.  
  
 Il processo di compilazione di C# è più semplice rispetto a quelli di C e C++ e più flessibile rispetto a quello di Java. Non sono previsti file di intestazione separati e non è necessario che i metodi e i tipi vengano dichiarati in un ordine specifico. In un file di origine C# è possibile definire un numero qualsiasi di classi, struct, interfacce ed eventi.  
  
 Di seguito sono riportate alcune risorse aggiuntive su C#:  
  
-   Per un'introduzione generale al linguaggio, vedere il capitolo 1 di [Specifiche del linguaggio C#](../../csharp/language-reference/language-specification.md).  
  
-   Per informazioni dettagliate su aspetti specifici del linguaggio C#, vedere [Riferimenti per C#](../../csharp/language-reference/index.md).  
  
-   Per altre informazioni su [!INCLUDE[vbteclinq](../../csharp/includes/vbteclinq_md.md)], vedere [LINQ (Language-Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d).  
  
-   Per trovare gli articoli e le risorse più recenti del team di Visual C#, visitare il [Centro per sviluppatori Visual C#](http://go.microsoft.com/fwlink/?LinkId=47811).  
  
## <a name="net-framework-platform-architecture"></a>Architettura della piattaforma .NET Framework  
 I programmi C# vengono eseguiti su [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)], un componente integrale di Windows contenente un sistema di esecuzione virtuale denominato CLR (Common Language Runtime) e un insieme unificato di librerie di classi. Il CLR rappresenta l'implementazione commerciale di Microsoft dell'infrastruttura CLI (Common Language Infrastructure), uno standard internazionale che costituisce la base per la creazione di ambienti di esecuzione e sviluppo in cui linguaggi e librerie interagiscono senza problemi.  
  
 Il codice sorgente scritto in C# viene compilato in un linguaggio intermedio (Intermediate Language, IL) conforme alle specifiche CLI. Il codice e le risorse IL, come bitmap e stringhe, vengono archiviati su disco in un file eseguibile denominato assembly, in genere con estensione exe o dll. Un assembly contiene un manifesto che include informazioni sui tipi, la versione, le impostazioni cultura e i requisiti di sicurezza.  
  
 Quando viene eseguito il programma C#, l'assembly viene caricato nel CLR, che può eseguire diverse azioni in base alle informazioni contenute nel manifesto. Se i requisiti di sicurezza sono soddisfatti, il CLR esegue quindi una compilazione JIT (Just-In-Time) per convertire il codice IL in istruzioni del linguaggio macchina nativo. Il CLR offre anche altri servizi correlati alla procedura automatica di Garbage Collection e alla gestione delle eccezioni e delle risorse. Il codice eseguito dal CLR viene talvolta indicato con il termine "codice gestito" per distinguerlo dal "codice non gestito", che viene compilato nel linguaggio macchina nativo destinato a un sistema specifico. Il diagramma seguente illustra le relazioni, in fase di compilazione e di esecuzione, tra i file di codice sorgente C#, le librerie di classi di .NET Framework, gli assembly e il CLR.  
  
 ![Dal codice sorgente C&#35; all'esecuzione nel computer](../../csharp/getting-started/media/netarchitecture.png "NETarchitecture")  
  
 Una delle funzionalità chiave di [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)] è l'interoperabilità del linguaggio. Poiché il codice IL generato dal compilatore C# è conforme alle specifiche del Common Type System (CTS), può interagire con il codice generato dalle versioni .NET di Visual Basic, Visual C++ o di uno qualsiasi degli oltre 20 linguaggi conformi alle specifiche del CTS. Un singolo assembly può contenere più moduli scritti in linguaggi .NET differenti e i tipi possono fare riferimento l'uno all'altro come se fossero scritti nello stesso linguaggio.  
  
 Oltre ai servizi di runtime, [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)] include una libreria estesa contenente oltre 4000 classi, organizzate in spazi dei nomi, che offrono un'ampia gamma di utili funzionalità, dalla gestione dell'input e dell'output dei file, alla modifica delle stringhe, all'analisi XML e ai controlli Windows Form. Una tipica applicazione C# usa ampiamente la libreria di classi di [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)] per gestire le principali attività di plumbing.  
  
 Per altre informazioni su .NET Framework, vedere [Overview of the Microsoft .NET Framework](http://msdn.microsoft.com/en-us/d05daf50-00fe-45c7-8383-06fe41697355) (Cenni preliminari su Microsoft .NET Framework).  
  
## <a name="featured-book-chapters"></a>Capitoli del libro rappresentati  
 [C# Language Fundamentals](http://go.microsoft.com/fwlink/?LinkId=195416) (Nozioni fondamentali sul linguaggio C#) in [Learning C# 3.0: Master the fundamentals of C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412) (Informazioni su C# 3.0: nozioni fondamentali su C# 3.0)  
  
 [C# and .NET Programming](http://go.microsoft.com/fwlink/?LinkId=195413) (Programmazione in C# e .NET) in [Learning C# 3.0: Master the fundamentals of C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412) (Informazioni su C# 3.0: nozioni fondamentali su C# 3.0)  
  
 [Introducing C#](http://go.microsoft.com/fwlink/?LinkId=221226) (Introduzione a C#) in [Beginning Visual C# 2010](http://go.microsoft.com/fwlink/?LinkId=221214) (Introduzione a Visual C# 2010)  
  
 [Visual Studio 2008 and C# Express 2008](http://go.microsoft.com/fwlink/?LinkId=195414) (Visual Studio 2008 e C# Express 2008) in [Learning C# 3.0: Master the fundamentals of C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412) (Informazioni su C# 3.0: nozioni fondamentali su C# 3.0)  
  
## <a name="see-also"></a>Vedere anche  
 [C#](../../csharp/csharp.md)   
 [Guida introduttiva a Visual C# e Visual Basic](https://docs.microsoft.com/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)
