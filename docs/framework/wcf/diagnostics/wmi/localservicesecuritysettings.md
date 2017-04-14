---
title: "LocalServiceSecuritySettings | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 490aa0e5-5242-4f8d-b505-5ec6287633b4
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# LocalServiceSecuritySettings
LocalServiceSecuritySettings  
  
## Sintassi  
  
```  
class LocalServiceSecuritySettings  
{  
  boolean DetectReplays;  
  datetime InactivityTimeout;  
  datetime IssuedCookieLifetime;  
  sint32 MaxCachedCookies;  
  datetime MaxClockSkew;  
  sint32 MaxPendingSessions;  
  sint32 MaxStatefulNegotiations;  
  datetime NegotiationTimeout;  
  boolean ReconnectTransportOnFailure;  
  sint32 ReplayCacheSize;  
  datetime ReplayWindow;  
  datetime SessionKeyRenewalInterval;  
  datetime SessionKeyRolloverInterval;  
  datetime TimestampValidityDuration;  
};  
```  
  
## Metodi  
 La classe LocalServiceSecuritySettings non definisce metodi.  
  
## Proprietà  
 La classe LocalServiceSecuritySettings dispone delle proprietà seguenti:  
  
### DetectReplays  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura.  
  
 Valore booleano che specifica se gli attacchi di tipo replay contro il canale vengono rilevati e gestiti automaticamente.  
  
### InactivityTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di sessioni di sicurezza in sospeso supportate dal servizio.  
  
### IssuedCookieLifetime  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 TimeSpan che specifica la durata per tutti i nuovi cookie di sicurezza.  
  
### MaxCachedCookies  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di cookie che possono essere memorizzati nella cache.  
  
### MaxClockSkew  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 TimeSpan che specifica la differenza massima di tempo tra gli orologi di sistema delle due parti che stanno comunicando.  
  
### MaxPendingSessions  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di connessioni in sospeso nel servizio.  
  
### MaxStatefulNegotiations  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero di negoziazioni di sicurezza che possono essere attive contemporaneamente.  
  
### NegotiationTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 TimeSpan che specifica la durata massima della fase di negoziazione della protezione tra server e client.  
  
### ReconnectTransportOnFailure  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che specifica se le connessioni che utilizzano WS\-Reliable Messaging tentano la riconnessione in caso di errori del trasporto.  
  
### ReplayCacheSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero di parametri nonce utilizzato per il rilevamento degli attacchi di tipo replay.  
  
### ReplayWindow  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 TimeSpan che specifica la durata di validità dei singoli nonce dei messaggi.  
  
### SessionKeyRenewalInterval  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Timespan che specifica l'intervallo di tempo dopo il quale l'iniziatore rinnova la chiave per la sessione di sicurezza.  
  
### SessionKeyRolloverInterval  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 TimeSpan che specifica l'intervallo di tempo per il quale la chiave della sessione precedente è valida nei messaggi in arrivo durante un rinnovo della chiave.  
  
### TimestampValidityDuration  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 TimeSpan che specifica il periodo di validità di un timestamp.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>