---
title: "Servizi host | Microsoft Docs"
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
helpviewer_keywords: 
  - "servizi host [WCF]"
ms.assetid: 192be927-6be2-4fda-98f0-e513c4881acc
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# Servizi host
Per diventare attivo, un servizio deve essere ospitato all'interno di un ambiente di runtime che lo crea e ne controlla il contesto e la durata. I servizi [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] sono progettati per essere eseguiti in qualsiasi processo di Windows che supporta codice gestito.  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] fornisce un modello di programmazione unificato per la compilazione di applicazioni orientate ai servizi. Questo modello di programmazione rimane coerente ed è indipendente dall'ambiente di runtime nel quale viene distribuito il servizio. In pratica, ciò significa che il codice per i servizi interessati rimane praticamente invariato a prescindere dall'opzione di hosting.  
  
 Le opzioni di hosting vanno dall'esecuzione in una semplice applicazione console ad ambienti server come un servizio Windows in esecuzione in un processo di lavoro gestito da Internet Information Services \(IIS\) o dal servizio di attivazione dei processi di Windows \(WAS\). Gli sviluppatori scelgono l'ambiente host che soddisfa i requisiti di distribuzione del servizio. Questi requisiti potrebbero derivare dalla piattaforma sulla quale viene distribuita l'applicazione, il trasporto sul quale deve inviare e ricevere messaggi o sul tipo di riciclo del processo e gestione di altri processi richiesti per assicurare la disponibilità adeguata o su altri requisiti di gestione o affidabilità. Nella prossima sezione vengono fornite informazioni e istruzioni sulle opzioni di hosting.  
  
## Opzioni di hosting  
  
#### Self\-hosting in un'applicazione gestita  
 I servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] possono essere ospitati in qualsiasi applicazione gestita. Questa è l'opzione più flessibile perché richiede la distribuzione di un'infrastruttura minima. Incorporare il codice per il servizio all'interno del codice dell'applicazione gestita, quindi creare e aprire un'istanza di <xref:System.ServiceModel.ServiceHost> per rendere il servizio disponibile.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Procedura: ospitare un servizio WCF in un'applicazione gestita](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md).  
  
 Questa opzione consente due scenari comuni: servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in esecuzione all'interno di applicazioni console e applicazioni client ricche di funzionalità come quelle basate su [!INCLUDE[avalon1](../../../includes/avalon1-md.md)] o su Windows Form \(WinForms\). L'hosting di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] all'interno di un'applicazione console in genere è utile durante la fase di sviluppo dell'applicazione. Agevola infatti il debug, l'ottenimento di informazioni di traccia per scoprire cosa accadde all'interno dell'applicazione e lo spostamento copiandole in nuove posizioni. Questa opzione di hosting consente inoltre ad applicazioni rich client, quali quelle [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] e Windows Form, di comunicare più facilmente con l'esterno. Ne è un esempio un client di collaborazione peer\-to\-peer che utilizza [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] per l'interfaccia utente e che ospita anche un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] che consente ad altri client di connettersi ad esso per condividere informazioni.  
  
#### Servizi Windows gestiti  
 Questa opzione di hosting consiste nella registrazione del dominio dell'applicazione \(AppDomain\) che ospita un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] come servizio Windows gestito \(precedentemente noto come servizio NT\) affinché la durata del processo del servizio sia controllata da Gestione controllo servizi \(SCM, Service Control Manager\) per i servizi Windows. Analogamente all'opzione di self\-hosting, questo tipo di ambiente host richiede che venga scritto codice di hosting come parte dell'applicazione. Il servizio viene implementato sia come servizio Windows che come servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], di conseguenza eredita sia dalla classe <xref:System.ServiceProcess.ServiceBase> che da un'interfaccia di contratto del servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].<xref:System.ServiceModel.ServiceHost> viene quindi creato e aperto all'interno di un metodo [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> sottoposto a override e chiuso all'interno di un metodo <xref:System.ServiceProcess.ServiceBase.OnStop> sottoposto a override. È inoltre necessario implementare una classe del programma di installazione che eredita da <xref:System.Configuration.Install.Installer> per consentire l'installazione del programma come servizio Windows tramite Installutil.exe.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Procedura: ospitare un servizio WCF in un servizio Windows gestito](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md). Lo scenario reso possibile dall'opzione di hosting del servizio Windows gestito è quello di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di lunga durata ospitato all'esterno di IIS in un ambiente protetto non attivato da messaggi. La durata del servizio è controllata invece dal sistema operativo. Questa opzione di hosting è disponibile in tutte le versioni di Windows.  
  
