---
title: "ServiceAuthorizationBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77dad8e8-fea4-4d1c-b366-2f01a2a87f78
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceAuthorizationBehavior
ServiceAuthorizationBehavior  
  
## Sintassi  
  
```  
class ServiceAuthorizationBehavior : Behavior  
{  
  boolean ImpersonateCallerForAllOperations;  
  string PrincipalPermissionMode;  
  string RoleProvider;  
  string ServiceAuthorizationManager;  
};  
```  
  
## Metodi  
 La classe ServiceAuthorizationBehavior non definisce metodi.  
  
## Proprietà  
 La classe ServiceAuthorizationBehavior dispone delle proprietà seguenti:  
  
### ImpersonateCallerForAllOperations  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Valore che controlla se il servizio tenta di eseguire una rappresentazione utilizzando le credenziali fornite dal messaggio in ingresso.  
  
### PrincipalPermissionMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Entità di protezione utilizzata per eseguire operazioni nel server.  
  
### RoleProvider  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome del provider del ruolo ASP.NET.  
  
### ServiceAuthorizationManager  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Gestore autorizzazioni utilizzato per l'autorizzazione personalizzata.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>