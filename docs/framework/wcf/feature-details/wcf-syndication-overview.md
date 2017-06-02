---
title: "Panoramica sulla diffusione WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: af6d4c39-e5e8-4099-aee6-5261feff9107
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Panoramica sulla diffusione WCF
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce il supporto per l'esposizione di feed di diffusione da un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].La diffusione è un meccanismo di integrazione delle applicazioni in cui un server espone alcuni dati dell'applicazione in un formato interoperativo noto come feed.Un feed è una raccolta di dati dell'applicazione costituito da alcuni metadati a livello feed \(titolo, autore, URL e altri metadati\) e da una serie di elementi feed.All'interno del feed, gli elementi feed sono di solito organizzati in ordine cronologico inverso.Un elemento feed è costituito da un set standard di metadati di livello feed \(titolo, URL, data di creazione, categoria e altri metadati di livello elemento\) e da una quantità arbitraria di dati specifici dell'applicazione.I due tipi più comuni di feed di diffusione sono RSS \(Really Simple Syndication\) 2.0 e Atom 1.0, entrambi supportati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Modello a oggetti  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] definisce un set di classi specifiche della diffusione che consentono di utilizzare feed, elementi feed e metadati correlati in modo indipendente dal formato: <xref:System.ServiceModel.Syndication.SyndicationFeed>, <xref:System.ServiceModel.Syndication.SyndicationItem>, <xref:System.ServiceModel.Syndication.SyndicationPerson>, <xref:System.ServiceModel.Syndication.SyndicationLink> e altre classi specifiche della diffusione.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] definisce inoltre classi di infrastruttura, basate sul modello di programmazione WCF REST, per fornire il supporto della diffusione, tra cui: <xref:System.ServiceModel.Syndication.Atom10FeedFormatter> e <xref:System.ServiceModel.Syndication.RSS20FeedFormatter>.Le classi formatter di feed supportano la serializzazione del modello a oggetti da e verso RSS 2.0 e Atom 1.0.  
  
## Scenari  
 Un utilizzo comune della diffusione è oggi rappresentato dal blogging, processo con cui l'autore di un blog pubblica periodicamente alcuni tipi di informazioni,tra cui testo, immagini o audio.Anche molti giornali e riviste pubblicano nuove storie o articoli utilizzando la diffusione.Eseguendo la sottoscrizione a un feed di questo genere, un utente può ricevere tutte le nuove informazioni provenienti da tali siti.Anche se la diffusione è più frequentemente associata a blog ed editori, può essere utilizzata con qualsiasi applicazione che esponga una raccolta di informazioni; ad esempio, un database dei bug che si desidera esporre utilizzando un feed di diffusione.È possibile creare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che espone un'operazione denominata `CodeDefects`.Questa operazione può accettare un parametro che specifica l'indirizzo di posta elettronica della persona di cui si desidera recuperare i bug.Un client può utilizzare l'URL seguente per chiamare l'operazione: http:\/\/someserver\/bugDatabase\/CodeDefects?user\=johndoe.  
  
## Formati di diffusione  
 La piattaforma di diffusione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta RSS 2.0 e Atom 1.0.  
  
## Vedere anche  
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)