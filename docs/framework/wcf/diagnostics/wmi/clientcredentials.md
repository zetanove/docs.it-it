---
title: "ClientCredentials | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 41dffd6b-8f14-4fed-aefb-2a1bb168efb3
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ClientCredentials
ClientCredentials  
  
## Sintassi  
  
```  
class ClientCredentials : Behavior  
{  
  string ClientCertificate;  
  string HttpDigest;  
  string IssuedToken;  
  string Peer;  
  string ServiceCertificate;  
  boolean SupportInteractive;  
  string UserName;  
  string Windows;  
};  
```  
  
## Metodi  
 La classe ClientCredentials non definisce metodi.  
  
## Proprietà  
 La classe ClientCredentials dispone delle proprietà seguenti:  
  
### ClientCertificate  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura  
  
 Certificato X.509 utilizzato dal client per l'autenticazione per il servizio.  
  
### HttpDigest  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Credenziale digest HTTP corrente.  
  
### IssuedToken  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Indirizzo e associazione dell'endpoint utilizzati per contattare il servizio locale del token di sicurezza.  
  
### Peer  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Credenziali utilizzate dal nodo peer per l'autenticazione con gli altri nodi nella rete.  
  
### ServiceCertificate  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Certificato X.509 del servizio.  
  
### SupportInteractive  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che specifica se la credenziale supporta negoziazioni interattive.  
  
### UserName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome utente e password utilizzati dal client per l'autenticazione per il servizio.  
  
### Windows  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Credenziali Windows utilizzate dal client per l'autenticazione per il servizio.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ClientCredentials>