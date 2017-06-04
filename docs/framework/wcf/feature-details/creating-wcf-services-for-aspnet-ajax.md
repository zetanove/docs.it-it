---
title: "Creazione di servizi WCF per ASP.NET AJAX | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04c0402c-e617-4ba5-aedf-d17692234776
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Creazione di servizi WCF per ASP.NET AJAX
Microsoft ASP.NET AJAX consente di creare rapidamente pagine Web caratterizzate da un'esperienza utente più soddisfacente con i classici elementi dell'interfaccia utente di elevata reattività.ASP.NET AJAX fornisce librerie di script client in cui sono incorporate tecnologie multibrowser ECMAScript \(JavaScript\) e DHTML \(HTML dinamico\), nonché l'integrazione con la piattaforma di sviluppo basata su server ASP.NET 2.0.Con ASP.NET AJAX è possibile migliorare l'esperienza utente e l'efficienza delle applicazioni Web.  
  
 ASP.NET AJAX è costituito da librerie di script client e da componenti server integrati per fornire un framework di sviluppo affidabile.Per accedere a un servizio da una pagina ASP.NET: dopo l'aggiunta dell'URL del servizio al controllo Script Manager di ASP.NET nella pagina, è possibile richiamare le operazioni del servizio utilizzando codice JavaScript che assomiglia esattamente a una normale chiamata alla funzione JavaScript.Per informazioni sull'utilizzo di servizi Web all'interno del framework AJAX, vedere [Learn ASP.NET AJAX](http://go.microsoft.com/fwlink/?LinkId=186475).  
  
 La maggior parte dei servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] può essere esposta come servizio compatibile con ASP.NET AJAX aggiungendo un endpoint ASP.NET AJAX appropriato.  
  
 Se si sta utilizzando Visual Studio, è possibile utilizzare un modello predefinito per i servizi WCF compatibili AJAX, disponibile nella finestra di dialogo **Aggiungi nuovo elemento** quando si lavora con siti Web ASP.NET o applicazioni Web.  
  
 Se non si stanno utilizzando i modelli di Visual Studio, esistono due modalità per creare un endpoint ASP.NET AJAX:  
  
-   Creare l'endpoint utilizzando l'attivazione dinamica dell'host senza utilizzare alcuna configurazione.Questo è l'approccio più elementare se non si conosce il sistema di configurazione WCF.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: aggiungere un endpoint ASP.NET AJAX senza utilizzare la configurazione](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).  
  
-   Aggiungere un endpoint compatibile AJAX a un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando la configurazione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: aggiungere un endpoint ASP.NET AJAX con l'utilizzo della configurazione](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md).  
  
 Il modello di programmazione Web descritto in [Panoramica sul modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md) può essere utilizzato con i servizi ASP.NET AJAX.In particolare:  
  
-   È possibile utilizzare gli attributi <xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute> per selezionare tra i verbi HTTP GET e HTTP POST.Se utilizzati correttamente, possono migliorare notevolmente le prestazioni dell'applicazione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: scegliere tra richieste HTTP POST e HTTP GET per gli endpoint ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md).  
  
-   È possibile utilizzare le proprietà <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> e <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A> per fare in modo che il servizio restituisca dati XML anziché la notazione JSON \(JavaScript Object Notation\) predefinita.L'utilizzo di questo approccio con il framework ASP.NET AJAX fa sì che il client JavaScript riceva un oggetto XML DOM.  
  
    > [!WARNING]
    >  Per funzionare, l'operazione deve impostare il tipo di contenuto su Text\/XML.In caso contrario, il client JavaScript riceverà una stringa che contiene XML anziché un oggetto XML DOM.  
  
     Di seguito viene riportato l'esempio di un'operazione che restituisce dati XML con il tipo di contenuto impostato in modo appropriato:  
  
    ```  
    [OperationContract, WebGet(ResponseFormat=WebMessageFormat.Xml)]  
    public XElement GetData()  
    {  
    XElement x;  
    //Get some data here...  
  
    WebOperationContext.Current.OutgoingResponse.ContentType = "text/xml";      
    return x;  
    }  
  
    ```  
  
-   Se è richiesta la compatibilità con ASP.NET AJAX, non è possibile modificare nessun'altra proprietà negli attributi <xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute>.Gli altri aspetti del modello di programmazione Web possono essere utilizzati a condizione che non vengano violate le convenzioni di chiamata ASP.NET AJAX.  
  
 Scenari più avanzati richiedono la comprensione di alcuni dettagli aggiuntivi di supporto AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   Per capire come vengono trasferiti i dati tra un client della pagina AJAX e un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando JavaScript e per ulteriori informazioni sul mapping di tipi .NET Framework a tipi JavaScript, vedere [Supporto per JSON e altri formati di trasferimento dati](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md).  
  
-   Per sfruttare le funzionalità di ASP.NET, ad esempio, l'autenticazione basata su URL e l'accesso alle informazioni della sessione ASP.NET, è consigliabile abilitare la modalità di compatibilità ASP.NET tramite la configurazione.  
  
 Gli endpoint AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono essere utilizzati anche senza il framework ASP.NET AJAX.Ciò richiede una comprensione dell'architettura di supporto di AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per una discussione su questa architettura, vedere [Modello a oggetti per la programmazione HTTP Web di WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md).Per un esempio di codice che dimostra tale approccio, vedere [Servizio AJAX con esempi JSON e XML](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md).  
  
## Vedere anche  
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [Procedura: aggiungere un endpoint ASP.NET AJAX senza utilizzare la configurazione](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)   
 [Procedura: aggiungere un endpoint ASP.NET AJAX con l'utilizzo della configurazione](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)   
 [Procedura: scegliere tra richieste HTTP POST e HTTP GET per gli endpoint ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/http-post-and-http-get-requests-for-aspnet-ajax-endpoints.md)