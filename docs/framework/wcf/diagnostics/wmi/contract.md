---
title: "Contract | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aa00f6b3-7e1f-4213-841a-206463fca20b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Contract
Contract  
  
## Sintassi  
  
```  
class Contract  
{  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  string Name;  
  string Namespace;  
  Operation Operations[];  
  sint32 ProcessId;  
  Contract ref;  
  string SessionMode;  
  string Type;  
};  
```  
  
## Metodi  
 La classe Contract non definisce metodi.  
  
## Proprietà  
 La classe Contract ha le proprietà seguenti:  
  
### AppDomainId  
 Tipo di dati: sint32  
  
 Tipo di accesso: in sola lettura.  
  
 ID del dominio applicazione che ospita il contratto.  
  
### Behaviors  
 Tipo di dati: matrice di Behavior  
  
 Tipo di accesso: sola lettura.  
  
 Comportamenti associati al contratto.  
  
### Name  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome del contratto in WSDL.  
  
### Namespace  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Spazio dei nomi dell'elemento `portType` in WSDL.  
  
### Operations  
 Tipo di dati: matrice di Operation  
  
 Tipo di accesso: sola lettura.  
  
 Operazioni di questo contratto.  
  
### ProcessId  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 ID del processo che ospita il contratto.  
  
### ref  
 Tipo di dati: contratto  
  
 Tipo di accesso: sola lettura.  
  
 Tipo di callback se il contratto è duplex.  
  
### SessionMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Indica se il contratto richiede che l'associazione di questo contratto utilizzi le sessioni del canale.  
  
### Type  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Tipo del contratto.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ContractDescription>