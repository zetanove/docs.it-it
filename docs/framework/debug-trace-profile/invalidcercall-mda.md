---
title: "invalidCERCall MDA | Microsoft Docs"
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
  - "invalid CER calls"
  - "InvalidCERCall MDA"
  - "MDAs (managed debugging assistants), CER calls"
  - "constrained execution regions"
  - "CER calls"
  - "managed debugging assistants (MDAs), CER calls"
ms.assetid: c4577410-602e-44e5-9dab-fea7c55bcdfe
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# invalidCERCall MDA
L'assistente al debug gestito `invalidCERCall` viene attivato quando all'interno del grafico dell'area a esecuzione vincolata \(CER, Constrained Execution Region\) è presente una chiamata a un metodo per il quale non esiste alcun contratto di affidabilità o il cui contratto è eccessivamente debole.  Per contratto debole si intende un contratto in cui si dichiara che l'ambito dell'errore di stato più grave è maggiore di quello dell'istanza passata alla chiamata, ovvero lo stato di <xref:System.AppDomain> o del processo può essere danneggiato o il risultato del metodo non è sempre calcolabile in modo deterministico quando viene chiamato all'interno di una CER.  
  
## Sintomi  
 ‏Risultati imprevisti durante l'esecuzione di codice in una CER.  I sintomi non sono specifici.  Potrebbe verificarsi un'eccezione <xref:System.OutOfMemoryException> imprevista, un'eccezione <xref:System.Threading.ThreadAbortException> o un'altra eccezione durante la chiamata al metodo non affidabile poiché Common Language Runtime non ha preparato il metodo in anticipo né lo ha protetto da eccezioni <xref:System.Threading.ThreadAbortException> in fase di esecuzione.  Un rischio maggiore deriva dal fatto che qualsiasi eccezione generata dal metodo in fase di esecuzione potrebbe lasciare <xref:System.AppDomain> o il processo in uno stato instabile, in contrasto con gli obiettivi di una CER.  Lo scopo della creazione di una CER è quello di evitare questo tipo di errori di stato.  Poiché la definizione di stato coerente dipende dall'applicazione, i sintomi degli errori di stato sono specifici dell'applicazione.  
  
## Causa  
 Il codice all'interno di una CER sta chiamando una funzione senza <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> o utilizzando un attributo <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> debole non compatibile con l'esecuzione all'interno di una CER.  
  
 In termini di sintassi del contratto di affidabilità, un contratto debole è un contratto che non specifica un valore di enumerazione <xref:System.Runtime.ConstrainedExecution.Consistency> o specifica un valore <xref:System.Runtime.ConstrainedExecution.Consistency> di <xref:System.Runtime.ConstrainedExecution.Consistency>, <xref:System.Runtime.ConstrainedExecution.Consistency> o <xref:System.Runtime.ConstrainedExecution.Cer>.  Ognuna di queste condizioni indica che il codice chiamato può impedire i tentativi dell'altro codice nella CER di mantenere uno stato coerente.  Le CER consentono al codice di gestire gli errori in maniera deterministica, mantenendo le invariabili interne importanti per l'applicazione e consentendo a quest'ultima di proseguire l'esecuzione in caso di errori temporanei, ad esempio le eccezioni per memoria esaurita.  
  
 L'attivazione di questo assistente al debug gestito indica che nel metodo chiamato nella CER potrebbe verificarsi un errore non previsto dal chiamante o che <xref:System.AppDomain> o il processo venga lasciato in uno stato danneggiato o irrecuperabile.  È comunque possibile che il codice chiamato venga eseguito correttamente e che il problema riguardi semplicemente la mancanza di un contratto.  Tuttavia, i problemi associati alla scrittura di codice affidabile sono difficili da individuare e l'assenza di un contratto indica in genere che il codice potrebbe non essere eseguito correttamente.  I contratti sono indicatori dell'affidabilità del codice e garantiscono inoltre che le future revisioni del codice non modificheranno tale situazione.  In altre parole, i contratti non sono semplici dettagli di implementazione ma una vera e propria dichiarazione di intenti.  
  
 Poiché in un qualsiasi metodo senza contratto o con un contratto debole può verificarsi potenzialmente un qualsiasi tipo di errore, Common Language Runtime non tenta di rimuovere tali errori imprevedibili dal metodo, ad esempio quelli introdotti dalla compilazione JIT lenta, dall'inserimento di voci di dizionario generiche o dall'interruzione dei thread.  In altre parole, quando viene attivato, questo assistente al debug gestito indica che Common Language Runtime non ha incluso il metodo chiamato nella CER definita. Il grafico delle chiamate è stato terminato in questo nodo, per evitare che la preparazione di questo sottoalbero impedisca la rilevazione dell'eventuale errore.  
  
## Risoluzione  
 Aggiungere un contratto di affidabilità valido alla funzione o evitare di utilizzare tale funzione di chiamata.  
  
## Effetto sul runtime  
 La chiamata di un contratto debole da una CER potrebbe impedire il completamento delle operazioni relative alla CER,  con conseguente danneggiamento dello stato del processo <xref:System.AppDomain>.  
  
## Output  
 Di seguito è riportato un esempio di output generato da questo assistente al debug gestito.  
  
 `Method 'MethodWithCer', while executing within a constrained execution region, makes a call at IL offset 0x000C to 'MethodWithWeakContract', which does not have a sufficiently strong reliability contract and might cause non-deterministic results.`  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <invalidCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>   
 <xref:System.Runtime.ConstrainedExecution>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)