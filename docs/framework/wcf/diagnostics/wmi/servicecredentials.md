---
title: "ServiceCredentials | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9c780793-4785-46f7-add9-ac1ebeadb614
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceCredentials
ServiceCredentials  
  
## Sintassi  
  
```  
class ServiceCredentials : Behavior  
{  
  string ClientCertificate;  
  string IssuedTokenAuthentication;  
  string Peer;  
  string SecureConversationAuthentication;  
  string ServiceCertificate;  
  string UserNameAuthentication;  
  string WindowsAuthentication;  
};  
```  
  
## Metodi  
 La classe ServiceCredentials non definisce metodi.  
  
## Proprietà  
 La classe ServiceCredentials dispone delle proprietà seguenti:  
  
### ClientCertificate  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura  
  
 Impostazioni di provisioning e autenticazione dei certificati client per il servizio.  
  
### IssuedTokenAuthentication  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni correnti di autenticazione del token rilasciato per il servizio.  
  
### Peer  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni correnti di provisioning e autenticazione delle credenziali utilizzate dagli endpoint di trasporto del peer.  
  
### SecureConversationAuthentication  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Specifica le impostazioni correnti per le conversazioni protette.  
  
### ServiceCertificate  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Certificato associato al servizio.  
  
### UserNameAuthentication  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni di nome utente e password per il servizio.  
  
### WindowsAuthentication  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni di autenticazione Windows per il servizio.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceCredentials>