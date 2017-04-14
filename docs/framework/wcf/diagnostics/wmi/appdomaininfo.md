---
title: "AppDomainInfo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6610b7d8-81eb-4bec-a543-9b72ad7b6f73
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# AppDomainInfo
Informazioni sul dominio applicazione  
  
## Sintassi  
  
```  
class AppDomainInfo  
{  
  sint32 AppDomainId;  
  boolean IsDefault;  
  boolean LogMalformedMessages;  
  boolean LogMessagesAtServiceLevel;  
  boolean LogMessagesAtTransportLevel;  
  TraceListener MessageLoggingTraceListeners[];  
  string Name;  
  string PerformanceCounters;  
  sint32 ProcessId;  
  string ServiceConfigPath;  
  string TraceLevel;  
  TraceListener wmiTraceListeners[];  
};  
```  
  
## Metodi  
 La classe AppDomainInfo non definisce metodi.  
  
## Proprietà  
 La classe AppDomainInfo presenta le proprietà seguenti:  
  
### AppDomainId  
 Tipo di dati: sint32  
  
 Tipo di accesso: in sola lettura  
  
 ID del dominio applicazione.  
  
### IsDefault  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se il dominio applicazione è quello predefinito.  
  
### LogMalformedMessages  
 Tipo di dati: booleano  
  
 Tipo di accesso: in lettura\/scrittura  
  
 Valore che specifica se i messaggi in formato non valido vengono registrati.  
  
### LogMessagesAtServiceLevel  
 Tipo di dati: booleano  
  
 Tipo di accesso: in lettura\/scrittura  
  
 Valore che specifica se i messaggi vengono registrati a livello di servizio \(prima della crittografia e delle trasformazioni relative al trasporto\).  
  
### LogMessagesAtTransportLevel  
 Tipo di dati: booleano  
  
 Tipo di accesso: in lettura\/scrittura  
  
 Valore che specifica se i messaggi vengono registrati a livello di trasporto.  
  
### MessageLoggingTraceListeners  
 Tipo di dati: matrice di TraceListener  
  
 Tipo di accesso: sola lettura.  
  
 Raccolta di listener di traccia in attesa sull'origine di traccia System.Wmi.MessageLogging.  
  
### Name  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome del dominio applicazione.  
  
### PerformanceCounters  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Ambito dei contatori delle prestazioni attivi nel dominio applicazione.  
  
### ProcessId  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 ID del processo.  
  
### ServiceConfigPath  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Percorso della configurazione del servizio.  
  
### TraceLevel  
 Tipo di dati: stringa  
  
 Tipo di accesso: in lettura\/scrittura  
  
 Livello di traccia dell'origine di traccia di System.Wmi.  
  
### ServiceModelTraceListeners  
 Tipo di dati: matrice di TraceListener  
  
 Tipo di accesso: sola lettura.  
  
 Raccolta di listener in attesa sull'origine di traccia System.ServiceModel.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|