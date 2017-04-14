---
title: "Associazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Associazione
Associazione wmi  
  
## Sintassi  
  
```  
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## Metodi  
 La classe Binding non definisce metodi.  
  
## Proprietà  
 La classe Binding dispone delle proprietà seguenti:  
  
### BindingElements  
 Tipo di dati: matrice di BindingElement  
  
 Tipo di accesso: in sola lettura.  
  
 Raccolta di elementi di associazione implementati dall'associazione.  
  
### CloseTimeout  
 Tipo di dati: datetime  
  
 Tipo di accesso: sola lettura.  
  
 Intervallo di tempo consentito per il completamento di un'operazione di chiusura.  
  
### Name  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome dell'associazione.  
  
### Spazio dei nomi  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Spazio dei nomi XML dell'associazione.  
  
### OpenTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Intervallo di tempo consentito per il completamento di un'operazione di apertura.  
  
### ReceiveTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Intervallo di tempo consentito per il completamento di un'operazione di ricezione.  
  
### Scheme  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Schema di trasporto URI utilizzato dalla channel factory e dalla listener factory generate dall'associazione.  
  
### SendTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Intervallo di tempo consentito per il completamento di un'operazione di invio.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.Binding>