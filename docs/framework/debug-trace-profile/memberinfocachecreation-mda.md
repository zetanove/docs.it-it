---
title: "memberInfoCacheCreation MDA | Microsoft Docs"
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
  - "member info cache creation"
  - "MemberInfoCacheCreation MDA"
  - "reflection, run-time errors"
  - "MDAs (managed debugging assistants), cache"
  - "cache [.NET Framework], reflection"
  - "managed debugging assistants (MDAs), cache"
  - "MemberInfo cache"
ms.assetid: 5abdad23-1335-4744-8acb-934002c0b6fe
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# memberInfoCacheCreation MDA
L'assistente al debug gestito `memberInfoCacheCreation` viene attivato in caso di creazione di una cache <xref:System.Reflection.MemberInfo>.  Questa condizione potrebbe indicare che un programma sta utilizzando funzionalità di reflection che richiedono un uso intensivo delle risorse.  
  
## Sintomi  
 Il working set di un programma aumenta perché il programma sta utilizzando funzionalità di reflection che richiedono un uso intensivo delle risorse.  
  
## Causa  
 Le operazioni di reflection che coinvolgono oggetti <xref:System.Reflection.MemberInfo> sono considerate molto esigenti in termini di risorse poiché devono leggere i metadati archiviati nelle pagine meno recenti e indicano in genere che il programma sta utilizzando un tipo di scenario con associazione tardiva.  
  
## Risoluzione  
 È possibile determinare il punto del programma in cui viene utilizzata la funzionalità di reflection abilitando questo assistente al debug gestito ed eseguendo quindi il codice in un debugger o associando un debugger al momento dell'attivazione dell'assistente al debug gestito.  In questo modo sarà possibile ottenere una traccia dello stack indicante la posizione in cui è stata creata la cache <xref:System.Reflection.MemberInfo> e da cui è possibile determinare il punto del programma in cui è utilizzata la funzionalità di reflection.  
  
 La soluzione dipende dagli obiettivi del codice.  Questo assistente al debug gestito indica che il programma sta utilizzando uno scenario con associazione tardiva.  In questo caso, è possibile analizzare le prestazioni di tale scenario oppure verificare se può essere sostituito con uno scenario con associazione anticipata.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito viene attivato per ogni cache <xref:System.Reflection.MemberInfo> creata.  L'impatto sulle prestazioni è trascurabile.  
  
## Output  
 L'assistente al debug gestito genera un messaggio che indica la creazione della cache <xref:System.Reflection.MemberInfo>.  Utilizzare un debugger per ottenere una traccia dello stack in cui è indicato il punto del programma in cui è utilizzata la funzionalità di reflection.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <memberInfoCacheCreation/>  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Questo codice di esempio attiverà l'assistente al debug gestito `memberInfoCacheCreation`.  
  
```  
using System;  
  
public class Exe  
{  
    public static void Main()  
    {  
        typeof(object).GetMethods();  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Reflection.MemberInfo>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)