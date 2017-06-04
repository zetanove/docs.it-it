---
title: "MsmqBindingElementBase | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 210d41ab-a2a4-4d7a-afd2-0916c08a4015
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# MsmqBindingElementBase
MsmqBindingElementBase  
  
## Sintassi  
  
```  
class MsmqBindingElementBase : TransportBindingElement  
{  
  string CustomDeadLetterQueue;  
  string DeadLetterQueue;  
  boolean Durable;  
  boolean ExactlyOnce;  
  sint32 MaxRetryCycles;  
  string ReceiveErrorHandling;  
  sint32 ReceiveRetryCount;  
  datetime RetryCycleDelay;  
  datetime TimeToLive;  
  boolean UseMsmqTracing;  
  boolean UseSourceJournal;  
};  
```  
  
## Metodi  
 La classe MsmqBindingElementBase non definisce alcun metodo.  
  
## Proprietà  
 La classe MsmqBindingElementBase ha le proprietà seguenti:  
  
### CustomDeadLetterQueue  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 URI che contiene il percorso della coda dei messaggi non recapitabili per ogni applicazione, in cui vengono collocati i messaggi scaduti o che non possono essere trasferiti o recapitati.  
  
### DeadLetterQueue  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Valore di enumerazione che indica il tipo di coda dei messaggi non recapitabili da utilizzare.  
  
### Durevole  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica se i messaggi elaborati da questa associazione sono durevoli o volatili.  
  
### ExactlyOnce  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che indica se i messaggi elaborati da questa associazione vengono ricevuti una sola volta.  
  
### MaxRetryCycles  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di cicli di ripetizione dei tentativi di recapito dei messaggi all'applicazione ricevente.  
  
### ReceiveErrorHandling  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni per la gestione dei messaggi non elaborabili.  
  
### ReceiveRetryCount  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di tentativi immediati su un messaggio letto dalla coda dell'applicazione.  
  
### RetryCycleDelay  
 Tipo di dati: data e ora  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica l'intervallo di tempo tra i cicli di ripetizione dei tentativi di recapitare un messaggio che è impossibile recapitare immediatamente.  
  
### TimeToLive  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica per quanto tempo i messaggi elaborati da questa associazione possono rimanere nella coda prima di scadere.  
  
### UseMsmqTracing  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che indica se i messaggi elaborati da questa associazione devono essere tracciati.  
  
### UseSourceJournal  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che indica se le copie dei messaggi elaborati da questa associazione devono essere archiviate nella coda journal di origine.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.NetMsmqBinding>   
 <xref:System.ServiceModel.MsmqBindingBase>