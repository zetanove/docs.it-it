---
title: "Prevenzione degli attacchi di tipo &quot;replay&quot; quando un servizio WCF &#232; ospitato in una Web farm | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c2ed695-7a31-4257-92bd-9e9731b886a5
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Prevenzione degli attacchi di tipo &quot;replay&quot; quando un servizio WCF &#232; ospitato in una Web farm
Quando si utilizza la sicurezza dei messaggi WCF, si impediscono attacchi di tipo replay creando un parametro NONCE esterno al messaggio in arrivo e controllando l'oggetto `InMemoryNonceCache` interno per verificare se il parametro NONCE generato è presente.In tal caso, il messaggio viene rimosso come tipo replay.Quando un servizio WCF viene ospitato in una Web farm, poiché `InMemoryNonceCache` non viene condiviso tra i nodi della Web farm, il servizio è vulnerabile agli attacchi di tipo replay.Per mitigare questo scenario, WCF 4.5 fornisce un punto di estensibilità che consente di implementare la propria cache NONCE condivisa derivando una classe dalla classe astratta <xref:System.ServiceModel.Security.NoneCache>.  
  
## Implementazione di NoneCache  
 Per implementare la propria la cache NONCE condivisa, derivare una classe da <xref:System.ServiceModel.Security.NoneCache> ed eseguire l'override dei metodi [M:System.ServiceModel.Security.NoneCache.TryAddNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.TryAddNonce%2A> e [M:System.ServiceModel.Security.NoneCache.CheckNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.CheckNonce%2A>.Il metodo [M:System.ServiceModel.Security.NoneCache.CheckNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.CheckNonce%2A> controllerà se il parametro NONCE specificato esiste nella cache.Il metodo [M:System.ServiceModel.Security.NoneCache.TryAddNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.TryAddNonce%2A> tenterà di aggiungere un parametro NONCE alla cache.Una volta implementata, la classe viene associata creando un'istanza e assegnandola alla proprietà <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSecuritySettings.NonceCache%2A>, per il rilevamento di attacchi di tipo replay lato client, e alla proprietà <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSecuritySettings.NonceCache%2A>, per il rilevamento di attacchi di tipo replay lato server.Non esiste alcun supporto di configurazione predefinito per questa funzionalità.  
  
## Vedere anche  
 [Protezione dei messaggi](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)   
 [SymmetricSecurityBindingElement](../../../../docs/framework/wcf/diagnostics/wmi/symmetricsecuritybindingelement.md)