---
title: "Aggiunta di un riferimento al servizio in una soluzione del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83574cf3-9803-49bc-837f-432936dc9c76
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Aggiunta di un riferimento al servizio in una soluzione del flusso di lavoro
L'aggiunta di un riferimento al servizio in un'applicazione flusso di lavoro è leggermente differente da quella in un'applicazione WCF normale.Quando si seleziona Aggiungi riferimento al servizio e si specifica l'URL del servizio, i metadati vengono scaricati e le attività personalizzate vengono generate per consentire la chiamata al servizio WCF o al servizio del flusso di lavoro WCF a cui è stato aggiunto un riferimento.Dopo avere aggiunto un riferimento al servizio, ricompilare la soluzione per compilare le attività generateche verranno visualizzate nella casella degli strumenti di Progettazione flussi di lavoro.Notare tuttavia che l'operazione viene eseguita solo se si aggiunge un riferimento al servizio all'interno di una soluzione del flusso di lavoro.Nel cast Web seguente viene mostrato come aggiungere un riferimento al servizio negli altri tipi di progetti: [Chiamata di un servizio WCF da un flusso di lavoro in un progetto Web](http://go.microsoft.com/fwlink/?LinkId=207725).  
  
 L'aggiunta di due o più riferimenti ai servizi contenenti lo stesso nome di operazione causa un problema.Le attività generate chiameranno solo la prima operazione del servizio.Per ovviare a questo problema rinominare le operazioni del servizio in modo da renderle diverse o modificano il nome di configurazione dell'endpoint all'interno di ogni attività generata.  
  
## Vedere anche  
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Procedura: creare un servizio di flusso di lavoro che chiama un altro servizio di flusso di lavoro](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-that-calls-another-workflow-service.md)   
 [Chiamata di un servizio WCF da un flusso di lavoro in un progetto Web](http://go.microsoft.com/fwlink/?LinkId=207725)