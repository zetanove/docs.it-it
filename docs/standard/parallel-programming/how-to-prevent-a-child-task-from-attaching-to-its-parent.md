---
title: "How to: Prevent a Child Task from Attaching to its Parent | Microsoft Docs"
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
  - "tasks, preventing attachments"
ms.assetid: c0fb85d4-9e80-4905-9f65-29acc54201c4
caps.latest.revision: 5
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# How to: Prevent a Child Task from Attaching to its Parent
In questo documento viene illustrato come impedire a un'attività figlio di essere associata all'attività padre.  Impedendo a un'attività figlio di venir associata al proprio padre è utile quando si chiama un componente scritto da terze parti e che utilizza attività.  Ad esempio, un componente di terze parti che utilizza l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> per creare un oggetto <xref:System.Threading.Tasks.Task%601> o <xref:System.Threading.Tasks.Task> può causare problemi nel codice se è in esecuzione prolungata o genera un'eccezione non gestita.  
  
## Esempio  
 Nell'esempio seguente vengono confrontati gli effetti dell'utilizzo delle opzioni predefinite agli effetti di impedire a un'attività figlio di venir connessa al padre.  Nell'esempio viene creato un oggetto <xref:System.Threading.Tasks.Task> che chiama una libreria di terze parti che utilizza un oggetto <xref:System.Threading.Tasks.Task>.  La libreria di terze parti utilizza l'opzione <xref:System.Threading.Tasks.TaskCreationOptions> per creare l'oggetto <xref:System.Threading.Tasks.Task>.  L'applicazione utilizza l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> per creare l'attività padre.  Questa opzione indica al runtime di rimuovere la specifica <xref:System.Threading.Tasks.TaskCreationOptions> nelle attività figlio.  
  
 [!code-csharp[TPL_DenyChildAttach#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_denychildattach/cs/denychildattach.cs#1)]
 [!code-vb[TPL_DenyChildAttach#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_denychildattach/vb/denychildattach.vb#1)]  
  
 Poiché un'attività padre non viene completata finché tutte le attività figlio non vengono completate, un'attività figlio di lunga durata può ridurre notevolmente le prestazioni dell'applicazione generale.  In questo esempio, quando l'applicazione utilizza le opzioni predefinite per creare l'attività padre, l'attività figlio deve essere completata prima che l'attività padre venga completata.  Quando l'applicazione utilizza l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName>, l'elemento figlio non è connesso al padre.  Di conseguenza, l'applicazione può eseguire un'operazione aggiuntiva al termine dell'attività padre e prima deve attendere la fine dell'attività figlio.  
  
## Compilazione del codice  
 Copiare il codice di esempio e incollarlo in un progetto di Visual Studio, oppure incollarlo in un file denominato `DenyChildAttach.cs` \(`DenyChildAttach.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) e quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe DenyChildAttach.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe DenyChildAttach.vb**  
  
## Programmazione efficiente  
  
## Vedere anche  
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)