---
title: "Generazione della libreria client del servizio dati (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Aggiungi riferimento al servizio, finestra di dialogo"
  - "applicazioni client, WCF Data Services"
  - "WCF Data Services, libreria client"
ms.assetid: 314077c1-ac10-47e1-bed4-940b5462359d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Generazione della libreria client del servizio dati (WCF Data Services)
Un servizio dati che implementa [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] può restituire un documento dei metadati del servizio che descrive il modello di dati esposto dal feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Per altre informazioni, vedere [OData: documento dei metadati del servizio](http://go.microsoft.com/fwlink/?LinkId=186070). È possibile usare la finestra di dialogo **Aggiungi riferimento al servizio** in Visual Studio per aggiungere un riferimento a un servizio basato su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Quando si usa questo strumento per aggiungere un riferimento ai metadati restituiti da un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] in un progetto client, vengono eseguite automaticamente le azioni seguenti:  
  
-   Richiesta del documento dei metadati del servizio al servizio dati e interpretazione dei metadati restituiti.  
  
    > [!NOTE]
    >  I metadati restituiti vengono archiviati nel progetto client come file con estensione edmx.  Non è possibile aprire questo file con estensione edmx usando Entity Data Model Designer perché non presenta lo stesso formato di un file con estensione edmx usato da Entity Framework.  È possibile visualizzare questo file di metadati usando l'editor XML o qualsiasi editor di testo.  Per altre informazioni, vedere la specifica di [Entity Data Model per il formato dei pacchetti di servizi dati \[MC\-EDMX\]](http://go.microsoft.com/fwlink/?LinkID=178833).  
  
-   Generazione di una rappresentazione del servizio come classe contenitore di entità che eredita da <xref:System.Data.Services.Client.DataServiceContext>.  Il comportamento di questa classe contenitore di entità generata è simile a quello del contenitore di entità generato dagli strumenti di Entity Data Model.  Per altre informazioni, vedere [Object Services Overview \(Entity Framework\)](http://msdn.microsoft.com/it-it/43014cf9-c9cb-4538-bfbb-197820b60038).  
  
-   Generazione di classi di dati per i tipi di modello di dati individuati nei metadati del servizio.  
  
-   Aggiunta di un riferimento all'assembly `System.Data.Services.Client` per il progetto.  
  
 Per altre informazioni, vedere [Procedura: aggiungere un riferimento al servizio dati](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md).  
  
 Le classi del servizio dati client possono inoltre essere generate tramite lo strumento [DataSvcUtil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md) al prompt dei comandi.  Per altre informazioni, vedere [Procedura: generare in modo manuale classi del servizio dati client](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md).  
  
## Mapping dei tipi di dati client  
 Quando si usa la finestra di dialogo **Aggiungi riferimento al servizio** in Visual Studio o lo strumento `DataSvcUtil.exe` per generare classi di dati client basate su un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)], viene eseguito il mapping dei tipi di dati di .NET Framework ai tipi primitivi del modello di dati nel modo seguente:  
  
|Tipo del modello di dati|Tipi di dati di .NET Framework|  
|------------------------------|------------------------------------|  
|`Edm.Binary`|<xref:System.Byte> `[]`|  
|`Edm.Boolean`|<xref:System.Boolean>|  
|`Edm.Byte`|<xref:System.Byte>|  
|`Edm.DateTime`|<xref:System.DateTime>|  
|`Edm.Decimal`|<xref:System.Decimal>|  
|`Edm.Double`|<xref:System.Double>|  
|`Edm.Guid`|<xref:System.Guid>|  
|`Edm.Int16`|<xref:System.Int16>|  
|`Edm.Int32`|<xref:System.Int32>|  
|`Edm.Int64`|<xref:System.Int64>|  
|`Edm.SByte`|<xref:System.SByte>|  
|`Edm.Single`|<xref:System.Single>|  
|`Edm.String`|<xref:System.String>|  
  
 Per altre informazioni, vedere [OData: tipi di dati primitivi](http://go.microsoft.com/fwlink/?LinkId=186072).  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)