---
title: "Creazione di una classe BindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 01a35307-a41f-4ef6-a3db-322af40afc99
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Creazione di una classe BindingElement
Le associazioni e gli elementi di associazione \(oggetti che estendono rispettivamente le classi <xref:System.ServiceModel.Channels.Binding?displayProperty=fullName> e <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName>\) costituiscono la sede in cui il modello dell'applicazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene associato alle channel factory e ai listener del canale.Senza associazioni, per utilizzare canali personalizzati è necessaria una programmazione a livello di canale come descritto in [Programmazione client a livello di canale](../../../../docs/framework/wcf/extending/service-channel-level-programming.md) e [Programmazione a livello di canale client](../../../../docs/framework/wcf/extending/client-channel-level-programming.md).In questo argomento vengono illustrati il requisito minimo necessario per abilitare l'utilizzo del canale in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], lo sviluppo di una classe <xref:System.ServiceModel.Channels.BindingElement> e l'abilitazione dell'utilizzo dall'applicazione come descritto nel passaggio 4 di [Sviluppo di canali](../../../../docs/framework/wcf/extending/developing-channels.md).  
  
## Panoramica  
 La creazione di un oggetto <xref:System.ServiceModel.Channels.BindingElement> per il canale consente agli sviluppatori di utilizzarlo in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Gli oggetti <xref:System.ServiceModel.Channels.BindingElement> possono essere utilizzati dalla classe <xref:System.ServiceModel.ServiceHost?displayProperty=fullName> per connettere un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] al canale senza doverne precisare le informazioni sul tipo.  
  
 Una volta creata una classe <xref:System.ServiceModel.Channels.BindingElement>, è possibile abilitare ulteriori funzionalità a seconda delle esigenze, eseguendo i rimanenti passaggi di sviluppo del canale descritti in [Sviluppo di canali](../../../../docs/framework/wcf/extending/developing-channels.md).  
  
## Aggiunta di un elemento di associazione.  
 Per implementare una classe <xref:System.ServiceModel.Channels.BindingElement> personalizzata, scrivere una classe che eredita da <xref:System.ServiceModel.Channels.BindingElement>.Ad esempio, se è stato sviluppato un elemento `ChunkingChannel` per suddividere i messaggi di grandi dimensioni in blocchi e assemblarli di nuovo sull'altra estremità, è possibile utilizzare questo canale in qualsiasi associazione implementando una classe <xref:System.ServiceModel.Channels.BindingElement> e configurando l'associazione per il relativo utilizzo.Nella restante parte di questo argomento, verrà utilizzato `ChunkingChannel` come esempio per illustrare i requisiti dell'implementazione di un elemento di associazione.  
  
 `ChunkingBindingElement` è responsabile della creazione di `ChunkingChannelFactory` e `ChunkingChannelListener`.Esegue l'override delle implementazioni dei metodi <xref:System.ServiceModel.Channels.BindingElement.CanBuildChannelFactory%2A> e <xref:System.ServiceModel.Channels.BindingElement.CanBuildChannelListener%2A> e controlla che il parametro di tipo sia <xref:System.ServiceModel.Channels.IDuplexSessionChannel> \(nell'esempio si tratta dell'unica forma del canale supportata da `ChunkingChannel`\) e che gli altri elementi di associazione presenti nell'associazione supportino tale forma.  
  
 Il metodo <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> controlla prima che la forma del canale richiesta possa essere creata e poi ottiene un elenco di azioni del messaggio da suddividere in blocchi.Crea quindi una nuova `ChunkingChannelFactory`, passando la channel factory interna\(se si sta creando un elemento di associazione del trasporto, tale elemento è l'ultimo nello stack dell'associazione e pertanto deve necessariamente creare un listener del canale o una channel factory\).  
  
 L'implementazione del metodo <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> per creare `ChunkingChannelListener` e passare il listener del canale interno è simile.  
  
 Come ulteriore esempio di utilizzo di un canale di trasporto, in [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md) viene fornito l'override seguente.  
  
 Nell'esempio, l'elemento di associazione è `UdpTransportBindingElement`, che deriva dalla classe <xref:System.ServiceModel.Channels.TransportBindingElement>.Esso esegue l'override dei metodi seguenti per creare le factory associate al canale.  
  
```  
public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
{  
            return (IChannelFactory<TChannel>)(object)new UdpChannelFactory(this, context);  
}  
  
public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
{  
            return (IChannelListener<TChannel>)(object)new UdpChannelListener(this, context);  
}  
```  
  
 Contiene inoltre membri per duplicare `BindingElement` e restituire lo schema \(soap.udp\).  
  
