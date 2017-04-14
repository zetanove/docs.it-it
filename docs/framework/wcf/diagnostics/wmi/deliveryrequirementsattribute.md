---
title: "DeliveryRequirementsAttribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40c5435c-a325-4cf8-9dd0-d6e24b4a56a3
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# DeliveryRequirementsAttribute
DeliveryRequirementsAttribute  
  
## Sintassi  
  
```  
class DeliveryRequirementsAttribute : Behavior  
{  
  string QueuedDeliveryRequirements;  
  boolean RequireOrderedDelivery;  
  string TargetContract;  
};  
```  
  
## Metodi  
 La classe DeliveryRequirementsAttribute non definisce metodi.  
  
## Proprietà  
 La classe DeliveryRequirementsAttribute dispone delle proprietà seguenti:  
  
### QueuedDeliveryRequirements  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura  
  
 Specifica se l'associazione di un servizio supporta i contratti.  
  
### RequireOrderedDelivery  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se l'associazione supporta i messaggi ordinati.  
  
### TargetContract  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Contratto a cui viene applicato.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.DeliveryRequirementsAttribute>