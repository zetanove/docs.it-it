---
title: "MsmqTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c89f073-9ed3-4025-a8c5-13535a0f526b
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# MsmqTransportBindingElement
MsmqTransportBindingElement  
  
## Sintassi  
  
```  
class MsmqTransportBindingElement : MsmqBindingElementBase  
{  
  sint32 MaxPoolSize;  
  string QueueTransferProtocol;  
  boolean UseActiveDirectory;  
};  
```  
  
## Metodi  
 La classe MsmqTransportBindingElement non definisce alcun metodo.  
  
## Proprietà  
 La classe MsmqTransportBindingElement ha le proprietà seguenti:  
  
### MaxPoolSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: in sola lettura.  
  
 Dimensione massima del pool che contiene oggetti di messaggi MSMQ interni.  
  
### QueueTransferProtocol  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Valore di enumerazione che indica il trasporto per il canale delle comunicazioni in coda utilizzato da questa associazione.  
  
### UseActiveDirectory  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Restituisce un valore booleano che indica se convertire gli indirizzi delle code mediante Active Directory.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>