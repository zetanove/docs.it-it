---
title: "ActivityTransfer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc40ef17-2a92-4ce2-853c-6ba8e5d571f3
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# ActivityTransfer
Evento trasferimento attività  
  
## Sintassi  
  
```  
class ActivityTransfer : WSAT_TraceEvent  
{  
  object ActivityID;  
  object RelatedActivityID;  
};  
```  
  
## Metodi  
 La classe ActivityTransfer non definisce metodi.  
  
## Proprietà  
 La classe ActivityTransfer dispone delle proprietà seguenti:  
  
### ActivityID  
  
-   Tipo di dati: oggetto                   
     Tipo di accesso: sola lettura  
  
-   ID attività  
  
### RelatedActivityID  
  
-   Tipo di dati: oggetto                   
     Tipo di accesso: sola lettura  
  
-   ID attività correlata  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel.|