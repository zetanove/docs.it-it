---
title: "WSAT_TraceRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99bc7f66-1335-40d8-aa68-e754d569dc0d
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# WSAT_TraceRecord
WSAT\_TraceRecord  
  
## Sintassi  
  
```  
class WSAT_TraceRecord : WSAT_TraceEvent  
{  
  object ActivityID;  
  sint32 EventID;  
  string TraceRecord;  
};  
```  
  
## Metodi  
 La classe WSAT\_TraceRecord non definisce metodi.  
  
## Proprietà  
 La classe WSAT\_TraceRecord dispone delle proprietà seguenti:  
  
### ActivityID  
 Tipo di dati: oggetto  
Tipo di accesso: sola lettura  
  
 ID attività del record di traccia.  
  
### EventID  
 Tipo di dati: sint32  
Tipo di accesso: sola lettura  
  
 ID evento del record di traccia.  
  
### TraceRecord  
 Tipo di dati: stringa  
Tipo di accesso: sola lettura  
  
 Record di traccia  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|