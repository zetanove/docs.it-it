---
title: "Creazione di associazioni definite dall&#39;utente | Microsoft Docs"
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
  - "associazioni definite dall'utente [WCF]"
ms.assetid: c4960675-d701-4bc9-b400-36a752fdd08b
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Creazione di associazioni definite dall&#39;utente
Esistono diversi modi per creare associazioni non fornite dal sistema:  
  
-   Creare un'associazione personalizzata, basata sulla classe <xref:System.ServiceModel.Channels.CustomBinding>, che è un contenitore riempito con elementi di associazione.  L'associazione personalizzata viene quindi aggiunta a un endpoint del servizio.  È possibile creare l'associazione personalizzata a livello di programmazione o in un file di configurazione dell'applicazione.  Per usare un elemento di associazione da un file di configurazione dell'applicazione, è necessario che l'elemento di associazione estenda <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle associazioni personalizzate, vedere [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md) e <xref:System.ServiceModel.Channels.CustomBinding>.  
  
-   È possibile creare una classe derivata da un'associazione standard.  È, ad esempio, possibile derivare una classe da <xref:System.ServiceModel.WSHttpBinding> ed eseguire l'override del metodo <xref:System.ServiceModel.Channels.CustomBinding.CreateBindingElements%2A> per ottenere gli elementi di associazione e inserire un elemento di associazione personalizzato o stabilire un particolare valore per la protezione.  
  
-   È possibile creare un nuovo tipo <xref:System.ServiceModel.Channels.Binding> per controllare completamente l'intera implementazione dell'associazione.  
  
## Ordine degli elementi di associazione  
 Ogni elemento di associazione rappresenta una fase di elaborazione durante l'invio o la ricezione di messaggi.  In fase di esecuzione, gli elementi di associazione creano i canali e i listener necessari per generare stack di canali in uscita e in ingresso.  
  
 Sono disponibili tre tipi di elementi di associazione: elementi di associazione di protocollo, elementi di associazione di codifica ed elementi di associazione del trasporto.  
  
 Elementi di associazione di protocollo: rappresentano passaggi di elaborazione di livello superiore che agiscono sui messaggi.  I canali e i listener creati da questi elementi di associazione possono aggiungere, rimuovere o modificare il contenuto del messaggio.  Una determinata associazione può avere un numero arbitrario di elementi di associazione di protocollo, ognuno dei quali eredita da <xref:System.ServiceModel.Channels.BindingElement>.  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] include diversi elementi di associazione di protocollo, tra cui <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> e <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.  
  
 Elementi di associazione di codifica: rappresentano trasformazioni tra un messaggio e una codifica pronti per la trasmissione in rete.  Le tipiche associazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] includono esattamente un elemento di associazione di codifica.  Tra gli esempi di elementi di associazione di codifica sono inclusi <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>, <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> e <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>.  Se non viene specificato alcun elemento di associazione di codifica per un'associazione, viene usata la codifica predefinita.  L'impostazione predefinita corrisponde a "testo", se il trasporto è HTTP, altrimenti a "binaria".  
  
 Elementi di associazione del trasporto: rappresentano la trasmissione di un messaggio di codifica su un protocollo di trasporto.  Le tipiche associazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] includono esattamente un elemento di associazione del trasporto, che eredita da <xref:System.ServiceModel.Channels.TransportBindingElement>.  Tra gli esempi di elementi di associazione del trasporto sono inclusi <xref:System.ServiceModel.Channels.TcpTransportBindingElement>, <xref:System.ServiceModel.Channels.HttpTransportBindingElement> e <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>.  
  
 Quando si creano nuove associazioni, l'ordine degli elementi di associazione aggiunti è importante.  Aggiungere sempre gli elementi di associazione nell'ordine seguente:  
  
|Livello|Opzioni|Obbligatorio|  
|-------------|-------------|------------------|  
|Flusso transazioni|<xref:System.ServiceModel.Channels.TransactionFlowBindingElement?displayProperty=fullName>|No|  
|Affidabilità|<xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=fullName>|No|  
|Sicurezza|<xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=fullName>|No|  
|Duplex composito|<xref:System.ServiceModel.Channels.CompositeDuplexBindingElement?displayProperty=fullName>|No|  
|Codifica|Testo, binario, MTOM, personalizzata|Sì\*|  
|Trasporto|TCP, named pipe, HTTP, HTTPS, MSMQ, personalizzato|Sì|  
  
 \*Dato che per ogni associazione è necessaria una codifica, se non viene specificata alcuna codifica, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ne aggiunge automaticamente una predefinita.  L'impostazione predefinita è Text\/XML per i trasporti HTTP e HTTPS e Binary per gli altri trasporti.  
  
## Creazione di un nuovo elemento di associazione  
 Oltre ai tipi derivati da <xref:System.ServiceModel.Channels.BindingElement> forniti da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è possibile creare propri elementi di associazione.  Questo consente di personalizzare la modalità di creazione dello stack di associazioni e di specificare i componenti in esso inclusi creando un proprio <xref:System.ServiceModel.Channels.BindingElement> che può essere composto con gli altri tipi forniti dal sistema nello stack.  
  
 Ad esempio, se si implementa un `LoggingBindingElement` che offre la possibilità di registrare il messaggio in un database, è necessario posizionare tale elemento sopra un canale di trasporto nello stack di canali.  In questo caso, l'applicazione crea un'associazione personalizzata che compone `LoggingBindingElement` con `TcpTransportBindingElement`, come nell'esempio seguente.  
  
```csharp  
Binding customBinding = new CustomBinding(  
  new LoggingBindingElement(),   
  new TcpTransportBindingElement()  
);  
```  
  
 La modalità di scrittura del nuovo elemento di associazione dipende dalla funzionalità esatta.  Uno degli esempi, [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md), fornisce una descrizione dettagliata di come implementare un tipo di elemento di associazione.  
  
## Creazione di una nuova associazione  
 Un elemento di associazione creato dall'utente può essere usato in due modi.  Nella sezione precedente è stato illustrato il primo modo, ovvero tramite un'associazione personalizzata.  Un'associazione personalizzata consente all'utente di creare una propria associazione basata su un set arbitrario di elementi di associazione, inclusi quelli creati dall'utente.  
  
 Se si usa l'associazione in più di un'applicazione, creare la propria associazione ed estendere <xref:System.ServiceModel.Channels.Binding>.  Questo evita di creare manualmente un'associazione personalizzata ogni volta che si desidera usarla.  Un'associazione definita dall'utente consente di definire il comportamento dell'associazione e includere elementi di associazione definiti dall'utente.  Inoltre è *preconfezionata*, ovvero non costringe a ricreare l'associazione ogni volta che la si usa.  
  
 Un'associazione definita dall'utente deve implementare almeno il metodo <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> e la proprietà <xref:System.ServiceModel.Channels.Binding.Scheme%2A>.  
  
 Il metodo <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> restituisce una nuova classe <xref:System.ServiceModel.Channels.BindingElementCollection> contenente gli elementi di associazione per l'associazione.  La raccolta è ordinata e deve contenere prima gli elementi di associazione di protocollo, seguiti dall'elemento di associazione di codifica, seguito dall'elemento di associazione del trasporto.  Quando si usano elementi di associazione forniti dal sistema [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è necessario seguire le regole di ordinamento degli elementi di associazione specificate in [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md).  Questa raccolta non deve mai fare riferimento a oggetti a cui si fa riferimento nella classe di associazioni definite dall'utente; gli autori delle associazioni devono pertanto restituire un `Clone()` di <xref:System.ServiceModel.Channels.BindingElementCollection> in ogni chiamata a <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A>.  
  
 La proprietà <xref:System.ServiceModel.Channels.Binding.Scheme%2A> rappresenta lo schema URI del protocollo di trasporto in uso nell'associazione.  Ad esempio, *WSHttpBinding* e *NetTcpBinding* restituiscono “http” e “net.tcp” dalle rispettive proprietà <xref:System.ServiceModel.Channels.Binding.Scheme%2A>.  
  
 Per un elenco completo delle proprietà e dei metodi facoltativi per le associazioni definite dall'utente, vedere <xref:System.ServiceModel.Channels.Binding>.  
  
### Esempio  
 In questo esempio viene implementata un'associazione di profilo in `SampleProfileUdpBinding`, che deriva da <xref:System.ServiceModel.Channels.Binding>.  `SampleProfileUdpBinding` contiene fino a quattro elementi di associazione: uno creato dall'utente \(`UdpTransportBindingElement`\) e tre forniti dal sistema: `TextMessageEncodingBindingElement`, `CompositeDuplexBindingElement` e `ReliableSessionBindingElement`.  
  
```  
public override BindingElementCollection CreateBindingElements()  
{     
    BindingElementCollection bindingElements = new BindingElementCollection();  
    if (ReliableSessionEnabled)  
    {  
        bindingElements.Add(session);  
        bindingElements.Add(compositeDuplex);  
    }  
    bindingElements.Add(encoding);  
    bindingElements.Add(transport);  
    return bindingElements.Clone();  
}  
```  
  
## Restrizioni di sicurezza con i contratti duplex  
 Non tutti gli elementi di associazione sono reciprocamente compatibili.  In particolare, esistono alcune restrizioni sugli elementi di associazione di sicurezza, se usati con contratti duplex.  
  
### Protezione monofase  
 È possibile implementare la sicurezza "monofase", in cui tutte le credenziali di sicurezza necessarie vengono inviate in un singolo messaggio, impostando l'attributo `negotiateServiceCredential` dell'elemento di configurazione \<message\> su `false`.  
  
 L'autenticazione monofase non funziona con i contratti duplex.  
  
 Per i contratti request\/reply, l'autenticazione monofase funziona solo se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IRequestSessionChannel>.  
  
 Per i contratti unidirezionali, l'autenticazione monofase funziona se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IRequestChannel>, <xref:System.ServiceModel.Channels.IRequestSessionChannel>, <xref:System.ServiceModel.Channels.IOutputChannel> o <xref:System.ServiceModel.Channels.IOutputSessionChannel>.  
  
### Token del contesto di sicurezza in modalità cookie  
 I token del contesto di sicurezza in modalità cookie non possono essere usati con contratti duplex.  
  
 Per i contratti request\/reply, i token del contesto di sicurezza in modalità cookie funzionano solo se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IRequestSessionChannel>.  
  
 Per i contratti unidirezionali, i token del contesto di sicurezza in modalità cookie funzionano se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IRequestSessionChannel>.  
  
### Token del contesto di sicurezza in modalità sessione  
 I token del contesto di sicurezza \(SCT\) in modalità sessione funzionano per i contratti duplex se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IDuplexChannel> o <xref:System.ServiceModel.Channels.IDuplexSessionChannel>.  
  
 I token del contesto di sicurezza \(SCT\) in modalità sessione funzionano per i contratti request\/reply se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IDuplexChannel>, <xref:System.ServiceModel.Channels.IDuplexSessionChannel>, <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IRequestSessionChannel>.  
  
 I token del contesto di sicurezza \(SCT\) in modalità sessione funzionano per i contratti unidirezionali se lo stack di associazioni sotto l'elemento di associazione di sicurezza supporta la creazione di istanze di <xref:System.ServiceModel.Channels.IDuplexChannel>, <xref:System.ServiceModel.Channels.IDuplexSessionChannel>, <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IRequestSessionChannel>.  
  
## Derivazione da un'associazione standard  
 Invece di creare una classe di associazioni completamente nuova, è possibile estendere una delle associazioni fornite dal sistema esistenti.  Analogamente al caso precedente, è necessario eseguire l'override del metodo <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> e della proprietà <xref:System.ServiceModel.Channels.Binding.Scheme%2A>.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.Binding>   
 [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md)