#### Elementi di associazione di protocollo  
 I nuovi elementi di associazione possono sostituire o aumentare gli elementi di associazione presenti, aggiungendo nuovi trasporti, codifiche o protocolli di livello superiore.Per creare un nuovo elemento di associazione di protocollo, iniziare estendendo la classe <xref:System.ServiceModel.Channels.BindingElement>.È necessario quindi implementare almeno il metodo <xref:System.ServiceModel.Channels.BindingElement.Clone%2A?displayProperty=fullName> e `ChannelProtectionRequirements` utilizzando il metodo <xref:System.ServiceModel.Channels.IChannel.GetProperty%2A?displayProperty=fullName>.In questo modo viene restituita la classe <xref:System.ServiceModel.Security.ChannelProtectionRequirements> per l'elemento di associazione.Per ulteriori informazioni, vedere <xref:System.ServiceModel.Security.ChannelProtectionRequirements>.  
  
 Il metodo <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> deve restituire una copia aggiornata dell'elemento di associazione.È consigliabile che gli autori dell'elemento di associazione implementino il metodo <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> utilizzando un costruttore di copia che chiami il costruttore di copia di base e che quindi duplichi i campi aggiuntivi in questa classe.  
  
#### Elementi di associazione del trasporto  
 Per creare un nuovo elemento di associazione del trasporto, estendere l'interfaccia <xref:System.ServiceModel.Channels.TransportBindingElement>.È necessario quindi implementare almeno il metodo <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> e la proprietà <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A?displayProperty=fullName>.  
  
 <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> – Deve restituire una copia aggiornata dell'elemento di associazione.È consigliabile che gli autori dell'elemento di associazione implementino Clone mediante un costruttore di copia che chiami il costruttore di copia di base e che quindi duplichi i campi aggiuntivi in questa classe.  
  
 <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> – La proprietà <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A> restituisce lo schema URI per il protocollo di trasporto rappresentato dall'elemento di associazione.Ad esempio, le classi <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=fullName> e <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=fullName> restituiscono "http" e "net.tcp" dalle rispettive proprietà <xref:System.ServiceModel.Channels.TransportBindingElement.Scheme%2A>.  
  
#### Elementi di associazione di codifica  
 Per creare un nuovo elemento di associazione di codifica, iniziare estendendo la classe <xref:System.ServiceModel.Channels.BindingElement> e implementando la classe <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=fullName>.È necessario quindi implementare almeno i metodi <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> e <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A?displayProperty=fullName> e la proprietà <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.MessageVersion%2A?displayProperty=fullName>.  
  
-   <xref:System.ServiceModel.Channels.BindingElement.Clone%2A>.Restituisce una copia aggiornata dell'elemento di associazione.È consigliabile che gli autori dell'elemento di associazione implementino il metodo <xref:System.ServiceModel.Channels.BindingElement.Clone%2A> utilizzando un costruttore di copia che chiami il costruttore di copia di base e che quindi duplichi i campi aggiuntivi in questa classe.  
  
-   <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A>.Restituisce una classe <xref:System.ServiceModel.Channels.MessageEncoderFactory> che fornisce un handle alla classe effettiva che implementa il nuovo codificatore e che deve estendere la classe <xref:System.ServiceModel.Channels.MessageEncoder>.Per ulteriori informazioni, vedere <xref:System.ServiceModel.Channels.MessageEncoderFactory> e <xref:System.ServiceModel.Channels.MessageEncoder>.  
  
-   <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.MessageVersion%2A>.Restituisce la classe <xref:System.ServiceModel.Channels.MessageVersion> utilizzata in questa codifica, che rappresenta le versioni di SOAP e WS\-Addressing utilizzate.  
  
 Per un elenco completo dei metodi e delle proprietà facoltative per gli elementi di associazione di codifica definiti dall'utente, vedere <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.  
  
 Per ulteriori informazioni sulla creazione di un nuovo elemento di associazione, vedere [Creazione di associazioni definite dall'utente](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).  
  
 Una volta creato un elemento di associazione per il canale, tornare all'argomento [Sviluppo di canali](../../../../docs/framework/wcf/extending/developing-channels.md) per verificare se si desidera aggiungere il supporto file di configurazione all'elemento di associazione, se e come aggiungere il supporto per la pubblicazione di metadati e se e come costruire un'associazione definita dall'utente che gli utilizzi l'elemento di associazione.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.BindingElement>   
 [Sviluppo di canali](../../../../docs/framework/wcf/extending/developing-channels.md)   
 [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md)