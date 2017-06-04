---
title: "Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
apiname: 
  - "Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor"
apilocation: 
  - "Microsoft.VisualStudio.Activities.dll"
apitype: "Assembly"
ms.assetid: 6b44b13c-7a23-4df2-8f9f-45e2b1430002
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder..ctor
Crea un'istanza della classe [Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/microsoft-visualstudio-activities-asr-clientactivitybuilder.md).  
  
## Sintassi  
  
```csharp  
public ClientActivityBuilder(OperationDescription operationDescription, string configurationName, string proxyNamespace);  
  
```  
  
#### Parametri  
  
## Valori parametro  
 *operationDescription*  
  
 Descrive l'operazione da eseguire nell'attività del flusso di lavoro che deve essere generata, includendo il nome dell'operazione, il tipo restituito e le informazioni sul parametro.  Il valore di questo parametro non deve essere **null**.  Dovrebbe descrivere un'operazione sincrona che utilizza un contratto di messaggio e accetta un argomento con un messaggio.  Se queste condizioni non vengono soddisfatte, il risultato runtime dell'utilizzo del costruttore e gli altri metodi di questa classe non vengono definiti.  
  
 *configurationName*  
  
 Specifica il nome della configurazione dell'endpoint.  Il valore di questo parametro non deve essere **null** o vuoto.  Se queste condizioni non vengono soddisfatte, il risultato runtime dell'utilizzo del costruttore e gli altri metodi di questa classe non vengono definiti.  
  
 *proxyNamespace*  
  
 Specifica lo spazio dei nomi del servizio per l'operazione.  Il valore di questo parametro non deve essere **null** o vuoto.  Se queste condizioni non vengono soddisfatte, il risultato runtime dell'utilizzo del costruttore e gli altri metodi di questa classe non vengono definiti.  
  
## Vedere anche  
 [Microsoft.VisualStudio.Activities.Asr.ClientActivityBuilder](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/microsoft-visualstudio-activities-asr-clientactivitybuilder.md)