---
title: "ServiceTimeoutsBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4412525d-a3cc-4eae-b3e8-a50ce766d09d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# ServiceTimeoutsBehavior
ServiceTimeoutsBehavior  
  
## Sintassi  
  
```  
class ServiceTimeoutsBehavior : Behavior  
{  
  datetime TransactionTimeout;  
};  
```  
  
## Metodi  
 La classe ServiceTimeoutsBehavior non definisce metodi.  
  
## Proprietà  
 La classe ServiceTimeoutsBehavior dispone della proprietà seguente:  
  
### TransactionTimeout  
 Tipo di dati: data e ora  
  
 Tipo di accesso: in sola lettura  
  
 Periodo entro il quale una transazione deve essere completata.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceTimeoutsElement>