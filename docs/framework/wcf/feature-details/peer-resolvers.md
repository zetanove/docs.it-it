---
title: "Resolver del peer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d86d12a1-7358-450f-9727-b6afb95adb9c
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Resolver del peer
Per connettersi a una mesh, un nodo peer necessita dell'indirizzo IP di altri nodi.  Gli indirizzi IP si ottengono contattando un servizio resolver, che accetta l'ID della rete e restituisce un elenco di indirizzi corrispondenti ai nodi registrati con quel particolare ID di rete.  Il resolver mantiene un elenco di indirizzi registrati, creato facendo in modo che ogni nodo nella mesh venga registrato con il servizio.  
  
 È possibile specificare il servizio PeerResolver da usare tramite la proprietà `Resolver` di <xref:System.ServiceModel.NetPeerTcpBinding>.  
  
## Resolver peer supportati  
 Il canale peer supporta due tipi di resolver, il protocollo PNRP \(Peer Name Resolution Protocol\) e i servizi resolver personalizzati.  
  
 Per impostazione predefinita, il canale peer usa il servizio resolver peer PNRP per l'individuazione di peer e di elementi adiacenti nella rete.  Per le situazioni o le piattaforme in cui PNRP non è disponibile o applicabile, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce un'alternativa, il servizio di individuazione basato su server <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>.  È possibile definire anche in modo esplicito un servizio resolver personalizzato scrivendo una classe che implementa l'interfaccia <xref:System.ServiceModel.PeerResolvers.IPeerResolverContract>.  
  
### Protocollo PNRP \(Peer Name Resolution Protocol\)  
 PNRP, resolver predefinito di [!INCLUDE[wv](../../../../includes/wv-md.md)], è un servizio di risoluzione dei nomi distribuito senza server.  PNRP può essere usato anche in [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] installando l'Advanced Networking Pack.  Due client qualsiasi che eseguono la stessa versione di PNRP possono individuarsi reciprocamente usando questo protocollo, a condizione di soddisfare determinate condizioni, ad esempio il mancato intervento di un firewall aziendale.  Si noti che la versione di PNRP fornita con [!INCLUDE[wv](../../../../includes/wv-md.md)] è più recente di quella inclusa nell'Advanced Networking Pack.  Verificare l'Area download Microsoft per gli aggiornamenti a PNRP per [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)].  
  
### Servizi resolver personalizzati  
 Quando il servizio PNRP non è disponibile o si desidera disporre del controllo completo sulla definizione della rete, è possibile usare un servizio resolver basato su server personalizzato.  È possibile definire questo servizio in modo esplicito scrivendo una classe resolver che implementi l'interfaccia <xref:System.ServiceModel.PeerResolvers.IPeerResolverContract> o usando l'implementazione predefinita inclusa <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>.  
  
 Nell'implementazione predefinita del servizio, le registrazioni client scadono dopo un determinato periodo di tempo se non vengono esplicitamente aggiornate.  I client che usano il servizio resolver devono conoscere il limite superiore della latenza client\-server per poter aggiornare correttamente le registrazioni entro il periodo di tempo previsto.  Questo implica la scelta di un timeout di aggiornamento appropriato \(`RefreshInterval`\) sul servizio resolver.  Per altre informazioni, vedere [CustomPeerResolverService: registrazioni client](../../../../docs/framework/wcf/feature-details/inside-the-custompeerresolverservice-client-registrations.md).  
  
 L'autore dell'applicazione deve prendere in considerazione anche la protezione della connessione tra i client e il servizio resolver personalizzato.  A questo scopo è possibile usare impostazioni di sicurezza sulla classe <xref:System.ServiceModel.NetTcpBinding> usata dai client per contattare il servizio resolver.  È necessario specificare credenziali \(se usate\) sulla classe `ChannelFactory` usata per creare il canale peer.  Queste credenziali vengono passate alla classe `ChannelFactory` usa per creare canali per il resolver personalizzato.  
  
> [!NOTE]
>  Quando si usano reti locali e improvvisate con un resolver personalizzato, è consigliabile che le applicazioni che usano o supportano reti improvvisate e locali rispetto al collegamento includano la logica per la selezione di un solo indirizzo locale rispetto al collegamento da usare per la connessione.  Ciò evita la confusione che può essere causata da computer con più indirizzi locali rispetto al collegamento.  In conformità a quanto sopra, il canale peer supporta l'uso di un solo indirizzo di collegamento locale alla volta.  È possibile specificare questo indirizzo con la proprietà `ListenIpAddress` sulla classe <xref:System.ServiceModel.NetPeerTcpBinding>.  
  
 Per una dimostrazione sull'implementazione di un resolver personalizzato, vedere [Peer Channel Custom Peer Resolver](http://msdn.microsoft.com/it-it/5b75a2bb-7ff1-4a14-abe7-3debf0537d23).  
  
## Contenuto della sezione  
 [CustomPeerResolverService: registrazioni client](../../../../docs/framework/wcf/feature-details/inside-the-custompeerresolverservice-client-registrations.md)  
  
## Vedere anche  
 [Concetti relativi al canale peer](../../../../docs/framework/wcf/feature-details/peer-channel-concepts.md)   
 [Protezione del canale peer](../../../../docs/framework/wcf/feature-details/peer-channel-security.md)   
 [Creazione di un'applicazione del canale peer](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)