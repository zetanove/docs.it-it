---
title: "AsymmetricSecurityBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7bd3b6be-8f77-4927-93ae-6fa371893cca
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# AsymmetricSecurityBindingElement
AsymmetricSecurityBindingElement  
  
## Sintassi  
  
```  
class AsymmetricSecurityBindingElement : SecurityBindingElement  
{  
  string MessageProtectionOrder;  
  boolean RequireSignatureConfirmation;  
};  
```  
  
## Metodi  
 La classe AsymmetricSecurityBindingElement non definisce metodi.  
  
## Proprietà  
 La classe AsymmetricSecurityBindingElement dispone delle proprietà seguenti:  
  
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
 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>