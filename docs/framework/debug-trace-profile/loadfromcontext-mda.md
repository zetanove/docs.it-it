---
title: "loadFromContext MDA | Microsoft Docs"
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
  - "MDAs (managed debugging assistants), LoadFrom context"
  - "managed debugging assistants (MDAs), LoadFrom context"
  - "LoadFrom context"
  - "LoadFromContext MDA"
ms.assetid: a9b14db1-d3a9-4150-a767-dcf3aea0071a
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# loadFromContext MDA
L'assistente al debug gestito `loadFromContext` viene attivato quando un assembly viene caricato nel contesto `LoadFrom`.  È possibile che questa situazione si verifichi in seguito alla chiamata al metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> o ad altri metodi simili.  
  
## Sintomi  
 L'utilizzo di alcuni metodi loader può determinare il caricamento degli assembly nel contesto `LoadFrom` e, a sua volta, l'utilizzo di questo contesto può causare un comportamento imprevisto per la serializzazione, l'esecuzione del cast e la risoluzione delle dipendenze.  Generalmente, per evitare questo problema è consigliabile caricare gli assembly nel contesto `Load`.  Senza questo assistente è difficile stabilire il contesto in cui è stato caricato un assembly.  
  
## Causa  
 In genere, la causa è data dal caricamento di un assembly nel contesto `LoadFrom` se il caricamento è avvenuto da un percorso esterno al contesto `Load`, quale la Global Assembly Cache o la proprietà <xref:System.AppDomainSetup.ApplicationBase%2A?displayProperty=fullName>.  
  
## Risoluzione  
 Configurare le applicazioni in modo che non siano più necessarie chiamate a <xref:System.Reflection.Assembly.LoadFrom%2A>.  A tale scopo, è possibile utilizzare le tecniche indicate di seguito.  
  
-   Installare gli assembly nella Global Assembly Cache.  
  
-   Inserire gli assembly nella directory <xref:System.AppDomainSetup.ApplicationBase%2A> di <xref:System.AppDomain>.  Nel caso del dominio predefinito, la directory <xref:System.AppDomainSetup.ApplicationBase%2A> corrisponde a quella che contiene il file eseguibile che ha avviato il processo.  In questo caso può anche essere necessario creare un nuovo <xref:System.AppDomain> se non è possibile spostare l'assembly.  
  
-   Aggiungere un percorso di sondaggio al file di configurazione dell'applicazione \(config\) o ai domini applicazione secondari se gli assembly dipendenti si trovano nelle directory figlio dell'eseguibile.  
  
 In ogni caso, è possibile modificare il codice per utilizzare il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>.  
  
## Effetto sul runtime  
 L'assistente al debug gestito non produce effetti su CLR.  Genera un report del contesto utilizzato in seguito a una richiesta di caricamento.  
  
## Output  
 L'assistente al debug gestito segnala che l'assembly è stato caricato nel contesto `LoadFrom` e specifica il percorso e il nome semplice dell'assembly.  Fornisce inoltre suggerimenti per evitare l'utilizzo del contesto `LoadFrom`.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <loadFromContext />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrata una situazione in cui è possibile attivare l'assistente al debug gestito di questo argomento.  
  
```  
using System.Reflection;  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // The following call caused the LoadFrom context to be used  
            // because the assembly is loaded using LoadFrom and the path is   
            // located outside of the Load context probing path.   
            Assembly.LoadFrom(@"C:\Text\Test.dll");  
        }  
    }  
}  
```  
  
## Vedere anche  
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)