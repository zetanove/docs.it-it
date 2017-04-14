---
title: "Procedura: generare in modo manuale classi del servizio dati client (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, configurazione"
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: generare in modo manuale classi del servizio dati client (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] si integra con Visual Studio per consentire la generazione automatica di classi del servizio dati client quando si usa la finestra di dialogo **Aggiungi riferimento al servizio** per aggiungere un riferimento a un servizio dati in un progetto di Visual Studio.  Per altre informazioni, vedere [Procedura: aggiungere un riferimento al servizio dati](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md).  È inoltre possibile generare in modo manuale le stesse classi del servizio dati client usando lo strumento per la generazione del codice, ovvero `DataSvcUtil.exe`. Questo strumento, incluso con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], consente di generare classi di .NET Framework in base alla definizione del servizio dati.  Può inoltre essere usato per generare classi del servizio dati in base al file del modello concettuale \(CSDL\) e al file con estensione edmx che rappresenta un modello di Entity Framework in un progetto di Visual Studio.  
  
 Nell'esempio riportato in questo argomento vengono create le classi del servizio dati client in base al servizio dati Northwind di esempio.  Questo servizio viene creato al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  Per alcuni esempi inclusi in questo argomento è richiesto il file del modello concettuale per il modello Northwind.  Per altre informazioni, vedere [Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping](../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  Per alcuni esempi inclusi in questo argomento è richiesto il file con estensione edmx per il modello Northwind.  Per altre informazioni, vedere [.edmx File Overview](http://msdn.microsoft.com/it-it/f4c8e7ce-1db6-417e-9759-15f8b55155d4).  
  
### Per generare classi C\# che supportano l'associazione dati  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  È necessario sostituire il valore fornito al parametro `/uri:` con l'URI dell'istanza del servizio dati Northwind di esempio.  
  
### Per generare Visual Basic che supportano l'associazione dati  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  È necessario sostituire il valore fornito al parametro `/uri:` con l'URI dell'istanza del servizio dati Northwind di esempio.  
  
### Per generare classi C\# basate sull'URI del servizio  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  È necessario sostituire il valore fornito al parametro `/uri:` con l'URI dell'istanza del servizio dati Northwind di esempio.  
  
### Per generare classi Visual Basic basate sull'URI del servizio  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  È necessario sostituire il valore fornito al parametro `/uri:` con l'URI dell'istanza del servizio dati Northwind di esempio.  
  
### Per generare classi C\# basate sul file del modello concettuale \(CSDL\)  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs  
    ```  
  
### Per generare classi Visual Basic basate sul file del modello concettuale \(CSDL\)  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb  
    ```  
  
### Per generare classi C\# basate sul file con estensione edmx  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs   
    ```  
  
### Per generare classi Visual Basic basate sul file con estensione edmx  
  
-   Al prompt dei comandi eseguire il comando seguente senza interruzioni di riga:  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb   
    ```  
  
## Vedere anche  
 [Generazione della libreria client del servizio dati](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)   
 [Procedura: aggiungere un riferimento al servizio dati](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)   
 [Utilità client di WCF Data Services \(DataSvcUtil.exe\)](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md)