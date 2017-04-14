---
title: "Supporto per le query | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 093c22f5-3294-4642-857a-5252233d6796
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Supporto per le query
L'archivio di istanze del flusso di lavoro SQL registra un set di proprietà note nell'archivio.Gli utenti possono eseguire query per le istanze basate su queste proprietà.Nell'elenco seguente sono contenute alcune di queste proprietà note:  
  
-   **Site Name.** Nome del sito Web che contiene il servizio.  
  
-   **Relative Application Path.** Percorso dell'applicazione relativo al sito Web.  
  
-   **Relative Service Path.** Percorso del servizio relativo all'applicazione.  
  
-   **Service Name.** Nome del servizio.  
  
-   **Service Namespace.** Nome dello spazio dei nomi utilizzato dal servizio.  
  
-   **Current Machine.**  
  
-   **Last Machine**.Computer su cui l'istanza del servizio flusso di lavoro è stata eseguita l'ultima volta.  
  
> [!NOTE]
>  Per gli scenari indipendenti che utilizzano l'host del servizio del flusso di lavoro vengono popolate solo le ultime quattro proprietà.Per gli scenari dell'applicazione flusso di lavoro, viene popolata solo l'ultima proprietà.  
  
 L'esecuzione del flusso di lavoro fornisce valori per le prime tre proprietà.L'host del servizio del flusso di lavoro fornisce il valore per la proprietà **Suspend Reason**.L'archivio di istanze del flusso di lavoro SQL fornisce valori per la proprietà **Last Updated Machine**.  
  
 La funzionalità di archivio di istanze del flusso di lavoro SQL consente anche di specificare le proprietà personalizzate per cui si desidera archiviare i valori nel database di persistenza e che si desidera utilizzare nelle query.Per ulteriori informazioni sulle promozioni personalizzate, vedere [Estensibilità dell'archivio](../../../docs/framework/windows-workflow-foundation//store-extensibility.md).  
  
## Views  
 L'archivio di istanze contiene le visualizzazioni seguenti.Per ulteriori informazioni, vedere [Schema di database di persistenza](../../../docs/framework/windows-workflow-foundation//persistence-database-schema.md).  
  
### Visualizzazione Instances  
 La visualizzazione Instances contiene i campi seguenti:  
  
1.  **Id**  
  
2.  **PendingTimer**  
  
3.  **CreationTime**  
  
4.  **LastUpdatedTime**  
  
5.  **ServiceDeploymentId**  
  
6.  **SuspensionExceptionName**  
  
7.  **SuspensionReason**  
  
8.  **ActiveBookmarks**  
  
9. **CurrentMachine**  
  
10. **Last Machine.**  
  
11. **ExecutionStatus**  
  
12. **IsInitialized**  
  
13. **IsSuspended**  
  
14. **IsCompleted**  
  
15. **EncodingOption**  
  
16. **ReadWritePrimitiveDataProperties**  
  
17. **WriteOnlyPrimitiveDataProperties**  
  
18. **ReadWriteComplexDataProperties**  
  
19. **WriteOnlyComplexDataProperties**  
  
### Visualizzazione ServiceDeployments  
 La visualizzazione ServiceDeployments contiene i campi seguenti:  
  
1.  **SiteName**  
  
2.  **RelativeServicePath**  
  
3.  **RelativeApplicationPath**  
  
4.  **ServiceName**  
  
5.  **ServiceNamespace**  
  
### Visualizzazione InstancePromotedProperties  
 La visualizzazione InstancePromotedProperties contiene i campi seguenti.Per dettagli sulle proprietà promosse, vedere l'argomento [Estensibilità dell'archivio](../../../docs/framework/windows-workflow-foundation//store-extensibility.md).  
  
1.  **InstanceId**  
  
2.  **EncodingOption**  
  
3.  **PromotionName**  
  
4.  **Value\#** \(un intervallo di campi da **Value1** a **Value64**\).