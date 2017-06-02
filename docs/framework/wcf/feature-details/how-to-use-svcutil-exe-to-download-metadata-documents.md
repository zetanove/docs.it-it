---
title: "Procedura: utilizzare Svcutil.exe per scaricare documenti di metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15524274-3167-4627-b722-d6cedb9fa8c6
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Procedura: utilizzare Svcutil.exe per scaricare documenti di metadati
È possibile utilizzare Svcutil.exe per scaricare i metadati dai servizi in esecuzione e salvarli in file locali.Per schemi URL HTTP e HTTPS, Svcutil.exe tenta di recuperare i metadati mediante WS\-MetadataExchange e l'[individuazione di servizi Web XML](http://go.microsoft.com/fwlink/?LinkId=94950).Per tutti gli altri schemi URL, Svcutil.exe utilizza solo WS\-MetadataExchange.  
  
 Per impostazione predefinita, Svcutil.exe utilizza le associazioni definite nella classe <xref:System.ServiceModel.Description.MetadataExchangeBindings>.Per configurare l'associazione utilizzata per WS\-MetadataExchange, nel file di configurazione di Svcutil.exe \(svcutil.exe.config\) è necessario definire un endpoint client che utilizza il contratto `IMetadataExchange` e che ha lo stesso nome dello schema URI \(Uniform Resource Identifier\) dell'indirizzo dell'endpoint dei metadati.  
  
> [!CAUTION]
>  Quando si esegue Svcutil.exe per ottenere metadati per un servizio che espone due contratti di servizio diversi, ciascuno dei quali contiene un'operazione dello stesso nome, in Svcutil.exe viene visualizzato un messaggio di errore del tipo "Impossibile ottenere metadati da....". Se ad esempio è presente un servizio che espone un contratto di servizio denominato ICarService con un'operazione Get\(Car c\) e lo stesso servizio espone un contratto di servizio denominato IBookService con un'operazione Get\(Book b\), si verifica un errore.Per risolvere il problema, effettuare una delle operazioni seguenti:  
>   
>  -   Rinominare una delle operazioni.  
> -   Impostare <xref:System.ServiceModel.OperationContractAttribute.Name%2A> su un nome diverso.  
> -   Impostare uno degli spazi dei nomi delle operazioni su uno spazio dei nomi diverso, utilizzando la proprietà <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A>.  
  
### Per scaricare metadati utilizzando Svcutil.exe  
  
1.  Individuare lo strumento Svcutil.exe nel percorso seguente:  
  
     C:\\Programmi\\Microsoft SDKs\\Windows\\v1.0.\\bin  
  
2.  Al prompt dei comandi, avviare lo strumento utilizzando il formato seguente.  
  
    ```  
    svcutil.exe /t:metadata  <url>* | <epr>  
    ```  
  
     Per scaricare i metadati, è necessario specificare l'opzione `/t:metadata`.In caso contrario, verranno generati il codice client e la configurazione.  
  
3.  L'argomento \<`url`\>specifica l'URL a un endpoint del servizio che fornisce metadati o a un documento di metadati ospitato online.L'argomento \<`epr`\> specifica il percorso di un file XML contenente un WS\-Addressing `EndpointAddress` per un endpoint del servizio che supporta WS\-MetadataExchange.  
  
 Per ulteriori opzioni per l'utilizzo di questo strumento per scaricare i metadati, vedere [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
## Esempio  
 Con il comando seguente vengono scaricati i documenti di metadati da un servizio in esecuzione.  
  
```  
svcutil /t:metadata http://service/metadataEndpoint  
```  
  
## Vedere anche  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)