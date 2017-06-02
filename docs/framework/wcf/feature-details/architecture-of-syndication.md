---
title: "Architettura di diffusione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ed4ca86e-e3d8-4acb-87aa-1921fbc353be
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Architettura di diffusione
L'API di diffusione è progettata per fornire un modello di programmazione indipendente dal formato, che consente di scrivere in rete contenuto diffuso in molteplici formati.  Il modello di dati astratto è costituito dalle classi seguenti:  
  
-   <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 Queste classi eseguono il mapping in modo rigoroso ai costrutti definiti nella specifica Atom 1.0, anche se alcuni dei nomi sono diversi.  
  
 In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], i feed di diffusione sono modellati come un altro tipo di operazione del servizio, quello in cui il tipo restituito è una delle classi derivate di <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>.  Il recupero di un feed è modellato come uno scambio di messaggi richiesta\-risposta.  Un client invia una richiesta al servizio e il servizio risponde.  Il messaggio di richiesta viene impostato in un protocollo dell'infrastruttura, ad esempio il protocollo HTTP non elaborato, e il messaggio di risposta contiene un payload costituito da un formato di diffusione noto \(RSS 2.0 o Atom 1.0\).  I servizi che implementano questi scambi di messaggi sono denominati servizi di diffusione.  
  
 Il contratto di un servizio di diffusione è costituito da un set di operazioni che restituisce un'istanza della classe <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>.  Nell'esempio seguente viene illustrata una dichiarazione di interfaccia per un servizio di diffusione.  
  
 [!code-csharp[S_UE_SyndicationBoth#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_syndicationboth/cs/service.cs#0)]  
  
 Il supporto della diffusione è basato sul modello di programmazione REST di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che definisce l'associazione <xref:System.ServiceModel.WebHttpBinding>, usata insieme a <xref:System.ServiceModel.Description.WebHttpBehavior> per rendere disponibili i feed come servizi.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]l modello di programmazione REST di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Panoramica sul modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md).  
  
> [!NOTE]
>  La specifica Atom 1.0 consente di specificare secondi frazionari in uno qualsiasi dei costrutti data.  I secondi frazionari verranno ignorati dall'implementazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] durante la fase di serializzazione e deserializzazione.  
  
## Modello a oggetti  
 Il modello a oggetti per la diffusione è costituito dai gruppi di classi riportati nelle tabelle seguenti.  
  
 Classi di formattazione:  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter>|Classe che serializza un'istanza di <xref:System.ServiceModel.Syndication.SyndicationFeed> in formato Atom 1.0.|  
|<xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601>|Classe che serializza le classi derivate da <xref:System.ServiceModel.Syndication.SyndicationFeed> in formato Atom 1.0.|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter>|Classe che serializza un'istanza di <xref:System.ServiceModel.Syndication.SyndicationItem> in formato Atom 1.0.|  
|<xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601>|Classe che serializza le classi derivate da <xref:System.ServiceModel.Syndication.SyndicationItem> in formato Atom 1.0.|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter>|Classe che serializza un'istanza di <xref:System.ServiceModel.Syndication.SyndicationFeed> in formato RSS 2.0.|  
|<xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601>|Classe che serializza le classi derivate da <xref:System.ServiceModel.Syndication.SyndicationFeed> in formato RSS 2.0.|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter>|Classe che serializza un'istanza di <xref:System.ServiceModel.Syndication.SyndicationItem> in formato RSS 2.0.|  
|<xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601>|Classe che serializza le classi derivate da <xref:System.ServiceModel.Syndication.SyndicationItem> in formato RSS 2.0.|  
  
 Classi del modello a oggetti:  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.ServiceModel.Syndication.SyndicationCategory>|Classe che rappresenta la categoria di un feed di diffusione.|  
|<xref:System.ServiceModel.Syndication.SyndicationContent>|Classe di base che rappresenta il contenuto di diffusione.|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtension>|Classe che rappresenta un'estensione degli elementi di diffusione.|  
|<xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection>|Raccolta di oggetti <xref:System.ServiceModel.Syndication.SyndicationElementExtension>.|  
|<xref:System.ServiceModel.Syndication.SyndicationFeed>|Classe che rappresenta un oggetto feed di livello superiore.|  
|<xref:System.ServiceModel.Syndication.SyndicationItem>|Classe che rappresenta un elemento del feed.|  
|<xref:System.ServiceModel.Syndication.SyndicationLink>|Classe che rappresenta un collegamento all'interno di un feed di diffusione o di un elemento del feed.|  
|<xref:System.ServiceModel.Syndication.SyndicationPerson>|Classe che rappresenta un costrutto Person di Atom.|  
|<xref:System.ServiceModel.Syndication.SyndicationVersions>|Classe che rappresenta le versioni del protocollo di diffusione supportato.|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContent>|Classe che rappresenta qualsiasi contenuto <xref:System.ServiceModel.Syndication.SyndicationItem> da visualizzare per un utente finale.|  
|<xref:System.ServiceModel.Syndication.TextSyndicationContentKind>|Enumerazione che rappresenta i diversi tipi di contenuto di diffusione testo supportati.|  
|<xref:System.ServiceModel.Syndication.UrlSyndicationContent>|Classe che rappresenta il contenuto di diffusione costituito da un URL di un'altra risorsa.|  
|<xref:System.ServiceModel.Syndication.XmlSyndicationContent>|Classe che rappresenta il contenuto di diffusione non destinato alla visualizzazione in un browser.|  
  
 Le astrazioni dati di base nel modello a oggetti sono Feed e Item, che corrispondono alle classi <xref:System.ServiceModel.Syndication.SyndicationFeed> e <xref:System.ServiceModel.Syndication.SyndicationItem>.  Un Feed espone alcuni metadati di livello feed, ad esempio Title, Description e Author, un percorso per la memorizzazione di estensioni sconosciute e un set di elementi che costituiscono il resto del contenuto di informazioni del feed.  Un Item rende disponibili alcuni metadati di livello elemento, ad esempio, Title, Summary e PublicationDate, un percorso per archiviare estensioni sconosciute e un elemento contenuto che include il resto del contenuto di informazioni dell'elemento.  Le astrazioni di base di Feed e Item sono supportate da ulteriori classi che rappresentano costrutti dati comuni a cui si fa riferimento nelle specifiche Atom 1.0 e RSS.  
  
 Le informazioni veicolate in un'istanza di Feed possono essere convertite in una varietà di formati XML.  Il processo di conversione da e verso XML viene gestito dalla classe <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>.  Questa classe è astratta; ne vengono fornite implementazioni concrete <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> e <xref:System.ServiceModel.Syndication.Rss20FeedFormatter> per Atom 1.0 e RSS 2.0.  Per usare classi Feed derivate, usare <xref:System.ServiceModel.Syndication.Atom10FeedFormatter%601> o <xref:System.ServiceModel.Syndication.Rss20FeedFormatter%601>, poiché consentono di specificare una classe Feed derivata.  Per usare classi di elementi derivate, usare <xref:System.ServiceModel.Syndication.Atom10ItemFormatter%601> o <xref:System.ServiceModel.Syndication.Rss20ItemFormatter%601>, poiché consentono di specificare una classe di elementi derivata. Le terze parti possono derivare la propria implementazione di <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> per supportare formati di diffusione diversi.  
  
## Estendibilità  
  
-   Una funzionalità chiave dei protocolli di diffusione è l'estensibilità.  Sia Atom 1.0 che RSS 2.0 consentono di aggiungere ai feed di diffusione attributi ed elementi che non sono definiti nelle specifiche.  Il modello di programmazione della diffusione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] prevede due modalità di utilizzo di attributi ed estensioni personalizzati: derivazione di una nuova classe e accesso non fortemente tipizzato.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Estendibilità della diffusione](../../../../docs/framework/wcf/feature-details/syndication-extensibility.md).  
  
## Vedere anche  
 [Panoramica sulla diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)   
 [Modalità di mapping del modello a oggetti di diffusione WCF ad Atom e RSS](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md)   
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)