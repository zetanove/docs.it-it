---
title: "SecurityBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ef93b6e6-3524-48a8-94d3-c8837f1872f9
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# SecurityBindingElement
SecurityBindingElement  
  
## Sintassi  
  
```  
class SecurityBindingElement : BindingElement  
{  
  string DefaultAlgorithmSuite;  
  boolean IncludeTimestamp;  
  string KeyEntropyMode;  
  LocalServiceSecuritySettings LocalServiceSecuritySettings;  
  string MessageSecurityVersion;  
  string SecurityHeaderLayout;  
};  
```  
  
## Metodi  
 La classe SecurityBindingElement non definisce metodi.  
  
## Proprietà  
 La classe SecurityBindingElement ha le proprietà seguenti:  
  
### DefaultAlgorithmSuite  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Specifica gli algoritmi da usare con l'associazione.  
  
### IncludeTimestamp  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Valore booleano che specifica se ogni messaggio contiene un timestamp.  
  
### KeyEntropyMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Origine dell'entropia usata per creare chiavi.  
  
### LocalServiceSecuritySettings  
 Tipo di dati: LocalServiceSecuritySettings  
  
 Tipo di accesso: sola lettura  
  
 Proprietà di sicurezza specifiche dell'associazione per il servizio locale.  
  
### MessageSecurityVersion  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Versione usata per la protezione del messaggio.  
  
### SecurityHeaderLayout  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Ordine degli elementi nell'intestazione di sicurezza di questa associazione.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>