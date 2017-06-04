---
title: "HttpTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 088a7bce-6bb2-4839-ad74-f68d4b1aa0f9
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# HttpTransportBindingElement
HttpTransportBindingElement  
  
## Sintassi  
  
```  
class HttpTransportBindingElement : TransportBindingElement  
{  
  boolean AllowCookies;  
  string AuthenticationScheme;  
  boolean BypassProxyOnLocal;  
  string HostNameComparisonMode;  
  boolean KeepAliveEnabled;  
  sint32 MaxBufferSize;  
  string ProxyAddress;  
  string ProxyAuthenticationScheme;  
  string Realm;  
  string TransferMode;  
  boolean UnsafeConnectionNtlmAuthentication;  
  boolean UseDefaultWebProxy;  
};  
```  
  
## Metodi  
 La classe HttpTransportBindingElement non definisce metodi.  
  
## Proprietà  
 La classe HttpTransportBindingElement dispone delle proprietà seguenti:  
  
### AllowCookies  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura.  
  
 Valore che indica se il client accetta cookie e li propaga alle richieste future.  
  
### AuthenticationScheme  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Schema di autenticazione utilizzato per autenticare le richieste del client da elaborare mediante un listener HTTP.  
  
### BypassProxyOnLocal  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica se i proxy vengono ignorati per gli indirizzi locali.  
  
### HostnameComparisonMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica se viene utilizzato il nome host per raggiungere il servizio in caso di corrispondenza dell'URI.  
  
### KeepAliveEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Se attivato, le connessioni HTTP vengono mantenute attive indipendentemente dal livello di attività.  
  
### MaxBufferSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Dimensione massima del pool di buffer.  
  
### ProxyAddress  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 URI contenente l'indirizzo del proxy da utilizzare per le richieste HTTP.  
  
### ProxyAuthenticationScheme  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Schema di autenticazione utilizzato per autenticare le richieste del client da elaborare mediante un listener HTTP.  
  
### Realm  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Area di autenticazione.  
  
### TransferMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Valore che specifica se i messaggi vengono memorizzati nel buffer o trasmessi in caso di richiesta o risposta.  
  
### UnsafeConnectionNtlmAuthentication  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica se sul server è attivata la condivisione di connessioni non sicure.  
  
### UseDefaultWebProxy  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica se vengono utilizzate impostazioni proxy a livello di computer invece delle specifiche impostazioni utente.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>