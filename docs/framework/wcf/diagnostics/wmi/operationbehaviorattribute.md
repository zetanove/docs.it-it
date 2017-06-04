---
title: "OperationBehaviorAttribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8c9b0755-9e83-411f-bdcb-61a586022797
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# OperationBehaviorAttribute
OperationBehaviorAttribute  
  
## Sintassi  
  
```  
class OperationBehaviorAttribute : Behavior  
{  
  boolean AutoDisposeParameters;  
  string Impersonation;  
  string ReleaseInstanceMode;  
  boolean TransactionAutoComplete;  
  boolean TransactionScopeRequired;  
};  
```  
  
## Metodi  
 La classe OperationBehaviorAttribute non definisce metodi.  
  
## Proprietà  
 La classe OperationBehaviorAttribute dispone delle proprietà seguenti:  
  
### AutoDisposeParameters  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura.  
  
 Stato della funzionalità di eliminazione automatica per i parametri.  
  
### Rappresentazione  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Indica il livello di rappresentazione del chiamante supportato dall'operazione.  
  
### ReleaseInstanceMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Indica quando riciclare l'oggetto nel corso della chiamata a un'operazione.  
  
### TransactionAutoComplete  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se eseguire automaticamente il commit della transazione corrente se non si verifica alcuna eccezione non gestita.  
  
### TransactionScopeRequired  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se l'operazione richiede una transazione.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.OperationBehaviorAttribute>