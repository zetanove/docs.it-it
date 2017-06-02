---
title: "ServiceBehaviorAttribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5faa266f-587f-4e03-828d-1c7dd5acfe65
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# ServiceBehaviorAttribute
ServiceBehaviorAttribute  
  
## Sintassi  
  
```  
class ServiceBehaviorAttribute : Behavior  
{  
  boolean AutomaticSessionShutdown;  
  string ConcurrencyMode;  
  string ConfigurationName;  
  boolean IgnoreExtensionDataObject;  
  boolean IncludeExceptionDetailInFaults;  
  string InstanceContextMode;  
  sint32 MaxItemsInObjectGraph;  
  string Name;  
  string Namespace;  
  boolean ReleaseServiceInstanceOnTransactionComplete;  
  boolean TransactionAutoCompleteOnSessionClose;  
  string TransactionIsolationLevel;  
  datetime TransactionTimeout;  
  boolean UseSynchronizationContext;  
  boolean ValidateMustUnderstand;  
};  
```  
  
## Metodi  
 La classe ServiceBehaviorAttribute non definisce metodi.  
  
## Proprietà  
 La classe ServiceBehaviorAttribute dispone delle proprietà seguenti:  
  
### AutomaticSessionShutdown  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura  
  
 Indica se chiudere automaticamente una sessione quando un client chiude una sessione di output.  
  
### ConcurrencyMode  
 Tipo di dati: stringa  
Tipo di accesso: sola lettura  
  
 Indica se un servizio supporta un solo thread, più thread o chiamate rientranti.  
  
### ConfigurationName  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome della configurazione di servizio.  
  
### IgnoreExtensionDataObject  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se inviare dati di serializzazione sconosciuti in transito.  
  
### IncludeExceptionDetailInFaults  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se includere informazioni di eccezione nei dettagli degli errori SOAP restituiti ai client a fini di debug.  
  
### InstanceContextMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Specifica quando viene creato un nuovo oggetto servizio.  
  
### MaxItemsInObjectGraph  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di elementi consentiti in un oggetto serializzato.  
  
### Name  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Attributo nome del servizio in WSDL.  
  
### Spazio dei nomi  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Spazio dei nomi di destinazione del servizio in WSDL.  
  
### ReleaseServiceInstanceOnTransactionComplete  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se l'oggetto servizio viene riciclato al completamento della transazione corrente.  
  
### TransactionAutoCompleteOnSessionClose  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se alla chiusura della sessione corrente vengono completate le transazioni in sospeso.  
  
### TransactionIsolationLevel  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Specifica il livello di isolamento della transazione.  
  
### TransactionTimeout  
 Tipo di dati: data e ora  
  
 Tipo di accesso: sola lettura.  
  
 Periodo entro il quale una transazione deve essere completata.  
  
### UseSynchronizationContext  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se utilizzare il contesto di sincronizzazione corrente per scegliere l'esecuzione del thread.  
  
### ValidateMustUnderstand  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Specifica se il sistema o l'applicazione impone l'elaborazione delle intestazioni MustUnderstand SOAP.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceBehaviorAttribute>