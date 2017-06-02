---
title: "Sicurezza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 737ec121-bfc5-4b75-a504-2d53c2c8af39
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Sicurezza
Nell'archivio di istanze del flusso di lavoro SQL vengono utilizzati i seguenti ruoli di sicurezza del database, per un accesso protetto alle informazioni sullo stato dell'istanza nel database di persistenza.  
  
-   **System.Activities.DurableInstancing.InstanceStoreUsers**.Questo ruolo dispone di autorizzazioni di accesso in lettura e scrittura a visualizzazioni pubbliche e diritti di esecuzione di stored procedure coinvolte in operazioni di creazione, caricamento e salvataggio di istanze.  
  
-   **System.Activities.DurableInstancing.InstanceStoreObservers**.Questo ruolo dispone di accesso in sola lettura alle visualizzazioni pubbliche.  
  
-   **System.Activities.DurableInstancing.WorkflowActivationUsers**.Questo ruolo dispone di diritti di esecuzione per stored procedure incluse nel processo di attivazione delle istanze.Per ulteriori informazioni sull'attivazione di istanze, vedere [Attivazione di istanze](../../../docs/framework/windows-workflow-foundation//instance-activation.md).L'account utente con il quale viene eseguito un host generico \(ad esempio il Servizio di gestione flussi di lavoro di [!INCLUDE[dublin](../../../includes/dublin-md.md)]\) deve essere aggiunto a questo ruolo del database.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]lla sicurezza per gli archivi di persistenza con Windows Server AppFabric, vedere [Configurazione della sicurezza per gli archivi di persistenza in AppFabric](http://go.microsoft.com/fwlink/?LinkId=201208)  
  
> [!CAUTION]
>  Un client con accesso ai dati dell'istanza nell'archivio di istanze dispone dell'accesso a tutte le altre istanze nello stesso archivio di istanze.L'archivio di istanze non supporta la specifica delle autorizzazioni della sicurezza a livello di istanza.È necessario creare archivi di istanze separati e mappare gruppi\/utenti diversi per disporre dell'accesso ai diversi archivi.