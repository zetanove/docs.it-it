---
title: "bindingFailure MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "binding failure"
  - "binding, failures"
  - "MDAs (managed debugging assistants), binding failures"
  - "assemblies [.NET Framework], binding failures"
  - "managed debugging assistants (MDAs), binding failures"
  - "BindingFailure MDA"
ms.assetid: 26ada5af-175c-4576-931a-9f07fa1723e9
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# bindingFailure MDA
L'assistente al debug gestito `bindingFailure` viene attivato quando si verifica un errore nel caricamento di un assembly.  
  
## Sintomi  
 Il codice ha tentato di caricare un assembly mediante un riferimento statico o uno dei metodi loader, quale <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> o <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>.  L'assembly non viene caricato e viene generata un'eccezione <xref:System.IO.FileNotFoundException> o<xref:System.IO.FileLoadException>.  
  
## Causa  
 Quando il runtime non è in grado di caricare un assembly, si verifica un errore di associazione  che può essere il risultato di una delle situazioni riportate di seguito.  
  
-   Common Language Runtime \(CLR\) non è in grado di trovare l'assembly richiesto.  Le ragioni possono essere diverse, ad esempio la mancata installazione dell'assembly o la configurazione non corretta dell'applicazione per l'individuazione dell'assembly.  
  
-   Uno scenario comune relativo a questo problema consiste nel passaggio di un tipo a un altro dominio applicazione che richiede a CLR il caricamento dell'assembly contenente il tipo in questione nell'altro dominio applicazione.  È possibile che il runtime non riesca a caricare l'assembly se l'altro dominio applicazione è configurato diversamente dal quello originale.  I due domini applicazione possono ad esempio presentare valori diversi per la proprietà <xref:System.AppDomain.BaseDirectory%2A>.  
  
-   L'assembly richiesto è danneggiato o non è un assembly.  
  
-   Il codice relativo al tentativo di caricamento dell'assembly non dispone delle autorizzazioni di sicurezza dell'accesso al codice necessarie per caricare assembly.  
  
-   Le credenziali utente non specificano le autorizzazioni necessarie per la lettura del file.  
  
## Risoluzione  
 Il primo passaggio consiste nel determinare la ragione per la quale CLR non è stato in grado di effettuare l'associazione all'assembly richiesto.  Numerose possono essere le ragioni per cui il runtime non è stato in grado di trovare o di caricare l'assembly richiesto, quali ad esempio quelle illustrate negli scenari della sezione Causa.  Per eliminare la causa dell'errore di associazione, sono consigliate le azioni indicate di seguito.  
  
-   Determinare la causa utilizzando i dati forniti dall'assistente al debug gestito `bindingFailure`:  
  
    -   Eseguire [Fuslogvw.exe \(Assembly Binding Log Viewer\)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md) per leggere i log degli errori prodotti dal binder di assembly.  
  
    -   Determinare se l'assembly si trova nella posizione richiesta.  Nel caso dei metodi <xref:System.Reflection.Assembly.LoadFrom%2A> e <xref:System.Reflection.Assembly.LoadFile%2A>, l'individuazione della posizione richiesta è semplice.  Nel caso del metodo <xref:System.Reflection.Assembly.Load%2A>, che esegue l'associazione mediante l'identità dell'assembly, è necessario cercare gli assembly corrispondenti all'identità specifica nella Global Assembly Cache e nel percorso di sondaggio della proprietà <xref:System.AppDomain.BaseDirectory%2A> del dominio applicazione.  
  
-   Risolvere la causa in base ai risultati del passaggio precedente.  Le opzioni di risoluzione possibili sono le seguenti:  
  
    -   Installare l'assembly richiesto nella Global Assembly Cache e chiamare il metodo  <xref:System.Reflection.Assembly.Load%2A> per caricare l'assembly in base all'identità.  
  
    -   Copiare l'assembly richiesto nella directory dell'applicazione e chiamare il metodo <xref:System.Reflection.Assembly.Load%2A> per caricare l'assembly in base all'identità.  
  
    -   Riconfigurare il dominio applicazione in cui si è verificato l'errore di associazione per includere il percorso dell'assembly modificando la proprietà <xref:System.AppDomain.BaseDirectory%2A> o aggiungendo percorsi di sondaggio privati.  
  
    -   Modificare l'elenco di controllo dell'accesso per il file in modo da consentirne la lettura all'utente connesso.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  Si limita a generare un report dei dati relativi agli errori di associazione.  
  
## Output  
 L'assistente in questione segnala l'assembly per il quale non è riuscito il caricamento, inclusi il percorso richiesto e\/o il nome visualizzato, il contesto di associazione, il dominio applicazione in cui è stato richiesto il caricamento e la ragione dell'errore.  
  
 È possibile che, se non è disponibile in CLR, il nome visualizzato o il percorso richiesto non sia definito.  Se la chiamata non riuscita è relativa al metodo <xref:System.Reflection.Assembly.Load%2A>, è probabile che il runtime non sia stato in grado di determinare il nome visualizzato dell'assembly.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <bindingFailure />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrata una situazione in cui è possibile attivare l'assistente al debug gestito di questo argomento.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Reflection;  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // This call attempts to load a nonexistent assembly.  
            // The call will throw a System.IO.FileNotFound exception  
            // and cause the activation of the bindingFailure MDA   
            // if it is registered.  
            Assembly.Load("NonExistentAssembly");  
        }  
    }  
}  
```  
  
## Vedere anche  
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)