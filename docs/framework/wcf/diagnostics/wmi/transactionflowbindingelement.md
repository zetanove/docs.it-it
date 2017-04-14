---
title: "TransactionFlowBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a9656fe-2400-45ca-ad79-92715c8cf190
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# TransactionFlowBindingElement
TransactionFlowBindingElement  
  
## Sintassi  
  
```  
class TransactionFlowBindingElement : BindingElement  
{  
  string IssuedTokens;  
  string TransactionProtocol;  
  boolean Transactions;  
};  
```  
  
## Metodi  
 La classe TransactionFlowBindingElement non definisce metodi.  
  
## Proprietà  
 La classe TransactionFlowBindingElement dispone delle proprietà seguenti:  
  
### IssuedTokens  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Specifica il requisito per un'intestazione dei token di sicurezza emessi \(IssuedTokens da WS\-Trust\).  
  
### TransactionProtocol  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Protocollo delle transazioni utilizzato dal servizio per il flusso delle transazioni.  
  
### Transactions  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se la transazione in ingresso è supportata.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>