---
title: "Associazioni di Windows Communication Foundation | Microsoft Docs"
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
  - "associazione [WCF]"
  - "WCF [WCF], bindings"
  - "Windows Communication Foundation [WCF], bindings"
ms.assetid: 83639133-89f7-43f0-b4ef-8d9e57c08d25
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Associazioni di Windows Communication Foundation
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] separa il modo in cui il software per un'applicazione viene scritto dal modo in cui comunica con altro software.Le associazioni vengono utilizzate per specificare i dettagli sul trasporto, sulla codifica e sul protocollo necessari per consentire la comunicazione tra client e servizi.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza associazioni per generare la rappresentazione della rete sottostante dell'endpoint, pertanto la maggior parte dei dettagli di associazione deve essere concordata dalle parti coinvolte nella comunicazione.Il modo più semplice per conseguire questo risultato consiste nel fare in modo che i client di un servizio utilizzino la stessa associazione utilizzata dall'endpoint del servizio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] su questa procedura, vedere [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb).  
  
 Un'associazione è costituita da una raccolta di elementi di associazione.Ogni elemento descrive alcuni aspetti relativi alla modalità di comunicazione tra l'endpoint e i client.Un'associazione deve includere almeno un elemento di associazione di trasporto, almeno un elemento di associazione di codifica del messaggio \(che può essere fornito per impostazione predefinita dall'elemento di associazione di trasporto\) e un numero qualsiasi di altri elementi di associazione del protocollo.Il processo che genera una fase di esecuzione da questa descrizione consente a ogni elemento di associazione di fornire codice alla fase di esecuzione.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce associazioni che contengono selezioni comuni di elementi di associazione.Questi possono essere utilizzati con le rispettive impostazioni predefinite oppure è possibile modificare i valori predefiniti in base ai requisiti dell'utente.Le associazioni fornite dal sistema presentano proprietà che consentono il controllo diretto degli elementi di associazione e delle relative impostazioni.È inoltre possibile utilizzare facilmente e side\-by\-side più versioni di un'associazione, assegnando a ogni versione dell'associazione un nome diverso.Per informazioni dettagliate, vedere [Configurazione di associazioni fornite dal sistema](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md).  
  
 Se risulta necessario una raccolta di elementi di associazione non disponibili tra queste associazioni fornite dal sistema, è possibile creare un'associazione personalizzata costituita dalla raccolta di elementi di associazione necessari.Le associazioni personalizzate sono di facile creazione e non richiedono una nuova classe ma non forniscono proprietà per il controllo degli elementi di associazione o delle relative impostazioni.È possibile accedere agli elementi di associazione e modificarne le impostazioni tramite la raccolta che li contiene.Per informazioni dettagliate, vedere [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## In questa sezione  
 [Configurazione di associazioni fornite dal sistema](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 Viene descritto come utilizzare e modificare le associazioni che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce a supporto di scenari comuni.  
  
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 Viene descritto come definire associazioni di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per servizi e client in modo imperativo nel codice e in modo dichiarativo utilizzando la configurazione.  
  
 [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md)  
 Viene descritto l'elemento <xref:System.ServiceModel.Channels.CustomBinding> e la circostanza in cui è utilizzato.  
  
## Riferimenti  
 <xref:System.ServiceModel.Channels.Binding>  
  
 <xref:System.ServiceModel.Channels.BindingElement>  
  
 <xref:System.ServiceModel.Channels.CustomBinding>  
  
## Sezioni correlate  
 [Estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md)