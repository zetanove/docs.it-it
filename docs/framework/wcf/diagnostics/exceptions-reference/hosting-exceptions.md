---
title: "Eccezioni host | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad9e14f8-fa17-4d59-b365-fe0e7ec17c98
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Eccezioni host
In questo argomento vengono elencate tutte le eccezioni generate dall'host.  
  
## Elenco delle eccezioni  
  
|Codice risorsa|Stringa di risorsa|  
|--------------------|------------------------|  
|Hosting\_AddressIsAbsoluteUri|Non è consentito l'URI completo.Gli URI completi non sono consentiti per l'API ServiceHostingEnvironment.EnsureServiceAvailable.Utilizzare un percorso virtuale per il servizio corrispondente.|  
|Hosting\_BuildProviderCouldNotCreateType|Impossibile caricare il tipo CLR specificato durante la compilazione del servizio.Verificare che questo tipo sia definito in un file di origine nella directory \\\\App\_Code dell'applicazione, contenuta in un assembly compilato all'interno della directory \\\\bin dell'applicazione, oppure sia presente in un assembly installato nella cache di assembly globale.Al nome del tipo viene applicata la distinzione tra maiuscole e minuscole.Le directory quali \\\\App\_Code e \\\\bin devono essere incluse nella directory principale dell'applicazione.Le directory \\\\App\_Code e \\\\bin non possono essere annidate in sottodirectory.|