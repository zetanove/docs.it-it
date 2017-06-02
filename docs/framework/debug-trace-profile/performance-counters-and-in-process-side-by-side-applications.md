---
title: "Performance Counters and In-Process Side-By-Side Applications | Microsoft Docs"
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
  - "performance counters"
  - "performance counters,and in-process side-by-side applications"
  - "performance,.NET Framework applications"
  - "performance monitoring,counters"
ms.assetid: 6888f9be-c65b-4b03-a07b-df7ebdee2436
caps.latest.revision: 26
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 26
---
# Performance Counters and In-Process Side-By-Side Applications
Tramite Performance Monitor \(Perfmon.exe\) è possibile distinguere i contatori delle prestazioni in base al runtime.  Questo argomento descrive come modificare il Registro di sistema per abilitare questa funzionalità.  
  
## Comportamento predefinito  
 Per impostazione predefinita, Performance Monitor visualizza i contatori delle prestazioni in base all'applicazione.  Esistono tuttavia due scenari in cui ciò risulta problematico:  
  
-   Quando si esegue il monitoraggio di due applicazioni aventi lo stesso nome.  Ad esempio, se entrambe le applicazioni sono denominate myapp.exe, una verrà visualizzata come **myapp** e l'altra come **myapp\#1** nella colonna **Istanza**.  In questo caso risulta difficile abbinare un contatore delle prestazioni a una determinata applicazione.  Non è chiaro se i dati raccolti per **myapp\#1** si riferiscono al primo myapp.exe o al secondo myapp.exe.  
  
-   Quando un'applicazione utilizza più istanze di Common Language Runtime.  [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] supporta scenari affiancati in\-process. In altre parole, un solo processo o applicazione può caricare più istanze di Common Language Runtime.  Se una sola applicazione denominata myapp.exe carica due istanze di runtime, per impostazione predefinita queste verranno definite nella colonna **Istanza** come **myapp** e **myapp\#1**.  In questo caso non è chiaro se **myapp** e **myapp\#1** si riferiscono a due applicazioni con lo stesso nome o alla stessa applicazione con due runtime.  Se più applicazioni con lo stesso nome caricano più runtime, l'ambiguità risulta essere ancora maggiore.  
  
 Per eliminare questa ambiguità è possibile impostare una chiave del Registro di sistema.  Per le applicazioni sviluppate tramite [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], questa modifica del Registro di sistema comporta l'aggiunta di un identificatore del processo seguito da un identificatore dell'istanza di runtime al nome dell'applicazione nella colonna **Istanza**.  Anziché *application* o *application*\#1, l'applicazione viene identificata come *application*\_`p`*processID*\_`r`*runtimeID* nella colonna **Istanza**.  Se un'applicazione è stata sviluppata utilizzando una versione precedente di Common Language Runtime, tale istanza viene rappresentata come *application\_*`p`*processID*, purché sia stato installato [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
## Contatori delle prestazioni per le applicazioni affiancate in\-process  
 Per gestire i contatori delle prestazioni per più versioni di Common Language Runtime ospitate in un'unica applicazione è necessario modificare una sola impostazione della chiave del Registro di sistema, come mostrato nella tabella seguente.  
  
|||  
|-|-|  
|Nome della chiave|HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\.NETFramework\\Performance|  
|Nome del valore|ProcessNameFormat|  
|Tipo di valore|REG\_DWORD|  
|Valore|1 \(0x00000001\)|  
  
 Il valore 0 per `ProcessNameFormat` indica che il comportamento predefinito è abilitato; ovvero, Perfmon.exe visualizza i contatori delle prestazioni in base all'applicazione.  Quando si imposta questo valore su 1, Perfmon.exe risolve l'ambiguità relativa a più versioni di un'applicazione e fornisce i contatori delle prestazioni in base al runtime.  Qualsiasi altro valore per l'impostazione della chiave del Registro di sistema `ProcessNameFormat` è non supportato ed è riservato per un utilizzo futuro.  
  
 Una volta aggiornata l'impostazione della chiave del Registro di sistema `ProcessNameFormat`, è necessario riavviare Perfmon.exe o qualsiasi altro utente dei contatori delle prestazioni in modo che la nuova funzionalità di denominazione dell'istanza funzioni correttamente.  
  
 Nell'esempio seguente viene mostrato come modificare il valore `ProcessNameFormat` a livello di codice.  
  
 [!code-csharp[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/cs/regsetting1.cs#1)]
 [!code-vb[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/vb/regsetting1.vb#1)]  
  
 Quando si applica questa modifica al Registro di sistema, Perfmon.exe visualizza i nomi delle applicazioni indirizzate a [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] come *application*\_`p`*processID*\_`r`*runtimeID*, dove *application* è il nome dell'applicazione, *processID* è l'identificatore del processo dell'applicazione e *runtimeID* è un identificatore di Common Language Runtime.  Ad esempio, se un'applicazione denominata myapp.exe carica due istanze di Common Language Runtime, Perfmon.exe può identificare un'istanza come myapp\_p1416\_r10 e l'altra come myapp\_p3160\_r10.  L'identificatore di runtime si limita a eliminare l'ambiguità fra i runtime all'interno di un processo. Non fornisce nessun'altra informazione sul runtime. Ad esempio, l'identificatore di runtime non è correlato in alcun modo alla versione o alla SKU del runtime.  
  
 Se è stato installato [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], la modifica del Registro di sistema interessa anche le applicazioni sviluppate utilizzando versioni precedenti di .NET Framework.  Queste applicazioni vengono visualizzate in Perfmon.exe come *application\_*`p`*processID*, dove *application* è il nome dell'applicazione e *processID* è l'identificatore del processo.  Ad esempio, se si esegue il monitoraggio dei contatori delle prestazioni di due applicazioni denominate myapp.exe, una potrebbe essere visualizzata come myapp\_p23900 e l'altra come myapp\_p24908.  
  
> [!NOTE]
>  L'identificatore del processo elimina l'ambiguità della risoluzione di due applicazioni con lo stesso nome che utilizzano versioni precedenti di runtime.  Per le versioni precedenti non è necessario utilizzare un identificatore di runtime, poiché le versioni precedenti di Common Language Runtime non supportano scenari affiancati.  
  
 Se [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] non è presente o è stato disinstallato, l'impostazione della chiave del Registro di sistema non ha alcun effetto.  Ciò significa che due applicazioni con lo stesso nome continueranno a essere identificate in Perfmon.exe come *application* e *application\#1* \(ad esempio, **myapp** e **myapp\#1**\).