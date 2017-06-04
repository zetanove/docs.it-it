---
title: "Autorizzazione di sicurezza per il reindirizzamento delle versioni di assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "assembly [.NET Framework], reindirizzamento dell'associazione"
  - "esecuzione affiancata, reindirizzamento dell'associazione di assembly"
ms.assetid: 24a5cdff-7ed9-4195-93f3-edf6899019fc
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Autorizzazione di sicurezza per il reindirizzamento delle versioni di assembly
Il reindirizzamento esplicito dell'associazione di assembly in un file di configurazione di un'applicazione richiede un'autorizzazione di sicurezza,  che vale per il reindirizzamento degli assembly .NET Framework e di quelli di altri produttori.  Tale autorizzazione viene concessa impostando il flag [BindingRedirects](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic) sulla [classe SecurityPermission](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic).  Agli assembly gestiti non sono concesse autorizzazioni per impostazione predefinita.  
  
 L'autorizzazione di sicurezza viene concessa alle applicazioni eseguite nell'area attendibile \(corrispondente al computer locale\) e nell'area Intranet.  Alle applicazioni eseguite nell'area Internet non è assolutamente consentito di eseguire il reindirizzamento dell'associazione di assembly.  
  
 L'autorizzazione non è richiesta se il reindirizzamento degli assembly viene eseguito in un file di criteri editore controllato dall'editore del componente oppure nel file di configurazione del computer controllato dall'amministratore.  L'autorizzazione è tuttavia richiesta per le applicazioni in cui i criteri forniti dall'editore vengono ignorati in modo esplicito mediante l'elemento [\<publisherPolicy apply\="no"\/\>](../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md) del file di configurazione dell'applicazione.  
  
 Nella tabella riportata di seguito vengono riportate le impostazioni di sicurezza predefinite per il flag **BindingRedirects**.  
  
|Area|Impostazione del flag BindingRedirects|  
|----------|--------------------------------------------|  
|Area attendibile \(computer locale\)|**ON**|  
|Area Intranet|**ON**|  
|Area Internet|**OFF**|  
|Aree non attentibili|**OFF**|  
  
 Queste impostazioni di sicurezza possono essere modificate da un amministratore per implementare il supporto o la restrizione per scenari specifici su un determinato computer.  Non sono disponibili strumenti in grado di modificare l'impostazione del flag **BindingRedirects** dall'impostazione predefinita. L'amministratore deve modificare manualmente il file Security.config sul computer dell'utente.  
  
## Vedere anche  
 [Publisher Policy Files and Side\-by\-Side Execution](http://msdn.microsoft.com/it-it/97a042be-4d72-40c3-91c0-76fd36bdf133)   
 [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)   
 [Esecuzione affiancata di diverse versioni](../../../docs/framework/deployment/side-by-side-execution.md)