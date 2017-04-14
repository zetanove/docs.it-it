---
title: "Endpoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe63370d-81a1-40f3-97c2-59cb357c78d2
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Endpoint
Endpoint  
  
## Sintassi  
  
```  
class Endpoint  
{  
  string Address;  
  string AddressHeaders[];  
  string AddressIdentity;  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  Binding Binding;  
  string ContractName;  
  string CounterInstanceName;  
  string ListenUri;  
  string Name;  
  sint32 ProcessId;  
  Contract ref;  
};  
```  
  
## Metodi  
 La classe Endpoint definisce il metodo seguente.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[GetOperationCounterInstanceName](../../../../../docs/framework/wcf/diagnostics/wmi/getoperationcounterinstancename.md)|Recupera il nome dell'istanza del contatore delle prestazioni dell'operazione.|  
  
## Proprietà  
 La classe Endpoint ha le proprietà seguenti:  
  
### Address  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 URI che contiene l'indirizzo dell'endpoint.  
  
### AddressHeaders  
 Tipo di dati: matrice di stringhe  
  
 Tipo di accesso: sola lettura  
  
 Raccolta di intestazioni di indirizzo associato a questo endpoint.  
  
### AddressIdentity  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Identità dell'endpoint.  
  
### AppDomainId  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 ID del dominio applicazione che ospita l'endpoint.  
  
### Comportamenti  
 Tipo di dati: matrice di Behavior  
  
 Tipo di accesso: sola lettura  
  
 Raccolta dei comportamenti implementati da questo endpoint.  
  
### Binding  
 Tipo di dati: associazione  
  
 Tipo di accesso: sola lettura  
  
 Associazione usata da questo endpoint.  
  
### ContractName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Stringa che specifica il contratto che viene esposto da questo endpoint.  
  
### CounterInstanceName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Nome dell'istanza del contatore delle prestazioni dell'endpoint.  
  
### ListenUri  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 URI sul quale resta in attesa l'endpoint.  
  
### Nome  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Nome univoco di questo endpoint.  
  
### ProcessId  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 ID del processo che ospita l'endpoint.  
  
### ref  
 Tipo di dati: contratto  
  
 Tipo di accesso: sola lettura  
  
 Contratto esposto dall'endpoint.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|