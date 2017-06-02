---
title: "Procedura: scegliere tra richieste HTTP POST e HTTP GET per gli endpoint ASP.NET AJAX | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b47de82a-4c92-4af6-bceb-a5cb8bb8ede9
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Procedura: scegliere tra richieste HTTP POST e HTTP GET per gli endpoint ASP.NET AJAX
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente di creare un servizio che espone un endpoint ASP.NET compatibile con AJAX che può essere chiamato da JavaScript su un sito Web client.  La procedura di base per generare tali servizi viene illustrata in [Procedura: aggiungere un endpoint ASP.NET AJAX con l'utilizzo della configurazione](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md) e [Procedura: aggiungere un endpoint ASP.NET AJAX senza utilizzare la configurazione](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).  
  
 ASP.NET AJAX supporta operazioni che usano verbi HTTP POST e HTTP GET, con HTTP POST come impostazione predefinita.  Quando si crea un'operazione che non ha effetti collaterali e restituisce dati che non vengono mai modificati o vengono modificati solo di rado, usare HTTP GET.  I risultati delle operazioni GET possono essere memorizzati nella cache, il che significa che più chiamate alla stessa operazione possono produrre una sola richiesta al servizio.  La memorizzazione nella cache non viene eseguita da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ma può verificarsi a qualsiasi livello, ad esempio nel browser di un utente o in un server proxy. La memorizzazione nella cache è vantaggiosa se si desidera migliorare le prestazioni del servizio, ma potrebbe non essere accettabile se i dati vengono modificati di frequente o se l'operazione esegue azioni.  
  
 Ad esempio, se si sta progettando un servizio per gestire il catalogo musicale di un utente, un'operazione che ricerca l'artista in base al titolo di un album trae vantaggio dall'utilizzo di GET, ma un'operazione che aggiunge un album alla raccolta personale dell'utente deve usare POST.  
  
 Per controllare la durata della cache, usare il tipo <xref:System.ServiceModel.Web.OutgoingWebResponseContext>.  Ad esempio, quando si progetta un servizio che restituisce previsioni meteorologiche aggiornate ogni ora, si utilizzerà GET limitando però la durata della cache a massimo un'ora, per impedire agli utenti del servizio di accedere a dati non aggiornati.  
  
 Quando si usano servizi da una pagina ASP.NET AJAX che usano il controllo Script Manager, non c'è alcuna differenza se l'operazione usa GET o POST, il meccanismo di gestione degli script assicura che venga emesso il tipo di richiesta corretto.  
  
 Le operazioni HTTP GET usano qualsiasi parametro di input supportato dalle operazioni POST, inclusi i tipi di contratto dati complessi.  Tuttavia, nella maggior parte dei casi è consigliabile evitare di usare troppi parametri o parametri troppo complessi nelle operazioni GET, per non ridurre l'efficienza della memorizzazione nella cache.  
  
 In questo argomento viene illustrato come scegliere tra GET e POST aggiungendo gli attributi <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> alle operazioni pertinenti nel contratto di servizio.  Gli altri passaggi \(per implementare, configurare e ospitare il servizio\), necessari per rendere operativo il servizio sono simili a quelli usati da qualsiasi servizio ASP.NET AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Un'operazione contrassegnata da <xref:System.ServiceModel.Web.WebGetAttribute> usa sempre una richiesta GET.  Un'operazione contrassegnata da <xref:System.ServiceModel.Web.WebInvokeAttribute> o non contrassegnata da nessuno dei due attributi, usa una richiesta POST.  <xref:System.ServiceModel.Web.WebInvokeAttribute> consente di usare altri verbi HTTP, diversi da GET e POST, quali PUT e DELETE, tramite la proprietà <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>.  Tuttavia, questi verbi non sono supportati da ASP.NET AJAX.  Se si intende usare il servizio da pagine ASP.NET che usano il controllo Script Manager, non usare la proprietà <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>.  
  
 Per un esempio pratico di passaggio a GET, vedere [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md).  
  
 Per un esempio in cui viene usato POST, vedere [Servizio AJAX con il protocollo HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md).  
  
### Per creare un servizio WCF che risponde a richieste HTTP GET o HTTP POST  
  
1.  Definire un contratto di servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base con un'interfaccia contrassegnata con l'attributo <xref:System.ServiceModel.ServiceContractAttribute>.  Contrassegnare ogni operazione con <xref:System.ServiceModel.OperationContractAttribute>.  Aggiungere l'attributo <xref:System.ServiceModel.Web.WebGetAttribute> per stabilire che un'operazione deve rispondere a richieste HTTP GET.  È inoltre possibile aggiungere l'attributo <xref:System.ServiceModel.Web.WebInvokeAttribute> per specificare esplicitamente HTTP POST o non specificare alcun attributo e scegliere quindi HTTP POST per impostazione predefinita.  
  
    ```  
    [ServiceContract]  
    public interface IMusicService  
    {  
        //This operation uses a GET method.  
        [OperationContract]  
        [WebGet]  
        string LookUpArtist(string album);  
  
        //This operation will use a POST method.  
        [OperationContract]  
        [WebInvoke]  
        void AddAlbum(string user, string album);  
  
        //This operation will use POST method by default  
        //since nothing else is explicitly specified.  
        [OperationContract]  
        string[] GetAlbums(string user);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2.  Implementare il contratto di servizio `IMusicService` con `MusicService`.  
  
    ```  
    public class MusicService : IMusicService  
    {  
        public void AddAlbum(string user, string album)  
        {  
            //Add implementation here.  
        }  
  
         //Other operations omitted…  
    }  
    ```  
  
3.  Creare un nuovo file denominato "file del servizio" con estensione svc nell'applicazione.  Modificare questo file aggiungendo le informazioni della direttiva [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) appropriate per il servizio.  Specificare che è necessario usare <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> nella direttiva [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) per configurare automaticamente un endpoint ASP.NET AJAX.  
  
    ```  
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.MusicService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
### Per chiamare il servizio  
  
1.  È possibile testare le operazioni GET del servizio senza alcun codice client, usando il browser.  Ad esempio, se il servizio è configurato all'indirizzo "http:\/\/example.com\/service.svc", digitando "http:\/\/example.com\/service.svc\/LookUpArtist?album\=SomeAlbum" nella barra degli indirizzi del browser si richiama il servizio e si provoca il download o la visualizzazione della risposta.  
  
2.  È possibile usare servizi con operazioni GET esattamente come qualsiasi altro servizio ASP.NET AJAX, immettendo l'URL del servizio nella raccolta degli script del controllo Script Manager ASP.NET AJAX.  Per un esempio, vedere [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md).  
  
## Vedere anche  
 [Creazione di servizi WCF per ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [Procedura: eseguire la migrazione di servizi Web ASP.NET compatibili AJAX a WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)