#### Internet Information Services \(IIS\)  
 L'opzione di hosting di IIS è integrata con [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] e utilizza le funzionalità offerte da queste tecnologie, ad esempio riciclo del processo, chiusura per inattività, monitoraggio dell'integrità del processo e attivazione basata su messaggi. Nei sistemi operativi [!INCLUDE[wxp](../../../includes/wxp-md.md)] e [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], questa è la soluzione preferita per ospitare applicazioni del servizio Web che devono essere estremamente disponibili ed estremamente scalabili. IIS offre inoltre la gestione integrata che i clienti si aspettano da un prodotto server aziendale. Questa opzione di hosting richiede che IIS sia configurato correttamente, ma non richiede la scrittura di codice di hosting come parte dell'applicazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)] come configurare l'hosting di IIS per un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Procedura: ospitare un servizio WCF in IIS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md).  
  
 Si noti che i servizi ospitati da IIS possono utilizzare solo il trasporto HTTP. L'implementazione in IIS 5.1 ha introdotto alcune limitazioni in [!INCLUDE[wxp](../../../includes/wxp-md.md)]. L'attivazione basata su messaggi fornita per un servizio di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] da IIS 5.1 su [!INCLUDE[wxp](../../../includes/wxp-md.md)] impedisce a qualsiasi altro servizio di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] self\-hosted nello stesso computer di utilizzare la porta 80 per comunicare. I servizi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] possono essere eseguiti nello stesso AppDomain\/Pool di applicazioni\/Processo di lavoro di altre applicazioni quando sono ospitati da [!INCLUDE[iis601](../../../includes/iis601-md.md)] su [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]. Dato che [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e [!INCLUDE[iis601](../../../includes/iis601-md.md)] utilizzano entrambi lo stack HTTP \(HTTP.sys\) della modalità kernel, a differenza di IIS 5.1, [!INCLUDE[iis601](../../../includes/iis601-md.md)] può invece condividere la porta 80 con altri servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] indipendenti in esecuzione sullo stesso computer.  
  
#### Servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\)  
 Il servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\) è il nuovo meccanismo di attivazione del processo per [!INCLUDE[lserver](../../../includes/lserver-md.md)] disponibile anche su [!INCLUDE[wv](../../../includes/wv-md.md)]. Mantiene il modello di processo \(pool di applicazioni e attivazione del processo basata su messaggi\) e le funzionalità di hosting \(ad esempio protezione rapida da errori, monitoraggio dell'integrità e riciclo\) classiche di [!INCLUDE[iis601](../../../includes/iis601-md.md)], ma rimuove la dipendenza da HTTP dall'architettura di attivazione.[!INCLUDE[iisver](../../../includes/iisver-md.md)] utilizza WAS per eseguire l'attivazione basata su messaggi su HTTP. Anche i componenti aggiuntivi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] si collegano a WAS per fornire l'attivazione basata su messaggi sugli altri protocolli supportati da [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], ad esempio TCP, MSMQ e named pipe. Ciò consente alle applicazioni che utilizzano protocolli di comunicazione di utilizzare funzionalità IIS quali il riciclo del processo, la protezione rapida da errori e il sistema di configurazione comune che erano disponibili solo per applicazioni basate su HTTP.  
  
 Questa opzione di hosting richiede che WAS sia configurato correttamente, ma non richiede la scrittura di codice di hosting come parte dell'applicazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)] come configurare l'hosting di WAS, vedere [Procedura: ospitare un servizio WCF in WAS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md).  
  
## Scelta di un ambiente host  
 Nella tabella seguente vengono riepilogati alcuni dei vantaggi e degli scenari principali associati a ogni opzione di hosting.  
  
|Ambiente host|Scenari comuni|Vantaggi e limitazioni principali|  
|-------------------|--------------------|---------------------------------------|  
|Applicazione gestita \("indipendente"\)|-   Applicazioni console utilizzate durante lo sviluppo.<br />-   Applicazioni client ricche di funzionalità WinForm e [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] che accedono ai servizi.|-   Flessibile.<br />-   Facile da distribuire.<br />-   Non è una soluzione aziendale per i servizi.|  
|Servizi Windows \(precedentemente noti come servizi NT\)|-   Un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di lunga durata ospitato al di fuori di IIS.|-   Durata del processo del servizio controllata dal sistema operativo, non attivata da messaggi.<br />-   Supportato da tutte le versioni di Windows.<br />-   Ambiente protetto.|  
|IIS 5.1, [!INCLUDE[iis601](../../../includes/iis601-md.md)]|-   Esecuzione di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] side\-by\-side con contenuto [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] su Internet utilizzando il protocollo HTTP.|-   Riciclo del processo.<br />-   Chiusura per inattività.<br />-   Monitoraggio dell'integrità del processo.<br />-   Attivazione basata su messaggi.<br />-   Solo HTTP.|  
|Servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\)|-   Esecuzione di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] senza installare IIS su Internet utilizzando vari protocolli di trasporto.|-   IIS non è richiesto.<br />-   Riciclo del processo.<br />-   Chiusura per inattività.<br />-   Monitoraggio dell'integrità del processo.<br />-   Attivazione basata su messaggi.<br />-   Funziona con HTTP, TCP, named pipe e MSMQ.|  
|IIS 7.0|-   Esecuzione di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con contenuto [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].<br />-   Esecuzione di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] su Internet utilizzando vari protocolli di trasporto.|-   Vantaggi di WAS.<br />-   Integrato con [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] e contenuto IIS.|  
  
 La scelta di un ambiente host dipende dalla versione di Windows sulla quale è distribuito, dal trasporto necessario per inviare i messaggi e dai requisiti per il tipo di riciclo del dominio dell'applicazione e del processo. Nella tabella seguente sono riepilogati i dati relativi a tali requisiti.  
  
|Ambiente host|Disponibilità della piattaforma|Trasporti supportati|Riciclo di processo e AppDomain|  
|-------------------|-------------------------------------|--------------------------|-------------------------------------|  
|Applicazioni gestite \("indipendenti"\)|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP,<br /><br /> net.tcp,<br /><br /> net.pipe,<br /><br /> net.msmq|No|  
|Servizi Windows \(precedentemente noti come servizi NT\)|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP,<br /><br /> net.tcp,<br /><br /> net.pipe,<br /><br /> net.msmq|No|  
|IIS 5,1|[!INCLUDE[wxp](../../../includes/wxp-md.md)]|HTTP|Sì|  
|[!INCLUDE[iis601](../../../includes/iis601-md.md)]|[!INCLUDE[ws2003](../../../includes/ws2003-md.md)]|HTTP|Sì|  
|Servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\)|[!INCLUDE[wv](../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP,<br /><br /> net.tcp,<br /><br /> net.pipe,<br /><br /> net.msmq|Sì|  
  
 È importante notare che l'esecuzione di un servizio o di una qualsiasi estensione da un host non attendibile compromette la sicurezza. Si noti inoltre che quando si apre un <xref:System.ServiceModel.ServiceHost> in caso di utilizzo della rappresentazione, un'applicazione deve controllare che l'utente non si sia disconnesso, ad esempio memorizzando nella cache l'elemento <xref:System.Security.Principal.WindowsIdentity> dell'utente.  
  
## Vedere anche  
 [Requisiti di sistema](../../../docs/framework/wcf/wcf-system-requirements.md)   
 [Ciclo di vita della programmazione di base](../../../docs/framework/wcf/basic-programming-lifecycle.md)   
 [Implementazione dei contratti di servizio](../../../docs/framework/wcf/implementing-service-contracts.md)   
 [Procedura: ospitare un servizio WCF in IIS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)   
 [Procedura: ospitare un servizio WCF in WAS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)   
 [Procedura: ospitare un servizio WCF in un servizio Windows gestito](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)   
 [Procedura: ospitare un servizio WCF in un'applicazione gestita](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)