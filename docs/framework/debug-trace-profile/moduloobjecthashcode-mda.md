---
title: "moduloObjectHashcode MDA | Microsoft Docs"
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
  - "managed debugging assistants (MDAs), hashcode modulus"
  - "Modulo object hash code"
  - "moduloObjectHashcode MDA"
  - "hashcode modulus"
  - "MDAs (managed debugging assistants), hashcode modulus"
  - "GetHashCode method"
  - "modulus of hashcodes"
ms.assetid: b45366ff-2a7a-4b8e-ab01-537b72e9de68
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# moduloObjectHashcode MDA
L'assistente al debug gestito `moduloObjectHashcode` modifica il comportamento della classe <xref:System.Object> in modo che venga eseguita un'operazione modulo sul codice hash restituito dal metodo <xref:System.Object.GetHashCode%2A>.  Il modulo predefinito per questo assistente al debug gestito è 1, che fa sì che <xref:System.Object.GetHashCode%2A> restituisca 0 per tutti gli oggetti.  
  
## Sintomi  
 Dopo il passaggio a una nuova versione di Common Language Runtime \(CLR\), un programma non viene più eseguito correttamente:  
  
-   Il programma sta ottenendo l'oggetto errato da <xref:System.Collections.Hashtable>.  
  
-   L'ordine di enumerazione da <xref:System.Collections.Hashtable> contiene una modifica che causa l'interruzione del programma.  
  
-   Due oggetti precedentemente uguali non risultano più uguali.  
  
-   Due oggetti precedentemente non uguali adesso risultano uguali.  
  
## Causa  
 È possibile che il programma stia ottenendo l'oggetto errato da <xref:System.Collections.Hashtable> poiché l'implementazione del metodo <xref:System.Object.Equals%2A> sulla classe per la chiave in <xref:System.Collections.Hashtable> verifica l'uguaglianza degli oggetti confrontando i risultati della chiamata al metodo <xref:System.Object.GetHashCode%2A>.  I codici hash non devono essere utilizzati per verificare l'uguaglianza degli oggetti poiché due oggetti potrebbero avere lo stesso codice hash anche se i rispettivi campi contengono valori differenti.  Questi conflitti tra codici hash, sebbene rari, possono comunque verificarsi.  In questo caso, da una ricerca in <xref:System.Collections.Hashtable> risulterebbe che due chiavi diverse siano invece uguali e verrebbe quindi restituito l'oggetto errato da <xref:System.Collections.Hashtable>.  Per motivi di prestazioni, l'implementazione di <xref:System.Object.GetHashCode%2A> può variare tra le diverse versioni di Common Language Runtime. Pertanto, un conflitto che non si verifica in una versione potrebbe verificarsi nelle versioni successive.  Abilitare questo assistente al debug gestito per verificare la presenza di bug nel codice in caso di conflitto tra i codici hash.  Quando questo assistente al debug gestito è abilitato, il metodo <xref:System.Object.GetHashCode%2A> restituisce 0, causando un conflitto tra tutti i codici hash.  L'unico effetto dell'abilitazione di questo assistente al debug gestito sul programma consiste in un rallentamento dell'esecuzione.  
  
 L'ordine di enumerazione da <xref:System.Collections.Hashtable> può variare tra le diverse versioni di Common Language Runtime se viene modificato l'algoritmo utilizzato per calcolare i codici hash per la chiave.  Per verificare se il programma presenta una dipendenza dall'ordine di enumerazione delle chiavi o dei valori in una tabella hash, è possibile abilitare questo assistente al debug gestito.  
  
## Risoluzione  
 Non utilizzare mai codici hash come sostituti dell'identità dell'oggetto.  Implementare l'override del metodo <xref:System.Object.Equals%2A?displayProperty=fullName> per non confrontare i codici hash.  
  
 Non creare dipendenze dall'ordine di enumerazione delle chiavi o dei valori nelle tabelle hash.  
  
## Effetto sul runtime  
 Quando questo assistente al debug gestito è abilitato, l'esecuzione delle applicazioni risulta più lenta.  L'assistente recupera semplicemente il codice hash che sarebbe stato restituito e restituisce invece il resto della divisione modulo.  
  
## Output  
 Per questo assistente al debug gestito non esiste alcun output.  
  
## Configurazione  
 L'attributo `modulus` specifica il modulo utilizzato sul codice hash.  Il valore predefinito è 1.  
  
```  
<mdaConfig>  
  <assistants>  
    <moduloObjectHashcode modulus="1" />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Object.GetHashCode%2A?displayProperty=fullName>   
 <xref:System.Object.Equals%2A?displayProperty=fullName>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)