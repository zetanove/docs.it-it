---
title: "Attacchi di tipo replay | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Attacchi di tipo replay
Un *attacco di tipo replay* si verifica quando un utente malintenzionato copia un flusso di messaggi tra due parti e lo riproduce verso una o più parti.Se l'attacco non viene respinto, i computer colpiti elaborano il flusso come se i messaggi fossero legittimi. Ciò determina una serie di conseguenze negative, ad esempio la creazione di ordini ridondanti di un articolo.  
  
## Vulnerabilità delle associazioni agli attacchi di tipo reflection  
 Un *attacco di tipo reflection* consiste nella riproduzione di un messaggio verso il mittente sottoforma di risposta proveniente dal destinatario.Il meccanismo standard di *rilevamento di attacchi di tipo replay* di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] non è in grado di gestire automaticamente questo tipo di attacco.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], tuttavia, gli attacchi di tipo reflection vengono respinti per impostazione predefinita. Infatti, il modello dei servizi di tale piattaforma prevede l'aggiunta di un ID di messaggio firmato ai messaggi di richiesta nonché un'intestazione firmata `relates-to` nei messaggi di risposta.Risulta di conseguenza impossibile riprodurre il messaggio di richiesta come risposta.Negli scenari che prevedono messaggi affidabili gli attacchi di tipo reflection vengono respinti per i motivi seguenti:  
  
-   Lo schema dei messaggi di creazione di sequenza non corrisponde a quello di creazione di sequenza di risposta.  
  
-   Per le sequenze simplex, i messaggi di sequenza inviati dal client non possono essere riprodotti verso il client stesso in quanto quest'ultimo non è in grado di riconoscere tali messaggi.  
  
-   Per le sequenze duplex, i due ID di sequenza devono essere univoci.Inoltre, ogni intestazione e corpo della sequenza è firmato. Risulta pertanto impossibile riprodurre un messaggio di sequenza in uscita sottoforma di messaggio di sequenza in ingresso.  
  
 Le uniche associazioni vulnerabili agli attacchi di tipo reflection sono quelle in cui non viene applicata la specifica WS\-Addressing, ovvero le associazioni personalizzate in cui la funzionalità WS\-Addressing è stata disattivata e in cui si utilizza la protezione basata su chiavi simmetriche.Per impostazione predefinita, l'associazione <xref:System.ServiceModel.BasicHttpBinding> non applica la specifica WS\-Addressing. Tuttavia, tale associazione presenta una modalità di sicurezza basata su chiavi simmetriche in grado di respingere gli attacchi di questo tipo.  
  
 Affinché le associazioni personalizzate siano in grado di respingere gli attacchi di tipo reflection è necessario richiedere l'utilizzo di intestazioni WS\-Addressing oppure evitare di stabilire contesti di sicurezza.  
  
## Web farm: attacco basato sulla riproduzione di richieste verso più nodi  
 Si consideri il caso di un client che utilizza un servizio implementato in una Web farm.In questo caso un utente malintenzionato può riprodurre una richiesta inviata a un determinato nodo della farm verso un'altro nodo della stessa farm.Inoltre, se un servizio viene riavviato, la cache di riproduzione viene svuotata. Ciò consente a un utente malintenzionato di riprodurre una richiesta.Nota: una cache di riproduzione contiene i valori di firma dei messaggi usati o già visualizzati e impedisce che tali firme vengano utilizzate più di una volta, respingendo in questo modo gli attacchi di tipo replay.Tuttavia, le funzionalità di una cache di riproduzione non vengono estese all'intera Web farm.  
  
 Segue un elenco di alcune prevenzioni possibili.  
  
-   Utilizzare una modalità di sicurezza dei messaggi che preveda token del contesto di sicurezza con stato. La funzionalità di conversazione protetta può essere attiva o disattivata.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
-   Configurare il servizio in modo che utilizzi un meccanismo di sicurezza a livello di trasporto.  
  
## Vedere anche  
 [Considerazioni sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [Diffusione di informazioni](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [Elevazione dei privilegi](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [Denial of Service \(Negazione del servizio\)](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [Manomissioni](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)