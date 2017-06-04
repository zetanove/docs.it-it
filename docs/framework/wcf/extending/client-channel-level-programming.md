---
title: "Programmazione a livello di canale client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b787719-4e77-4e77-96a6-5b15a11b995a
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Programmazione a livello di canale client
In questo argomento viene descritta la procedura di scrittura di un'applicazione client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] senza utilizzare la classe <xref:System.ServiceModel.ClientBase%601?displayProperty=fullName> e il relativo modello a oggetti associato.  
  
## Invio di messaggi  
 Per l'invio di messaggi e la ricezione e l'elaborazione di risposte è necessario eseguire i passaggi seguenti:  
  
1.  Creare un'associazione.  
  
2.  Generare una channel factory.  
  
3.  Creare un canale.  
  
4.  Inviare una richiesta e leggere la riposta.  
  
5.  Chiudere tutti gli oggetti canale.  
  
#### Creazione di un'associazione  
 Come nel caso della ricezione \(vedere [Programmazione client a livello di canale](../../../../docs/framework/wcf/extending/service-channel-level-programming.md)\), l'invio di messaggi inizia dalla creazione di un'associazione.In questo esempio viene creato un nuovo <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> e viene aggiunto un <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=fullName> alla rispettiva raccolta di elementi.  
  
#### Generare una channel factory.  
 Anziché creare un <xref:System.ServiceModel.Channels.IChannelListener?displayProperty=fullName>, questa volta è necessario creare una <xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName> chiamando <xref:System.ServiceModel.ChannelFactory.CreateFactory%2A?displayProperty=fullName> nell'associazione dove il parametro del tipo è <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=fullName>.Mentre i listener del canale vengono utilizzati dalla parte in attesa di messaggi in arrivo, le channel factory vengono utilizzate dalla parte che inizia la comunicazione per creare un canale.Esattamente come i listener del canale, le channel factory devono essere aperte prima di poter essere utilizzate.  
  
#### Creazione di un canale  
 È necessario quindi chiamare <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=fullName> per creare un <xref:System.ServiceModel.Channels.IRequestChannel>.Questa chiamata prende l'indirizzo dell'endpoint con il quale si vuole comunicare utilizzando il nuovo canale creato.Quando viene ottenuto un canale, è necessario chiamare Open su di esso per renderlo pronto per la comunicazione.A seconda della natura del trasporto, con questa chiamata a Open viene avviata una connessione con l'endpoint di destinazione oppure non viene eseguita alcuna operazione nella rete.  
  
#### Invio di una richiesta e lettura della risposta  
 Dopo che un canale è stato aperto, è possibile creare un messaggio e utilizzare il metodo di richiesta del canale per inviare la richiesta e attendere la risposta.Questo metodo restituisce un messaggio di risposta che è possibile leggere per scoprire quale è stata la risposta dell'endpoint.  
  
#### Chiusura di oggetti  
 Per evitare la perdita di risorse, è necessario chiudere gli oggetti utilizzati nelle comunicazioni quando non sono più necessari.  
  
 Nell'esempio di codice seguente viene illustrato un client di base che utilizza la channel factory per inviare un messaggio e leggere la risposta.  
  
 [!code-csharp[ChannelProgrammingBasic#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/channelprogrammingbasic/cs/clientprogram.cs#2)]
 [!code-vb[ChannelProgrammingBasic#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelprogrammingbasic/vb/clientprogram.vb#2)]