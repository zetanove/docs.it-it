---
title: "Modellazione e mapping | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: ec8a9515-3708-4cde-a688-4d8e6975f150
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Modellazione e mapping
In [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è possibile definire il modello concettuale, il modello di archiviazione e il mapping tra i due nella modalità che soddisfa meglio le esigenze dell'applicazione.  Gli strumenti di Entity Data Model disponibili in [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] consentono di creare un file con estensione [edmx](http://msdn.microsoft.com/it-it/f4c8e7ce-1db6-417e-9759-15f8b55155d4) da un database o un modello grafico e successivamente di aggiornare il file creato nel caso vengano apportate modifiche al database o al modello.  
  
 A partire da Entity Framework 4.1 è inoltre possibile creare un modello a livello di codice usando lo sviluppo Code First.  Esistono due scenari diversi per lo sviluppo Code First.  In entrambi i casi, lo sviluppatore definisce un modello codificando le definizioni di classi di .NET Framework e, successivamente, in modo facoltativo specifica la configurazione o il mapping aggiuntivo usando le annotazioni dei dati o l'API Fluent.  
  
 Per altre informazioni, vedere la pagina relativa alla [creazione e al mapping di un modello concettuale](http://go.microsoft.com/fwlink/?LinkId=235016).  
  
 È inoltre possibile usare il generatore di EDM, incluso in [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)].  EdmGen.exe genera file con estensione csdl, ssdl e msl da un'origine dati esistente.  È possibile inoltre creare il contenuto del modello e del mapping manualmente.  Per altre informazioni, vedere [Generatore EDM \(EdmGen.exe\)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md).