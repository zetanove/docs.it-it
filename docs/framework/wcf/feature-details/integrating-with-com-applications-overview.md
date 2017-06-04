---
title: "Panoramica sull&#39;integrazione con applicazioni COM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "COM [WCF], cenni preliminari sull'integrazione"
ms.assetid: 02c5697f-6e2e-47d6-b715-f3a28aebfbd5
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Panoramica sull&#39;integrazione con applicazioni COM
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce allo sviluppatore di codice gestito un ambiente completo per la creazione di applicazioni connesse.Se tuttavia si dispone di una grande quantità di codice non gestito basato su COM e non si desidera eseguirne la migrazione, è comunque possibile integrare i servizi Web [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] direttamente nel codice esistente utilizzando il moniker del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Il moniker del servizio può essere utilizzato in un'ampia gamma di ambienti di sviluppo basati su COM, ad esempio Office VBA, Visual Basic 6.0 o Visual C\+\+ 6.0.  
  
> [!NOTE]
>  Il moniker del servizio utilizza un canale di comunicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per tutte le comunicazioni.I meccanismi di sicurezza e identità per tale canale differiscono da quelli utilizzati nei proxy COM e DCOM standard.Inoltre, poiché il moniker del servizio utilizza un canale di comunicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], il periodo di timeout predefinito è di un minuto per tutte le chiamate.  
  
 Il moniker del servizio viene utilizzato con la funzione `GetObject` per fornire allo sviluppatore di codice non gestito un approccio specifico COM fortemente tipizzato per chiamare i servizi Web [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].A tale scopo è necessaria una definizione locale visibile a COM del contratto del servizio Web [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e dell'associazione da utilizzare.Come altri client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], il moniker del servizio deve costruire un canale tipizzato per il servizio, anche se la costruzione di tale canale avviene in modo trasparente per il programmatore COM alla prima chiamata al metodo.  
  
 In comune con altri client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], quando si utilizza il moniker, le applicazioni specificano l'indirizzo, l'associazione e il contratto per comunicare con un servizio.Il contratto può essere specificato in uno dei modi seguenti:  
  
-   Contratto tipizzato: il contratto viene registrato come tipo visibile a COM sul computer client.  
  
-   Contratto WSDL: il contratto viene fornito sotto forma di documento WSDL.  
  
-   Contratto MEX: il contratto viene recuperato in fase di esecuzione da un endpoint MEX \(Metadata Exchange\).  
  
## Parametri supportati dal moniker del servizio  
 Nella tabella seguente vengono illustrati i parametri supportati dal moniker del servizio.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|`address`|Percorso URL del servizio.|  
|`binding`|Nome della sezione dell'associazione ottenuto dalla configurazione dell'applicazione.|  
|`bindingConfiguration`|Istanza dell'associazione non anonima ottenuta dall'interno la sezione dell'associazione non anonima.|  
|`contract`|Identificatore di interfaccia \(IID\) che rappresenta il contratto del servizio o il nome del contratto \(ottenuto da MEX\).|  
|`wsdl`|Documento WSDL che fornisce un tipo alternativo di definizione del contratto.|  
|`spnIdentity`|Identità del nome principale del server \(SPN\) da utilizzare per comunicare con il servizio.|  
|`upnIdentity`|Identità del nome di entità utente \(UPN\) da utilizzare per comunicare con il servizio.|  
|`dnsIdentity`|Identità DNS da utilizzare per comunicare con il servizio.|  
|`mexAddress`|Percorso URL dell'endpoint MEX \(Metadata Exchange\) del servizio.|  
|`mexBinding`|Nome della sezione dell'associazione ottenuto dalla configurazione dell'applicazione da connettere con l'endpoint MEX.|  
|`mexBindingConfiguration`|Istanza dell'associazione non anonima ottenuta dall'interno della sezione dell'associazione non anonima da connettere con l'endpoint MEX.|  
|`bindingNamespace`|Spazio dei nomi del nome della sezione dell'associazione ottenuto dal MEX recuperato.|  
|`contractNamespace`|Spazio dei nomi del contratto ottenuto dal MEX recuperato.|  
|`mexSpnIdentity`|Identità del nome principale del server \(SPN\) da utilizzare per comunicare con l'endpoint MEX.|  
|`mexUpnIdentity`|Identità del nome dell'entità utente \(UPN\) da utilizzare per comunicare con l'endpoint MEX.|  
|`mexDnsIdentity`|Identità DNS da utilizzare per comunicare con l'endpoint MEX.|  
|`serializer`|Consente di specificare l'utilizzo del serializzatore "xml" o "datacontract."|  
  
> [!NOTE]
>  Anche quando il moniker del servizio viene utilizzato con client interamente basati su COM, è necessario che nel computer client siano installati [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e .NET Framework 2.0.È inoltre fondamentale che le applicazioni client che utilizzano il moniker del servizio carichino la versione appropriata del runtime .NET Framework.Quando il moniker viene utilizzato all'interno di applicazioni Office, può essere necessario un file di configurazione per garantire il caricamento della versione corretta del framework.Ad esempio, con Excel, è consigliabile inserire il testo seguente in un file denominato Excel.exe.config nella stessa directory del file Excel.exe:  
>   
>  `<?xml version="1.0" encoding="utf-8"?>`  
>   
>  `<configuration xmlns=` `http://schemas.microsoft.com/.NetConfiguration/v2.0` `>`  
>   
>  `<startup>`  
>   
>  `<requiredRuntime version="v2.0.50727" />`  
>   
>  `</startup>`  
>   
>  `</configuration>`  
  
## Vedere anche  
 [Procedura: registrare e configurare un moniker servizio](../../../../docs/framework/wcf/feature-details/how-to-register-and-configure-a-service-moniker.md)