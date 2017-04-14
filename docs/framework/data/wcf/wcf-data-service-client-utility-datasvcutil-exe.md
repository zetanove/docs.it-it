---
title: "Utilit&#224; client di WCF Data Services (DataSvcUtil.exe) | Microsoft Docs"
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
  - "WCF Data Services, libreria client"
  - "WCF Data Services, utilizzo"
  - "WCF Data Services, generazione di classi di dati client"
ms.assetid: 9d0af606-929b-4c03-b307-3ef5f705afce
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Utilit&#224; client di WCF Data Services (DataSvcUtil.exe)
DataSvcUtil.exe è un strumento da riga di comando fornito da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] che consente di usare un feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] e di generare le classi del servizio dati client necessarie per accedere a un servizio dati da un'applicazione client .NET Framework.  Questa utilità consente di generare classi di dati usando le origini di metadati seguenti:  
  
-   L'URI radice di un servizio dati.  L'utilità richiede il documento dei metadati del servizio che descrive il modello di dati esposto dal servizio dati.  Per altre informazioni, vedere [OData: documento dei metadati del servizio](http://go.microsoft.com/fwlink/?LinkId=186070).  
  
-   Un file del modello di dati \(con estensione csdl\) definito tramite schema CSDL \(Conceptual Schema Definition Language\), come da specifica del [formato di file CSDL \(Conceptual Schema Definition Language\) \[MC\-CSDL\]](http://go.microsoft.com/fwlink/?LinkID=159072).  
  
-   Un file con estensione edmx creato usando gli strumenti di Entity Data Model forniti con Entity Framework.  Per altre informazioni, vedere la specifica di [Entity Data Model per il formato dei pacchetti di servizi dati \[MC\-EDMX\]](http://go.microsoft.com/fwlink/?LinkID=178833).  
  
 Per altre informazioni, vedere [Procedura: generare in modo manuale classi del servizio dati client](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md).  
  
 Lo strumento DataSvcUtil.exe viene installato nella directory [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  In molti casi, il file si trova in C:\\Windows\\Microsoft.NET\\Framework\\v4.0.  Per i sistemi a 64 bit, questa directory si trova in C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.  È inoltre possibile accedere allo strumento DataSvcUtil.exe dal prompt dei comandi di Visual Studio facendo clic sul pulsante **Start**, scegliendo **Tutti i programmi**, **Microsoft Visual Studio 2010**, **Visual Studio Tools**, quindi **Prompt dei comandi di Visual Studio 2010**.  
  
## Sintassi  
  
```  
datasvcutil /out:file [/in:file | /uri:serviceuri] [/dataservicecollection] [/language:devlang] [/nologo] [/version:ver] [/help]  
```  
  
#### Parametri  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|`/dataservicecollection`|Indica che verrà generato anche il codice necessario per l'associazione di oggetti a controlli.|  
|`/help`<br /><br /> \-oppure\-<br /><br /> `/?`|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|`/in:` *\<file\>*|Consente di specificare il file con estensione csdl o edmx oppure una directory in cui si trova il file.|  
|`/language:`\[VB&#124;CSharp\]|Consente di specificare il linguaggio per i file di codice sorgente generati.  Il linguaggio predefinito è C\#.|  
|`/nologo`|Consente di disattivare la visualizzazione del messaggio di copyright.|  
|`/out:` *\<file\>*|Consente di specificare il nome del file di codice sorgente contenente le classi del servizio dati client generate.|  
|`/uri:` *\<string\>*|URI del feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].|  
|`/version:`\[1.0&#124;2.0\]|Consente di specificare la versione accettata più recente di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  La versione viene determinata in base all'attributo `DataServiceVersion` dell'elemento DataService nei metadati del servizio dati restituiti.  Per altre informazioni, vedere [Controllo delle versioni del servizio dati](../../../../docs/framework/data/wcf/data-service-versioning-wcf-data-services.md).  Quando si specifica il parametro `/dataservicecollection`, è inoltre necessario specificare `/version:2.0` per abilitare l'associazione dati.|  
  
## Vedere anche  
 [Generazione della libreria client del servizio dati](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)   
 [Procedura: aggiungere un riferimento al servizio dati](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)