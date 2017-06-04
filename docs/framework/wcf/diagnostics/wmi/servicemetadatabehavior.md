---
title: "ServiceMetadataBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0f194476-72f1-467e-bdce-674306316e64
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceMetadataBehavior
ServiceMetadataBehavior  
  
## Sintassi  
  
```  
class ServiceMetadataBehavior : Behavior  
{  
  string ExternalMetadataLocation;  
  boolean HttpGetEnabled;  
  string HttpGetUrl;  
  boolean HttpsGetEnabled;  
  string HttpsGetUrl;  
};  
```  
  
## Metodi  
 La classe ServiceMetadataBehavior non definisce metodi.  
  
## Proprietà  
 La classe ServiceMetadataBehavior dispone delle proprietà seguenti:  
  
### ExternalMetadataLocation  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Imposta il percorso a cui il servizio reindirizza richieste di metadati.  
  
### HttpGetEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Definisce se il servizio pubblica il relativo WSDL all'indirizzo controllato dall'attributo `HttpGetUrl`.  
  
### HttpGetUrl  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Imposta il percorso in cui è pubblicato il WSDL del servizio per il recupero tramite HTTP.  
  
### HttpsGetEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Definisce se il servizio pubblica il relativo WSDL su HTTPS all'indirizzo controllato dall'attributo `HttpsGetUrl`.  
  
### HttpsGetUrl  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Imposta il percorso in cui è pubblicato il WSDL del servizio per il recupero tramite HTTPS.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>