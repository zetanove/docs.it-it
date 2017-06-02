---
title: "Annunci di individuazione e client annunci | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 426c6437-f8d2-4968-b23a-18afd671aa4b
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Annunci di individuazione e client annunci
La funzionalità di individuazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente ai componenti di annunciare la propria disponibilità.Se viene configurato a tale scopo, un servizio invia annunci Hello e Bye.I client o altri componenti possono attendere tali messaggi dell'annuncio ed eseguire azioni su di loro.In questo modo viene fornito un metodo alternativo che consente ai client di essere consapevoli della presenza di servizi.La funzionalità degli annunci può essere utilizzata per vari scopi. Se ad esempio i servizi entrano ed escono periodicamente da una rete, gli annunci possono costituire un'alternativa migliore rispetto alla ricerca di servizi.Con questo approccio, il traffico di rete è ridotto e il client è in grado di sapere se un servizio è presente o assente contestualmente alla ricezione degli annunci.  
  
## Annunci di individuazione  
 Se un servizio configurato per gli annunci si unisce a una rete e diviene individuabile, invia un messaggio Hello che annuncia la propria disponibilità ai client in ascolto.Il messaggio contiene le informazioni relative all'individuazione sul servizio, ad esempio il contratto, l'indirizzo endpoint e gli ambiti associati.È possibile specificare la destinazione dell'invio del messaggio di annuncio con la classe <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>.Se l'endpoint annunci è un elemento <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>, Hello e Bye sono multicast, mentre se l'endpoint annunci è unicast, i messaggi vengono inviati direttamente all'endpoint specificato.  
  
> [!NOTE]
>  Gli annunci vengono inviati quando l'host del servizio viene aperto e chiuso.Se queste chiamate non vengono completate in modo corretto, è possibile che il messaggio dell'annuncio non venga inviato.Se ad esempio si verificano errori nel servizio, il messaggio di annuncio Bye non viene inviato.  
  
> [!TIP]
>  È possibile personalizzare la funzionalità di annunci, con la possibilità di inviare annunci in qualsiasi momento.  
  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] definisce <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> e <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> come endpoint standard per consentire a servizi e client di inviare facilmente annunci Hello e Bye.  
  
### Annunci sul servizio  
 Per configurare l'invio di annunci da parte del servizio, aggiungere un <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> con un endpoint annunci.Nell'esempio seguente viene mostrato come aggiungere a livello di codice questo comportamento all'host del servizio.In questo esempio viene utilizzato `UdpAnnouncementEndpoint`, che implica che gli annunci vengono inviati in multicast a un percorso specificato dallo specifico endpoint standard.  
  
```  
ServiceDiscoveryBehavior serviceDiscoveryBehavior = new ServiceDiscoveryBehavior();  
serviceDiscoveryBehavior.AnnouncementEndpoints.Add(new UdpAnnouncementEndpoint());  
serviceHost.Description.Behaviors.Add(serviceDiscoveryBehavior);  
```  
  
 È inoltre possibile configurare il comportamento nel file di configurazione, come indicato nell'esempio seguente.  
  
```  
<services>  
  <service behaviorConfiguration="CalculatorBehavior" name="Microsoft.Samples.Discovery.CalculatorService">  
    <!--Add Discovery Endpoint-->  
    <endpoint name="udpDiscoveryEpt" kind="udpDiscoveryEndpoint" />  
  </service>  
</services>  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorBehavior">  
      <!--Add Discovery behavior-->  
      <serviceDiscovery>  
        <announcementEndpoints>  
          <endpoint kind="udpAnnouncementEndpoint" />  
        </announcementEndpoints>  
      </serviceDiscovery>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Negli esempi precedenti viene configurato un servizio per inviare messaggi di annuncio in modo automatico.È inoltre possibile inviare messaggi di annuncio in modo esplicito tramite la classe <xref:System.ServiceModel.Discovery.AnnouncementClient>.  
  
### Annunci sul client  
 Un'applicazione client deve ospitare un servizio annunci per rispondere ai messaggi Hello e Bye ed eseguire la sottoscrizione agli eventi <xref:System.ServiceModel.Discovery.AnnouncementService.OnlineAnnouncementReceived> e <xref:System.ServiceModel.Discovery.AnnouncementService.OfflineAnnouncementReceived>.Nell'esempio seguente viene illustrato come effettuare questa operazione.  
  
```  
// Create an AnnouncementService instance  
AnnouncementService announcementService = new AnnouncementService();  
  
// Subscribe the announcement events  
announcementService.OnlineAnnouncementReceived += OnOnlineEvent;  
announcementService.OfflineAnnouncementReceived += OnOfflineEvent;  
  
// Create ServiceHost for the AnnouncementService  
using (ServiceHost announcementServiceHost = new ServiceHost(announcementService))  
{  
    // Listen for the announcements sent over UDP multicast  
    announcementServiceHost.AddServiceEndpoint(new UdpAnnouncementEndpoint());  
    announcementServiceHost.Open();  
  
    Console.WriteLine("Press <ENTER> to terminate.");  
    Console.ReadLine();  
}  
  
```  
  
 Alla ricezione di un messaggio Hello o Bye è possibile accedere ai metadati di individuazione di endpoint tramite <xref:System.ServiceModel.Discovery.AnnouncementEventArgs>, come indicato nell'esempio seguente.  
  
```  
static void OnOnlineEvent(object sender, AnnouncementEventArgs e)  
{  
    Console.WriteLine("Received an online announcement from {0}",   
e.EndpointDiscoveryMetadata.Address);  
}  
  
static void OnOfflineEvent(object sender, AnnouncementEventArgs e)  
{  
    Console.WriteLine("Received an offline announcement from {0}",   
e.EndpointDiscoveryMetadata.Address);  
}  
```