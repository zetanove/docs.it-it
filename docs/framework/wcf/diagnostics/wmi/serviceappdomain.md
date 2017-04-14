---
title: "ServiceAppDomain | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f28e5186-a66d-46c1-abe9-b50e07f8cb4f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceAppDomain
Esegue il mapping di un servizio a un dominio applicazione.  
  
## Sintassi  
  
```  
class ServiceAppDomain  
{  
  Service ref;  
  AppDomainInfo ref;  
};  
```  
  
## Metodi  
 La classe ServiceAppDomain non definisce metodi.  
  
## Proprietà  
 La classe ServiceAppDomain presenta le proprietà seguenti:  
  
### ref  
 Tipo di dati: servizio               
 Qualificatori: chiave  
  
 Tipo di accesso: sola lettura  
  
 Il servizio di questo dominio applicazione.  
  
### ref  
 Tipo di dati: AppDomainInfo               
 Qualificatori: chiave  
  
 Tipo di accesso: sola lettura  
  
 Contiene proprietà del dominio applicazione.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|