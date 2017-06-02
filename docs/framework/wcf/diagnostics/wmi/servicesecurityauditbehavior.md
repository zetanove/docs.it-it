---
title: "ServiceSecurityAuditBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2c5809e7-5364-44ce-bc71-848be4672e2a
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# ServiceSecurityAuditBehavior
ServiceSecurityAuditBehavior  
  
## Sintassi  
  
```  
class ServiceSecurityAuditBehavior : Behavior  
{  
  string AuditLogLocation;  
  string MessageAuthenticationAuditLevel;  
  string ServiceAuthorizationAuditLevel;  
  boolean SuppressAuditFailure;  
};  
```  
  
## Metodi  
 La classe ServiceSecurityAuditBehavior non definisce metodi.  
  
## Proprietà  
 La classe ServiceSecurityAuditBehavior dispone delle proprietà seguenti:  
  
### AuditLogLocation  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Percorso del registro di controllo.  
  
### MessageAuthenticationAuditLevel  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Tipo di livello di autenticazione dei messaggi utilizzato per registrare eventi di controllo.  
  
### ServiceAuthorizationAuditLevel  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Tipi di eventi di autorizzazione registrati nel registro di controllo.  
  
### SuppressAuditFailure  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che specifica il comportamento per l'eliminazione di errori di scrittura nel registro di controllo.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>