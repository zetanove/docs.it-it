---
title: "CallbackBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42acd302-2b62-4849-a2d1-a03084343ecd
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# CallbackBehavior
CallbackBehavior  
  
## Sintassi  
  
```  
class CallbackBehavior : Behavior  
{  
  boolean AutomaticSessionShutdown;  
  string ConcurrencyMode;  
  boolean IgnoreExtensionDataObject;  
  boolean IncludeExceptionDetailInFaults;  
  boolean MaxItemsInObjectGraph;  
  boolean UseSynchronizationContext;  
  boolean ValidateMustUnderstand;  
};  
```  
  
## Metodi  
 La classe CallbackBehavior non definisce metodi.  
  
## Proprietà  
 La classe CallbackBehavior dispone delle proprietà seguenti:  
  
### AutomaticSessionShutdown  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura  
  
 Se True, la sessione viene chiusa automaticamente quando un servizio chiude una sessione duplex.  
  
### ConcurrencyMode  
 Tipo di dati: stringa  
Tipo di accesso: sola lettura  
  
 Specifica se il servizio supporta un solo thread, più thread o chiamate rientranti.  
  
### IgnoreExtensionDataObject  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore che specifica se inviare dati di serializzazione sconosciuti in transito.  
  
### IncludeExceptionDetailInFaults  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Se attivato, i dettagli sulle eccezioni nel callback vengono collegati agli errori restituiti al servizio.  
  
### MaxItemsInObjectGraph  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di elementi consentiti in un oggetto serializzato.  
  
### UseSynchronizationContext  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se utilizzare il contesto di sincronizzazione corrente per scegliere il thread di esecuzione.  
  
### ValidateMustUnderstand  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se il sistema o l'applicazione impone l'elaborazione delle intestazioni MustUnderstand SOAP.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.CallbackBehaviorAttribute>