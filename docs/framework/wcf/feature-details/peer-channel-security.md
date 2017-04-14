---
title: "Protezione del canale peer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2c59b164-3729-44f0-a967-f247c42de662
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Protezione del canale peer
Il canale peer attiva diversi tipi di applicazioni distribuite che dipendono da messaggistica a più parti.Ne è un esempio la distribuzione di contenuto Internet, in cui un'origine attendibile distribuisce il contenuto \(ad esempio aggiornamenti di supporti o software\), un gruppo di amici si scambiano musica e foto o un gruppo di colleghi lavora in modo collaborativo a un documento.Ognuno di questi scenari richiede un modello di sicurezza univoco.Il modello di sicurezza del canale peer ha lo scopo di affrontare tali scenari e offrire un modello sicuro per le rispettive esigenze di diversi modelli di identità, autenticazione e autorizzazione.  
  
## Scenari di sicurezza  
 Uno scenario di distribuzione del contenuto richiede che ogni destinatario del contenuto identifichi l'origine del contenuto.A causa della natura distribuita dello scenario, non è sempre possibile conoscere e considerare attendibili gli intermediari che elaborano o intercettano i messaggi.Per contrastare con efficacia il rischio che un intermediario non attendibile manometta i messaggi, è possibile proteggerli tramite le applicazioni presso il mittente al fine di rilevare facilmente qualsiasi tentativo di manomissione.In tal caso, a seconda della riservatezza del contenuto, può essere necessaria la crittografia.  
  
 Scenari come la collaborazione su documenti di gruppo, spesso richiedono che ogni membro che partecipa alla sessione venga identificato e autenticato individualmente.Ciò significa che, per avere una sessione protetta, è necessario un meccanismo per definire e autenticare tali gruppi di utenti.Le applicazioni potrebbero inoltre richiedere l'analisi di ogni messaggio tramite l'autenticazione al livello di messaggio.In questi tipi di applicazioni, è possibile sacrificare le prestazioni a favore di uno schema di sicurezza più sicuro.  
  
 Una sessione di comunicazione tra un gruppo di utenti casuali può richiedere modelli di sicurezza informali, ad esempio la conoscenza di un segreto comune tra il gruppo.Per questi tipi di applicazioni, è più importante avere un modello di sicurezza facile da applicare e configurare che non disporre di una forma di autenticazione più sicura o di misure di non ripudio.Per questi scenari, un meccanismo di autenticazione basato su password consente di proteggere il livello di comunicazione consentendo, al contempo, l'autenticazione dei messaggi.La sicurezza basata su password è l'impostazione predefinita per il canale peer.  
  
## Tipi di token  
 Il canale peer riconosce un solo tipo di token per l'identificazione sicura, i certificati X.509 che offrono un modello sicuro di identità basato sul tipo di autenticazione e di autorizzazione che può essere implementato.Riservatezza e integrità sono assicurate facilmente dall'utilizzo di certificati.Può tuttavia essere difficile utilizzare e distribuire i certificati X.509.  
  
 Il canale peer fornisce inoltre il supporto per applicazioni semplici tramite l'utilizzo di password.Le applicazioni possono scegliere di impostare gruppi peer rapidi e semplici basati su una password fornita.In questo caso, il proprietario di un gruppo decide e comunica la password ai membri.Ogni membro deve accedere utilizzando la password prima di poter partecipare alla sessione.Le password possono essere utilizzate solo per consentire l'accesso alla sessione, non per eseguire l'autenticazione dei messaggi.Ciò è dovuto al fatto che è difficile e inappropriato utilizzare per l'autenticazione dell'origine un token simmetrico condiviso da un gruppo di peer.  
  
## Modello di sicurezza  
 Il canale peer consente di proteggere i singoli collegamenti tra peer.Ciò significa che un messaggio non passa mai per un collegamento non protetto \(dal punto di vista dell'applicazione\).Internamente, ogni collegamento \(un canale di trasporto tra due peer\) viene protetto utilizzando Transport Layer Security \(TLS\).Ciò significa che quando un mittente compone e invia un messaggio, quest'ultimo viene inviato su un trasporto protetto a ognuno dei peer vicini che vi accedono e tali peer, a loro volta, lo inviano ai peer vicini su connessioni protette.Questa protezione funziona solo a livello di trasporto ed è indipendente dai modelli di sicurezza del messaggio.  
  
 Il canale peer offre inoltre un modo per proteggere i messaggi indipendentemente dalla sicurezza del trasporto utilizzata.In questo modello, il messaggio viene protetto all'origine utilizzando il token di sicurezza dell'origine, anche se attualmente sono supportati solo i certificati X.509.Il messaggio protetto viene quindi trasmesso sulla rete peer.Ogni peer ricevente può verificare l'autenticità dell'origine.Si noti che il messaggio è protetto in modo che gli intermediari non possano manometterlo.  
  
 Ai fini della riservatezza, le applicazioni possono utilizzare la protezione del trasporto con schemi di appartenenza a un gruppo sicuri per impedire l'accesso non autorizzato al messaggio.  
  
 Il canale peer non richiede un modello di identità specifico a condizione che l'applicazione scelga uno dei tipi di token supportati.Le applicazioni detengono la proprietà completa del ciclo di vita di queste identità e delle decisioni di autenticazione.  
  
## Vedere anche  
 [Protezione di applicazioni del canale peer](../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)   
 [Concetti relativi al canale peer](../../../../docs/framework/wcf/feature-details/peer-channel-concepts.md)   
 [Creazione di un'applicazione del canale peer](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)