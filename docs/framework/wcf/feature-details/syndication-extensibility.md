---
title: "Estendibilit&#224; della diffusione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4d941175-74a2-4b15-81b3-086e8a95d25f
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Estendibilit&#224; della diffusione
L'API di diffusione è progettata per fornire un modello di programmazione di formato neutro che consente di scrivere in rete il contenuto diffuso in molteplici formati.Il modello di dati astratto è costituito dalle classi seguenti:  
  
-   <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
-   <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 Queste classi eseguono il mapping in modo rigoroso ai costrutti definiti nella specifica Atom 1.0, anche se alcuni dei nomi sono diversi.  
  
 Una funzionalità chiave dei protocolli di diffusione è l'estendibilità.Sia Atom 1.0 che RSS 2.0 aggiungono attributi ed elementi ai feed di diffusione che non sono definiti nelle specifiche.Il modello di programmazione della diffusione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] offre le modalità seguenti di utilizzare attributi personalizzati ed estensioni, accesso non fortemente tipizzato e derivazione di una nuova classe.  
  
## Accesso non fortemente tipizzato  
 L'aggiunta di estensioni tramite la derivazione di una nuova classe richiede che venga scritto codice aggiuntivo.Un'altra opzione consiste nell'accedere alle estensioni in modo non fortemente tipizzato.Tutti i tipi definiti nel modello di dati astratto di diffusione contengono le proprietà denominate `AttributeExtensions` e `ElementExtensions` \(con un'eccezione, <xref:System.ServiceModel.Syndication.SyndicationContent> ha una proprietà `AttributeExtensions` ma nessuna proprietà `ElementExtensions`\).Queste proprietà sono raccolte di estensioni non elaborate rispettivamente dai metodi `TryParseAttribute` e `TryParseElement`.È possibile accedere a queste estensioni non elaborate chiamando <xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection.ReadElementExtensions%2A?displayProperty=fullName> sulla proprietà `ElementExtensions` di <xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem>, <xref:System.ServiceModel.Syndication.SyndicationLink>, <xref:System.ServiceModel.Syndication.SyndicationPerson> e <xref:System.ServiceModel.Syndication.SyndicationCategory>.Questo set di metodi cerca tutte le estensioni con il nome e lo spazio dei nomi specificati, le deserializza singolarmente in istanze di `TExtension` e le restituisce come una raccolta di oggetti `TExtension`.  
  
## Derivazione di una nuova classe  
 È possibile derivare una nuova classe da qualsiasi classe di modello di dati astratto esistente.Adottare questo approccio quando si implementa un'applicazione in cui la maggior parte dei feed utilizzati ha un'estensione particolare.In questo argomento, la maggior parte dei feed utilizzati dal programma contiene un'estensione `MyExtension`.Per offrire una migliore esperienza di programmazione, eseguire le operazioni seguenti:  
  
-   Creare una classe in cui possano essere contenuti i dati dell'estensione.In questo caso, creare una classe chiamata MyExtension.  
  
-   Derivare una classe chiamata MyExtensionItem da <xref:System.ServiceModel.Syndication.SyndicationItem> per esporre una proprietà di tipo MyExtension a fini di programmabilità.  
  
-   Eseguire l'override di <xref:System.ServiceModel.Syndication.SyndicationItem.TryParseElement%28System.Xml.XmlReader%2CSystem.String%29> nella classe MyExtensionItem per creare l'istanza di una nuova istanza MyExtension quando viene letta una MyExtension.  
  
-   Eseguire l'override di <xref:System.ServiceModel.Syndication.SyndicationItem.WriteElementExtensions%28System.Xml.XmlWriter%2CSystem.String%29> nella classe MyExtensionItem per scrivere il contenuto della proprietà MyExtension in un writer XML.  
  
-   Derivare una classe chiamata MyExtensionFeed da <xref:System.ServiceModel.Syndication.SyndicationFeed>.  
  
-   Eseguire l'override di <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateItem> nella classe MyExtensionFeed per creare l'istanza di un MyExtensionItem anziché del <xref:System.ServiceModel.Syndication.SyndicationItem> predefinito.In <xref:System.ServiceModel.Syndication.SyndicationFeed> e <xref:System.ServiceModel.Syndication.SyndicationItem> è definita una serie di metodi in grado di creare oggetti <xref:System.ServiceModel.Syndication.SyndicationLink>, <xref:System.ServiceModel.Syndication.SyndicationCategory> e <xref:System.ServiceModel.Syndication.SyndicationPerson> \(ad esempio, <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateLink>, <xref:System.ServiceModel.Syndication.SyndicationFeed.CreateCategory> e <xref:System.ServiceModel.Syndication.SyndicationFeed.CreatePerson>\).Tutti possono essere sottoposti a override per creare una classe derivata personalizzata.  
  
## Vedere anche  
 [Panoramica sulla diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md)   
 [Architettura di diffusione](../../../../docs/framework/wcf/feature-details/architecture-of-syndication.md)