---
title: "ServiceDebugBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5ec9061-1e95-43fb-b0d9-dbd0a7bc3c44
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# ServiceDebugBehavior
ServiceDebugBehavior  
  
## Sintassi  
  
```  
class ServiceDebugBehavior : Behavior  
{  
  boolean HttpHelpPageEnabled;  
  string HttpHelpPageUrl;  
  boolean HttpsHelpPageEnabled;  
  string HttpsHelpPageUrl;  
  boolean IncludeExceptionDetailInFaults;  
};  
```  
  
## Metodi  
 La classe ServiceDebugBehavior non definisce metodi.  
  
## Proprietà  
 La classe ServiceDebugBehavior dispone delle proprietà seguenti:  
  
### HttpHelpPageEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura  
  
 Definisce se il servizio pubblica il relativo WSDL all'indirizzo controllato dall'attributo `HttpGetUrl`.  
  
### HttpHelpPageUrl  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Imposta il percorso in cui è pubblicato il WSDL del servizio per il recupero tramite HTTP.  
  
### HttpsHelpPageEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Definisce se il servizio pubblica il relativo WSDL su HTTPS all'indirizzo controllato dall'attributo `HttpsGetUrl`.  
  
### HttpsHelpPageUrl  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Imposta il percorso in cui è pubblicato il WSDL del servizio per il recupero tramite HTTPS.  
  
### IncludeExceptionDetailInFaults  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se includere informazioni di eccezione nei dettagli degli errori SOAP restituiti ai client a fini di debug.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceDebugBehavior>