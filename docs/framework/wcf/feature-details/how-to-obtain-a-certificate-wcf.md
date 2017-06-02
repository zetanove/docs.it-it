---
title: "Procedura: ottenere un certificato (WCF) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "certificati [WCF], acquisizione"
ms.assetid: d53762fd-15ea-42dc-b0ea-6a6597aa23f7
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: ottenere un certificato (WCF)
Per usare una qualsiasi delle funzionalità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che usano certificati X.509, è necessario prima ottenere i certificati.  
  
### Per ottenere un certificato X.509  
  
1.  Effettuare una delle seguenti operazioni:  
  
    -   Acquistare un certificato da un'autorità di certificazione, ad esempio VeriSign, Inc.  
  
    -   Configurare il proprio servizio certificati e fare in modo che un'autorità di certificazione firmi i certificati.  [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], Windows 2000 Server, Windows 2000 Datacenter Server e Windows 2000 Datacenter Server includono tutti servizi certificati che supportano l'infrastruttura a chiave pubblica \(PKI\).  In Windows Server 2008 usare il ruolo [Servizi certificati Active Directory](http://go.microsoft.com/fwlink/?LinkID=153483) per gestire un'autorità di certificazione.  
  
    -   Configurare un proprio servizio certificati e non far firmare i certificati.  
  
    > [!NOTE]
    >  Indipendentemente dall'approccio adottato, il destinatario della richiesta SOAP che contiene il certificato X.509 deve considerare attendibile il certificato X.509.  Questo significa che il certificato X.509 o un'autorità emittente nella catena di certificati si trova nell'archivio certificati Persone attendibili e che il certificato X.509 non si trova nell'archivio Certificati non disponibili nell'elenco locale.  
  
## Vedere anche  
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Procedura: creare certificati temporanei da usare durante lo sviluppo](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)