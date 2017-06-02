---
title: "Procedura: usare Svcutil.exe per convalidare il codice del servizio compilato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d0d820fb-41c2-45b8-8f22-0fa5aeebbbaa
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: usare Svcutil.exe per convalidare il codice del servizio compilato
È possibile usare [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per rilevare errori in implementazioni e configurazioni del servizio senza ospitare il servizio.  
  
### Per convalidare un servizio  
  
1.  Compilare il servizio in un file eseguibile e in uno o più assembly dipendenti.  
  
2.  Aprire un prompt dei comandi SDK.  
  
3.  Al prompt dei comandi, avviare lo strumento Svcutil.exe usando il formato seguente.  Per altre informazioni sui vari parametri, vedere la sezione Convalida del servizio nell'argomento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
    ```  
    svcutil.exe /validate /serviceName:<serviceConfigName>  <assemblyPath>*  
    ```  
  
     È necessario usare l'opzione `/serviceName` per indicare il nome di configurazione del servizio che si desidera convalidare.  
  
     L'argomento `assemblyPath` specifica il percorso del file eseguibile per il servizio e uno o più assembly che contengono i tipi di servizio da convalidare.  L'assembly eseguibile deve avere un file di configurazione associato per fornire la configurazione del servizio.  È possibile usare caratteri jolly della riga di comando standard per fornire più assembly.  
  
## Esempio  
 Il comando seguente implementa il servizio myServiceName nel file eseguibile myServiceHost.exe.  Il file di configurazione per il servizio \(myServiceHost.exe.config\) viene automaticamente caricato.  
  
```  
svcutil /validate /serviceName:myServiceName myServiceHost.exe  
```  
  
## Vedere anche  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)