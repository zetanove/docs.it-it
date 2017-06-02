---
title: "Distribuzione di servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac361bfb-017d-4da9-a2d7-fc0fb72d65bb
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Distribuzione di servizi
In questo argomento viene illustrato come distribuire un'applicazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in un ambiente di runtime.  
  
## Scelta dell'ambiente di hosting per l'applicazione  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono progettati per essere eseguiti in qualsiasi processo di Windows che supporta codice gestito.Per diventare attivo, un servizio deve essere ospitato all'interno di un ambiente di runtime che lo crea e ne controlla il contesto e la durata.Le opzioni di hosting vanno dall'esecuzione in una semplice applicazione console ad ambienti server come un servizio Windows, Internet Information Services \(IIS\) o all'interno di un processo di lavoro gestito da Windows Activation Service \(WAS\).Per esaminare le diverse opzioni di hosting per l'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Servizi host](../../../../docs/framework/wcf/hosting-services.md).  
  
## Vedere anche  
 [Hosting](../../../../docs/framework/wcf/feature-details/hosting.md)   
 [Servizi host](../../../../docs/framework/wcf/hosting-services.md)