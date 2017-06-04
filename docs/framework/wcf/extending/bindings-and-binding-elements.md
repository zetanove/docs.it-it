---
title: "Associazioni ed elementi di associazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "elementi di associazione [WCF]"
ms.assetid: 765ff77b-7682-4ea3-90eb-e4d751e37379
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Associazioni ed elementi di associazione
Le associazioni sono raccolte di elementi di configurazione speciali, detti *elementi di associazione*. Questi elementi vengono esaminati dal runtime del servizio ogni volta che un endpoint client o server viene creato.Il tipo e l'ordine degli elementi di un'associazione determinano la scelta e l'ordine di sovrapposizione dei canali di protocollo e di trasporto dello stack di canali di un endpoint.  
  
 Le associazioni, specialmente le associazioni fornite dal sistema, in genere presentano diverse proprietà di configurazione che riflettono le proprietà degli elementi di associazione incapsulati che più di frequente vengono modificate.  
  
 Ogni associazione deve contenere un solo elemento di associazione di trasporto.Ogni elemento di associazione di trasporto implica un elemento di associazione di codifica dei messaggi predefinito. Per eseguire l'override di questo elemento è possibile aggiungere all'associazione un unico elemento di associazione di codifica dei messaggi.Oltre agli elementi di associazione di trasporto e di codifica, l'associazione può contenere un numero qualsiasi di elementi di associazione di protocollo per soddisfare i requisiti di funzionalità di un servizio nonché per consentire l'invio di messaggi SOAP fra endpoint.Per informazioni dettagliate, vedere [Uso di associazioni per configurare servizi e client](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md).  
  
## Estensione delle associazioni e degli elementi di associazione  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] offre associazioni fornite dal sistema in grado di soddisfare i requisiti di una vasta gamma di scenari.Per ulteriori informazioni, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md). In determinati casi, tuttavia, è necessario creare e utilizzare associazioni non disponibili in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Negli scenari seguenti occorre creare una nuova associazione.  
  
-   Esigenza di utilizzare un nuovo elemento di associazione, ad esempio di trasporto, di codifica o di protocollo. In questo scenario è necessario creare una nuova associazione contenente l'elemento di associazione desiderato.Ad esempio, se si aggiunge un elemento di trasporto UDP `UdpTransportBindingElement` personalizzato occorre creare una nuova associazione per utilizzarlo.Per informazioni sull'implementazione di questo comportamento mediante il tipo <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>, vedere [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
-   Configurazione di elementi di associazione esistenti in modo che le associazioni fornite dal sistema non espongano proprietà pubbliche.Ad esempio, per modificare l'ordine di esecuzione delle operazioni di firma e crittografia è necessario creare una nuova associazione.Per informazioni sull'implementazione di questo comportamento, vedere [Procedura: personalizzare un'associazione fornita dal sistema](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md).  
  
-   Creazione di associazioni standard aziendali che espongono soltanto opzioni di configurazione specifiche.Ad esempio, per creare una versione aziendale dell'associazione <xref:System.ServiceModel.WSHttpBinding> in cui non sia consentito disattivare la protezione è possibile creare una nuova associazione che funziona come l'associazione <xref:System.ServiceModel.WSHttpBinding> ma in cui la protezione sia sempre attiva.Per informazioni dettagliate, vedere [Creazione di associazioni definite dall'utente](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).  
  
-   Personalizzazione di metadati, quasi sempre allo scopo di configurare o utilizzare un determinato elemento di associazione personalizzato.Per ulteriori informazioni su come implementare il supporto dei metadati nelle associazioni e negli elementi di associazione, vedere [Supporto di configurazione e metadati](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
-  
  
## Canali, associazioni ed elementi di associazione  
 Le associazioni e gli elementi di associazione rappresentano la connessione tra il modello di programmazione delle applicazioni, che comprende attributi e comportamenti, e il modello di canale, che comprende le factory e i listener, i codificatori di messaggi e le implementazioni di trasporto e di protocollo.In genere gli elementi di associazione e le associazioni vengono implementate per consentire al livello applicazione di utilizzare i canali.  
  
 Il livello di canale scambia messaggi con il livello di servizio e trasporta tali messaggi fra gli endpoint.In un client, il livello di canale è uno stack di channel factory che creano canali per un endpoint di rete.In un servizio, il livello di canale è uno stack di listener di canale che accettano i canali ricevuti presso un endpoint di rete.  
  
 Esistono due tipi generali di canali: canali di protocollo e canali di trasporto.I canali di trasporto sono responsabili per la trasmissione effettiva di un messaggio da un endpoint di rete a un altro.I canali di trasporto devono presentare un codificatore di messaggi predefinito e devono essere in grado di utilizzare un codificatore di messaggi alternativo fornito tramite un elemento di associazione di codifica.Un codificatore di messaggi è responsabile per la trasformazione di un messaggio <xref:System.ServiceModel.Channels.Message?displayProperty=fullName> in una rappresentazione di trasmissione e viceversa.I canali di protocollo sono responsabili per l'implementazione di protocolli a livello SOAP, ad esempio WS\-Security o WS\-ReliableMessaging.  
  
 Il requisito fondamentale dei canali di trasporto e di protocollo è implementare le interfacce di canale necessarie.Per creare un livello di canale funzionante è necessario associare a queste interfacce vari elementi, fra cui factory e listener.Per utilizzare le implementazioni di canale di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] occorre associare a ogni canale un elemento di associazione derivato dalla classe <xref:System.ServiceModel.Channels.BindingElement>. È inoltre necessario includere nei file di configurazione un elemento di estensione di associazione correlato derivato dalla classe <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>.  
  
 Come menzionato in precedenza, gli elementi di associazione dei codificatori di messaggi nonché le implementazioni di canali di protocollo e di trasporto possono essere sovrapposti allo scopo di creare uno stack di canali. Il meccanismo utilizzato per organizzare tali elementi in un set ordinato è l'associazione.Le associazioni e gli elementi di associazione rappresentano la connessione fra il modello di programmazione delle applicazioni e il modello di canale.Le implementazioni di canale personalizzate possono essere utilizzate direttamente dal codice. Tuttavia, tali implementazioni possono essere utilizzate dal modello di programmazione del livello di servizio soltanto se i codificatori, i trasporti e i protocolli vengono implementati come elementi di associazione.  
  
 Per informazioni dettagliate sullo sviluppo di canali e dei relativi elementi di associazione, vedere [Estensione del livello del canale](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md).