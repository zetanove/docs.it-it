---
title: "Classe Operation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b19d1496-ef06-4d0c-b2ae-e728ec00cca0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Classe Operation
Operation  
  
## Sintassi  
  
```  
class Operation  
{  
  string Action;  
  boolean AsyncPattern;  
  Behavior Behaviors[];  
  boolean IsCallback;  
  boolean IsInitiating;  
  boolean IsOneWay;  
  boolean IsTerminating;  
  string MethodSignature;  
  string Name;  
  string ParameterTypes[];  
  string ReplyAction;  
  string ReturnType;  
};  
```  
  
## Metodi  
 La classe Operation non definisce metodi.  
  
## Proprietà  
 La classe Operation ha le proprietà seguenti:  
  
### Action  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Azione WS\-Addressing del messaggio di richiesta.  
  
### AsyncPattern  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica che un'operazione viene implementata in modo asincrono utilizzando una coppia di metodi `Begin` \[parentesi angolari aperte\/chiuse\] e `End` \[parentesi angolari aperte\/chiuse\] in un contratto di servizio.  
  
### Behaviors  
 Tipo di dati: matrice di Behavior  
  
 Tipo di accesso: sola lettura.  
  
 Comportamenti associati all'operazione.  
  
### IsCallback  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Restituisce True quando l'operazione è un'operazione di callback.  
  
### IsInitiating  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se il metodo implementa un'operazione in grado di avviare una sessione nel server.  
  
### IsOneWay  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se un'operazione restituisce un messaggio di risposta.  
  
### IsTerminating  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Indica se un'operazione restituisce un messaggio di risposta.  
  
### MethodSignature  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Firma del metodo dell'operazione.  
  
### Name  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Nome dell'operazione.  
  
### ParameterTypes  
 Tipo di dati: matrice di stringhe  
  
 Tipo di accesso: sola lettura.  
  
 Tipi dei parametri dell'operazione.  
  
### ReplyAction  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Valore dell'azione SOAP del messaggio di risposta dell'operazione.  
  
### ReturnType  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Tipo restituito dall'operazione.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.OperationDescription>