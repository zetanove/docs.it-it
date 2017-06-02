---
title: "Security ETW Events | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "security events [.NET Framework]"
  - "ETW, security events (CLR)"
ms.assetid: 0ed69f73-5c01-4514-bd63-979c6e38d41d
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Security ETW Events
<a name="top"></a> Gli eventi di sicurezza vengono generati durante la verifica del nome sicuro e la verifica Authenticode.  
  
 Questa categoria include i seguenti eventi:  
  
-   [Eventi StrongNameVerificationStart\_V1 e StrongNameVerificationStop\_V1](#strongnameverificationstart_v1_and_strongnameverificationstop_v1_events)  
  
-   [Eventi AuthenticodeVerificationStart\_V1 e AuthenticodeVerificationStop\_V1](#authenticodeverificationstart_v1_and_authenticodeverificationstop_v1_events)  
  
<a name="strongnameverificationstart_v1_and_strongnameverificationstop_v1_events"></a>   
## Eventi StrongNameVerificationStart\_V1 e StrongNameVerificationStop\_V1  
 La tabella seguente illustra la parola chiave e il livello Per altre informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`SecurityKeyword` \(0x400\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`StrongNameVerificationStart_V1`|181|Inizio della verifica del nome sicuro.|  
|`StrongNameVerificationStop_V1`|182|Fine della verifica del nome sicuro.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|VerificationFlags|win:UInt32|Flag di verifica.|  
|ErrorCode|win:UInt32|Codice errore HResult.|  
|FullyQualifiedAssemblyName|win:UnicodeString|Nome completo dell'assembly.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="authenticodeverificationstart_v1_and_authenticodeverificationstop_v1_events"></a>   
## Eventi AuthenticodeVerificationStart\_V1 e AuthenticodeVerificationStop\_V1  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`SecurityKeyword` \(0x400\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`AuthenticodeVerificationStart_V1`|183|Inizio della verifica Authenticode.|  
|`AuthenticodeVerificationStop_V1`|184|Fine della verifica Authenticode.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|VerificationFlags|win:UInt32|Flag di verifica.|  
|ErrorCode|win:UInt32|Codice errore HResult.|  
|ModulePath|win:UnicodeString|Percorso del modulo.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)