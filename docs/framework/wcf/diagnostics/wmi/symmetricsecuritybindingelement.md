---
title: "SymmetricSecurityBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b2e182b6-c041-4d80-a926-6058068d9f79
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# SymmetricSecurityBindingElement
SymmetricSecurityBindingElement  
  
## Sintassi  
  
```  
class SymmetricSecurityBindingElement : SecurityBindingElement  
{  
  string MessageProtectionOrder;  
  boolean RequireSignatureConfirmation;  
};  
```  
  
## Metodi  
 La classe SymmetricSecurityBindingElement non definisce metodi.  
  
## Proprietà  
 La classe SymmetricSecurityBindingElement dispone delle proprietà seguenti:  
  
### MessageProtectionOrder  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Ordine di crittografia e firma dei messaggi per questa associazione.  
  
### RequireSignatureConfirmation  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se l'associazione richiede la conferma della firma.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>