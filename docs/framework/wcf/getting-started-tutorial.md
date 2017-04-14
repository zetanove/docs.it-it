---
title: "Esercitazione introduttiva | Microsoft Docs"
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
  - "guida introduttiva [WCF]"
  - "WCF [WCF], introduzione"
  - "Windows Communication Foundation [WCF], introduzione"
ms.assetid: df939177-73cb-4440-bd95-092a421516a1
caps.latest.revision: 47
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 47
---
# Esercitazione introduttiva
Gli argomenti contenuti in questa sezione intendono fornire una rapida descrizione dell'esperienza di programmazione [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].  Vengono ideati per essere completati secondo l'ordine dell'elenco posto nella parte inferiore di questo argomento.  Nel corso di questa esercitazione vengono fornite informazioni introduttive sui passaggi necessari per creare applicazioni di servizio e client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Un servizio espone uno o più endpoint, ciascuno dei quali espone una o più operazioni del servizio.  L'*endpoint* di un servizio specifica un indirizzo presso il quale è possibile trovare il servizio, un'associazione che contiene le informazioni che descrivono la modalità di comunicazione di un client con il servizio e un contratto che definisce la funzionalità fornita dal servizio ai propri client.  
  
 Seguendo la sequenza degli argomenti di questa esercitazione si otterrà un servizio funzionante e un client che chiama il servizio.  Nei primi tre argomenti viene descritto come definire e implementare un contratto di servizio, nonché come ospitare il servizio.  Il servizio creato è self\-hosted all'interno di un'applicazione console.  I servizi possono anche essere ospitati in Internet Information Services \(IIS\).  [!INCLUDE[crabout](../../../includes/crabout-md.md)] come effettuare questa operazione, vedere [Procedura: ospitare un servizio WCF in IIS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md).  Il servizio viene configurato nel codice; tuttavia, i servizi possono essere configurati anche all'interno di un file di configurazione.  [!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'utilizzo di un file di configurazione, vedere [Configurazione dei servizi tramite file di configurazione](../../../docs/framework/wcf/configuring-services-using-configuration-files.md).  
  
 Nei tre argomenti successivi viene descritto come creare un proxy client, configurare l'applicazione client e usare il proxy client per chiamare l'operazione del servizio esposta da quest'ultimo.  I servizi pubblicano i metadati che definiscono le informazioni necessarie a un'applicazione client per comunicare con il servizio.  In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] il processo di accesso a questi metadati viene automatizzato e i metadati vengono usati per creare e configurare l'applicazione client per il servizio.  Se non si usa [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], è possibile usare lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per creare e configurare l'applicazione client per il servizio.  
  
 In tutti gli argomenti di questa sezione si presuppone l'uso di Visual Studio 2011 come ambiente di sviluppo.  Se si sta usando un altro ambiente di sviluppo, ignorare le istruzioni specifiche di [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)].  
  
> [!NOTE]
>  Se è in esecuzione [!INCLUDE[wv](../../../includes/wv-md.md)] o versioni successive del sistema operativo Windows, è necessario avviare [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] selezionando il menu Start e facendo clic con il pulsante destro del mouse su Visual Studio 2011 e, infine, scegliendo **Esegui come amministratore**.  Per avviare sempre Visual Studio 2011 con diritti di amministratore è possibile creare un collegamento, fare clic con il pulsante destro del mouse sul collegamento, selezionare le proprietà, la scheda **Compatibilità** e la casella di controllo **Esegui questo programma come amministratore**.  Quando si avvia Visual Studio 2011 con questo collegamento, verrà sempre eseguito con diritti di amministratore.  
  
 Per informazioni sulle applicazioni di esempio che è possibile scaricare ed eseguire sul disco rigido, vedere gli argomenti in [Windows Communication Foundation Samples](http://msdn.microsoft.com/it-it/8ec9d192-5d81-4f64-bfd3-90c5e5858c91).  Per questo argomento, vedere, in particolare, [Guida introduttiva](../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
 Per altre informazioni dettagliate sulla creazione di servizi e client, vedere [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md).  
  
## In questa sezione  
 [Procedura: definire il contratto di servizio](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)  
 Viene descritto come creare un contratto [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] usando un'interfaccia definita dall'utente.  Il contratto definisce la funzionalità esposta dal servizio.  
  
 [Procedura: implementare un contratto di servizio](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)  
 Viene descritto come implementare un contratto di servizio.  Una volta definito, un contratto deve essere implementato con una classe di servizio.  
  
 [Procedura: ospitare ed eseguire un servizio di base](../../../docs/framework/wcf/how-to-host-and-run-a-basic-wcf-service.md)  
 Viene descritto come configurare un endpoint per il servizio nel codice e come ospitare il servizio in un'applicazione console.  Per diventare attivo, un servizio deve essere configurato e ospitato all'interno di un ambiente di runtime.  Questo ambiente crea il servizio e ne controlla contesto e durata.  
  
 [Procedura: creare un client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)  
 Viene descritto come recuperare i metadati usati per creare un proxy client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] da un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  In questo processo viene usata la funzionalità Aggiungi riferimento al servizio di Visual Studio 2011.  
  
 [Procedura: descrizione della configurazione di un client](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md)  
 Viene descritto come configurare un client WCF. La configurazione del client richiede la specifica dell'endpoint usato dal client per accedere al servizio.  
  
 [Procedura: usare un client](../../../docs/framework/wcf/how-to-use-a-wcf-client.md)  
 Viene descritto come usare il proxy client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per richiamare le operazioni del servizio.  
  
## Riferimenti  
 <xref:System.ServiceModel.ServiceContractAttribute>  
  
 <xref:System.ServiceModel.OperationContractAttribute>  
  
## Sezioni correlate  
 [Windows Communication Foundation Samples](http://msdn.microsoft.com/it-it/8ec9d192-5d81-4f64-bfd3-90c5e5858c91)  
  
 [Ciclo di vita della programmazione di base](../../../docs/framework/wcf/basic-programming-lifecycle.md)  
  
## Vedere anche  
 [Panoramica dei concetti](../../../docs/framework/wcf/conceptual-overview.md)   
 [Guida alla documentazione](../../../docs/framework/wcf/guide-to-the-documentation.md)   
 [Informazioni su Windows Communication Foundation](../../../docs/framework/wcf/whats-wcf.md)   
 [Dettagli delle funzioni di WCF](../../../docs/framework/wcf/feature-details/index.md)