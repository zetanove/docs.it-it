---
title: "Endpoint: indirizzi, associazioni e contratti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "endpoint [WCF]"
  - "WCF [WCF], endpoint"
  - "Windows Communication Foundation [WCF], endpoint"
ms.assetid: 9ddc46ee-1883-4291-9926-28848c57e858
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Endpoint: indirizzi, associazioni e contratti
La comunicazione con un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] si verifica interamente tramite gli *endpoint* del servizio.Gli endpoint forniscono ai client l'accesso alla funzionalità offerta da un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Ogni endpoint è costituito da quattro proprietà:  
  
-   Un indirizzo che indica dove si trova l'endpoint.  
  
-   Un'associazione che specifica in che modo un client può comunicare con l'endpoint.  
  
-   Un contratto che identifica le operazioni disponibili.  
  
-   Un set di comportamenti che specificano dettagli di implementazione locali dell'endpoint.  
  
 In questo argomento viene illustrata la struttura di un endpoint e viene spiegato come tale struttura viene rappresentata nel modello a oggetti [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Struttura di un endpoint  
 Ogni endpoint è costituito dagli elementi seguenti:  
  
-   Indirizzo: l'indirizzo identifica in modo univoco l'endpoint e comunica ai potenziali utenti l'ubicazione del servizio.Nel modello a oggetti [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], l'indirizzo è rappresentato dalla classe <xref:System.ServiceModel.EndpointAddress>.Una classe <xref:System.ServiceModel.EndpointAddress> contiene:  
  
    -   Una proprietà <xref:System.ServiceModel.EndpointAddress.Uri%2A>, che rappresenta l'indirizzo del servizio.  
  
    -   Una proprietà <xref:System.ServiceModel.EndpointAddress.Identity%2A>, che rappresenta l'identità di sicurezza del servizio e una raccolta di intestazioni di messaggio facoltative.Le intestazioni di messaggio facoltative vengono utilizzate per fornire ulteriori informazioni di indirizzamento più dettagliate, per identificare o interagire con l'endpoint.  
  
     [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Specifica di un indirizzo endpoint](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
-   Associazione: l'associazione specifica la modalità di comunicazione con l'endpoint,vale a dire:  
  
    -   Il protocollo di trasporto da utilizzare \(ad esempio, TCP o HTTP\).  
  
    -   La codifica da utilizzare per i messaggi \(ad esempio, testo o binaria\).  
  
    -   I necessari requisiti di sicurezza \(ad esempio, la protezione dei messaggi SSL o SOAP\).  
  
     [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Panoramica delle associazioni WCF](../../../../docs/framework/wcf/bindings-overview.md).Nel modello a oggetti [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], un'associazione è rappresentata dalla classe astratta di base <xref:System.ServiceModel.Channels.Binding>.Per la maggior parte degli scenari, gli utenti possono utilizzare una delle associazioni fornite dal sistema.Per ulteriori informazioni, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md).  
  
-   Contratti: il contratto delinea la funzionalità che l'endpoint espone al client.Un contratto specifica:  
  
    -   Quali operazioni possono essere chiamate da un client.  
  
    -   La forma del messaggio.  
  
    -   Il tipo di parametri di input o di dati necessario per chiamare l'operazione.  
  
    -   Il tipo di elaborazione o di messaggio di risposta che il client può aspettarsi.  
  
     Per ulteriori informazioni sulla definizione di un contratto, vedere [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md).  
  
-   Comportamenti: è possibile utilizzare i comportamenti dell'endpoint per personalizzare il comportamento locale dell'endpoint del servizio.I comportamenti dell'endpoint realizzano questo obiettivo partecipando al processo di generazione di un runtime [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Un esempio di comportamento dell'endpoint è rappresentato dalla proprietà <xref:System.ServiceModel.Description.ServiceEndpoint.ListenUri%2A>, che consente di specificare un indirizzo di ascolto diverso dall'indirizzo SOAP o WSDL \(Web Services Description Language\).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][ClientViaBehavior](../../../../docs/framework/wcf/diagnostics/wmi/clientviabehavior.md).  
  
## Definizione di endpoint  
 È possibile specificare l'endpoint di un servizio in modo imperativo, tramite codice, o in modo dichiarativo, tramite la configurazione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: creare un endpoint di servizio nella configurazione](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md) e [Procedura: creare un endpoint del servizio nel codice](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md).  
  
## Argomenti della sezione  
 In questa sezione viene illustrato lo scopo di associazioni, endpoint e indirizzi; viene descritto come configurare un'associazione e un endpoint e viene dimostrato come utilizzare il comportamento `ClientVia` e la proprietà `ListenUri`.  
  
 [Indirizzi](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md)  
 Viene descritto come vengono indirizzati gli endpoint in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [Associazioni](../../../../docs/framework/wcf/feature-details/bindings.md)  
 Viene descritto come vengono utilizzate le associazioni per specificare i dettagli sul trasporto, la codifica e il protocollo necessari per consentire la comunicazione tra client e servizi.  
  
 [Contratti](../../../../docs/framework/wcf/feature-details/contracts.md)  
 Viene descritto in che modo i contratti definiscono i metodi di un servizio.  
  
 [Procedura: creare un endpoint di servizio nella configurazione](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)  
 Viene descritto come creare un endpoint del servizio nella configurazione.  
  
 [Procedura: creare un endpoint del servizio nel codice](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)  
 Viene descritto come creare un endpoint del servizio nel codice.  
  
 [Procedura: usare Svcutil.exe per convalidare il codice del servizio compilato](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-validate-compiled-service-code.md)  
 Viene descritto come rilevare errori in implementazioni e configurazioni del servizio senza ospitare il servizio, tramite lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
## Vedere anche  
 [Configurazione dei servizi](../../../../docs/framework/wcf/configuring-services.md)   
 [Estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md)