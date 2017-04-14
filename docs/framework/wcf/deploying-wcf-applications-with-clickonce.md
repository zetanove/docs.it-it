---
title: "Distribuzione di applicazioni WCF con ClickOnce | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1a11feee-2a47-4d3e-a28a-ad69d5ff93e0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Distribuzione di applicazioni WCF con ClickOnce
Le applicazioni client che utilizzano [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] possono essere distribuite tramite la tecnologia ClickOnce.Questa tecnologia consente loro di avvalersi delle protezioni runtime fornite dalla protezione dall'accesso di codice, purché siano firmate digitalmente con un certificato attendibile.Il certificato utilizzato per firmare l'applicazione ClickOnce deve risiedere nell'archivio autori attendibili e il criterio di sicurezza locale nel computer client deve essere configurato per concedere autorizzazioni di attendibilità totale alle applicazioni firmate con il certificato dell'autore.  
  
 Per informazioni sulla configurazione di applicazioni ClickOnce e di autori attendibili, vedere [Configurazione di autori attendibili ClickOnce](http://go.microsoft.com/fwlink/?LinkId=94774) \(il contenuto potrebbe essere in inglese\).  
  
## Vedere anche  
 [Cenni preliminari sulla distribuzione di applicazioni attendibili](http://go.microsoft.com/fwlink/?LinkId=94775)   
 [Distribuzione ClickOnce per applicazioni Windows Form](http://go.microsoft.com/fwlink/?LinkId=94776)