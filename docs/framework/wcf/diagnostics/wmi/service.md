---
title: "Servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 999806e1-6376-409e-b998-b0af391adfe7
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Servizio
Servizio  
  
## Sintassi  
  
```  
class Service  
{  
  string BaseAddresses[];  
  Behavior Behaviors[];  
  string ConfigurationName;  
  string CounterInstanceName;  
  string DistinguishedName;  
  string Extensions[];  
  string Metadata[];  
  string Name;  
  string Namespace;  
  datetime Opened;  
  Channel OutgoingChannels[];  
  sint32 ProcessId;  
};  
```  
  
## Metodi  
 La classe Service non definisce metodi.  
  
## Proprietà  
 La classe Service presenta le proprietà seguenti:  
  
### BaseAddresses  
 Tipo di dati: matrice di stringhe  
  
 Tipo di accesso: in sola lettura.  
  
 Indirizzi di base utilizzati dal servizio.  
  
### Behaviors  
 Tipo di dati: matrice di Behavior  
  
 Tipo di accesso: sola lettura.  
  
 Comportamenti associati al servizio.  
  
### ConfigurationName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 ServiceElement\_BehaviorConfiguration  
  
### CounterInstanceName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome dell'istanza del contatore delle prestazioni del servizio.  
  
### DistinguishedName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome del servizio all'indirizzo.  
  
### Extensions  
 Tipo di dati: matrice di stringhe  
  
 Tipo di accesso: sola lettura.  
  
 Contesti dell'istanza per le estensioni dell'istanza del servizio.  
  
### Metadata  
 Tipo di dati: matrice di stringhe  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni dei metadati del servizio.  
  
### Name  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome univoco del servizio.  
  
### Spazio dei nomi  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Spazio dei nomi del servizio.  
  
### Opened  
 Tipo di dati: data e ora  
  
 Tipo di accesso: sola lettura.  
  
 Ora in cui il servizio è stato aperto.  
  
### OutgoingChannels  
 Tipo di dati: matrice di Channel  
  
 Tipo di accesso: sola lettura.  
  
 Canali in uscita dall'istanza di servizio.  
  
### ProcessId  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Id del processo che ospita il servizio.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|