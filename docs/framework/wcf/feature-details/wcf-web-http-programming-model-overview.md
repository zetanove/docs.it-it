---
title: "Panoramica sul modello di programmazione HTTP Web WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
caps.latest.revision: 45
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 45
---
# Panoramica sul modello di programmazione HTTP Web WCF
Il modello di programmazione HTTP Web di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce gli elementi di base necessari per compilare servizi HTTP Web in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].I servizi HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono progettati per consentire l'accesso alla tipologia più ampia di possibili client \(inclusi i browser Web senza alcun framework client aggiuntivo\) e sono caratterizzati dai requisiti univoci seguenti:  
  
-   **URI ed elaborazione di URI** Gli svolgono un ruolo centrale nella progettazione dei servizi HTTP Web.Nel modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono utilizzate le classi <xref:System.UriTemplate> e <xref:System.UriTemplateTable> per fornire le funzionalità di elaborazione URI.  
  
-   **Supporto per operazioni GET e POST** I servizi HTTP Web si avvalgono del verbo GET per recuperare i dati, oltre a numerosi verbi di chiamata per modificare i dati e per chiamate remote.Nel modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono utilizzati gli oggetti <xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute> per associare le operazioni del servizio sia al verbo GET che ad altri verbi HTTP, ad esempio PUT, POST e DELETE.  
  
-   **Più formati di dati** Oltre ai messaggi SOPA, i servizi Web consentono di elaborare numerosi tipi di dati.Nel modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono utilizzati gli oggetti <xref:System.ServiceModel.WebHttpBinding> e <xref:System.ServiceModel.Description.WebHttpBehavior> per supportare numerosi formati di dati diversi, ad esempio documenti XML, oggetti dati JSON e flussi di contenuto binario quale immagini, file video o testo normale.  
  
 Il modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] estende la portata di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per supportare scenari di tipo Web, ad esempio servizi HTTP Web, servizi AJAX e JSON e feed ATOM\/RSS.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] servizi AJAX e JSON, vedere [Integrazione AJAX e supporto JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] diffusione, vedere [Panoramica sulla diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md).  
  
 Non sono previste restrizioni aggiuntive sui tipi di dati che possono essere restituiti da un servizio HTTP Web.Qualsiasi tipo serializzabile può essere restituito da un'operazione del servizio HTTP Web.Poiché le operazioni del servizio HTTP Web possono essere richiamate da un Web browser, esiste una limitazione per i tipi di dati che possono essere specificati in un URL.Per ulteriori informazioni sui tipi supportati per impostazione predefinita, vedere la sezione relativa a **URL e parametri della stringa di query di UriTemplate** riportata di seguito.È possibile modificare il comportamento predefinito fornendo l'implementazione T:System.ServiceModel.Dispatcher.QueryStringConverter che specifica come convertire i parametri specificati in un URL nel tipo di parametro effettivo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
> [!CAUTION]
>  I servizi creati nel modello di programmazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non utilizzano messaggi SOAP.Per questo motivo le funzionalità di sicurezza disponibili in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non possono essere utilizzate.È tuttavia possibile implementare la sicurezza basata sul trasporto ospitando il servizio mediante HTTPS.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)  
  
> [!WARNING]
>  L'installazione dell'estensione WebDAV per IIS può causare la restituzione di un errore HTTP 405 da parte dei servizi HTTP Web quando tramite l'estensione WebDAV viene effettuato il tentativo di gestire tutte le richieste PUT.Per risolvere questo problema è possibile disinstallare l'estensione WebDAV o disabilitarla per il sito Web.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][IIS e WebDav](http://learn.iis.net/page.aspx/357/webdav-for-iis-70/)  
  
## Elaborazione di URI con UriTemplate e UriTemplateTable  
 I modelli URI forniscono una sintassi efficiente per esprimere grandi set di URI strutturalmente simili.Nel modello seguente, ad esempio, viene espresso il set di tutti gli URI di tre segmenti che iniziano con "a" e terminano con "c", a prescindere dal valore del segmento intermedio: a\/{segment}\/c  
  
 In questo modello vengono descritti URI come il seguente:  
  
-   a\/x\/c  
  
-   a\/y\/c  
  
-   a\/z\/c  
  
-   e così via.  
  
 In questo modello, la notazione tra parentesi graffe \("{segment}"\) indica un segmento variabile anziché un valore letterale.  
  
 In .NET Framework è disponibile un'API da utilizzare con i modelli URI denominata <xref:System.UriTemplate>.Gli oggetti `UriTemplates` consentono di effettuare le seguenti operazioni:  
  
-   È possibile chiamare uno dei metodi `Bind` con un set di parametri per produrre un *URI completamente chiuso* che corrisponde al modello.Ciò significa che tutte le variabili all'interno del modello URI vengono sostituite con i valori effettivi.  
  
-   È possibile chiamare `Match`\(\) con un URI candidato che utilizza un modello per suddividere un URI candidato nelle sue parti costitutive e restituisce un dizionario che contiene le varie parti dell'URI etichettate in base alle variabili nel modello.  
  
-   `Bind`\(\) e `Match`\(\) sono inverse, pertanto è possibile chiamare `Match`\( `Bind`\( x \) \) e ottenere lo stesso ambiente dal quale si è partiti.  
  
 Capita spesso \(specialmente nel server in cui è necessario inviare una richiesta a un'operazione del servizio basata sull'URI\) che si desideri tenere traccia di un set di oggetti <xref:System.UriTemplate> in una struttura dati che può fare riferimento in modo indipendente a ogni modello contenuto.L'oggetto <xref:System.UriTemplateTable> rappresenta un set di modelli URI e seleziona la migliore corrispondenza in base a un set di modelli e a un URI candidato.Ciò non è affiliato ad alcuno stack di rete particolare \([!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] incluso\), pertanto è possibile utilizzarlo ovunque sia necessario.  
  
 Nel modello di servizi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono utilizzati gli oggetti <xref:System.UriTemplate> e <xref:System.UriTemplateTable> per associare operazioni del servizio a un set di URI descritti da un oggetto <xref:System.UriTemplate>.Un'operazione del servizio viene associata a un <xref:System.UriTemplate>, utilizzando <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute>.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]<xref:System.UriTemplate> e <xref:System.UriTemplateTable>, vedere [UriTemplate e UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)  
  
## Attributi WebGet e WebInvoke  
 I servizi HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si avvalgono di verbi di recupero \(ad esempio HTTP GET\) oltre a numerosi verbi di chiamata \(ad esempio HTTP POST, PUT e DELETE\).Il modello  di programmazione HTTP WEb di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente agli sviluppatori del servizio di controllare sia il modello URI che il verbo associato alle relative operazioni del servizio con gli oggetti <xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute>.<xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute> consentono di controllare l'associazione di singole operazioni con gli URI e i metodi HTTP associati a detti URI.L'aggiunta di <xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute>, ad esempio, nel codice seguente.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,   
                               string newName );  
}  
```  
  
 Il codice precedente consente di effettuare le richieste HTTP seguenti.  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 L'impostazione predefinita di <xref:System.ServiceModel.Web.WebInvokeAttribute> è POST ma è possibile utilizzarlo anche per altri verbi.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It“ -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 Per visualizzare un esempio completo di un servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che utilizza il modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: creare un servizio HTTP Web WCF](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)  
  
## Nome del parametro della stringa di query UriTemplate e URL.  
 I servizi Web possono essere chiamati da un browser Web digitando un URL associato a un'operazione del servizio.Queste operazioni del servizio possono accettare parametri della stringa di query che devono essere specificati in un formato stringa all'interno dell'URL.Nella tabella seguente vengono illustrati i tipi che è possibile passare all'interno di un URL e il formato utilizzato.  
  
|Tipo|Formato|  
|----------|-------------|  
|<xref:System.Byte>|0 \- 255|  
|<xref:System.SByte>|\-128 \- 127|  
|<xref:System.Int16>|\-32768 \- 32767|  
|<xref:System.Int32>|\-2,147,483,648 \- 2,147,483,647|  
|<xref:System.Int64>|\-9,223,372,036,854,775,808 \- 9,223,372,036,854,775,807|  
|<xref:System.UInt16>|0 \- 65535|  
|<xref:System.UInt32>|0 \- 4,294,967,295|  
|<xref:System.UInt64>|0 \- 18,446,744,073,709,551,615|  
|<xref:System.Single>|\-3,402823e38 \- 3,402823e38 \(la notazione esponenziale non è obbligatoria\)|  
|<xref:System.Double>|\-1,79769313486232e308 \- 1,79769313486232e308 \(la notazione esponenziale non è obbligatoria\)|  
|<xref:System.Char>|Qualsiasi carattere singolo|  
|<xref:System.Decimal>|Qualsiasi numero decimale in notazione standard \(nessun esponente\)|  
|<xref:System.Boolean>|True o False \(senza distinzione maiuscole\/minuscole\)|  
|<xref:System.String>|Qualsiasi stringa \(la stringa null non è supportata e non viene effettuata alcuna operazione di escape\)|  
|<xref:System.DateTime>|MM\/GG\/AAAA<br /><br /> MM\/GG\/AAAA HH:MM:SS \[AM&#124;PM\]<br /><br /> Mese Giorno Anno<br /><br /> Mese Giorno Anno HH:MM:SS \[AM&#124;PM\]|  
|<xref:System.TimeSpan>|GG.HH:MM:SS<br /><br /> Dove GG \= Giorni, HH \= Ore, MM \= Minuti, SS \= Secondi|  
|<xref:System.Guid>|Un GUID, ad esempio:<br /><br /> 936DA01F\-9ABD\-4d9d\-80C7\-02AF85C822A8|  
|<xref:System.DateTimeOffset>|MM\/GG\/AAAA HH:MM:SS MM:SS<br /><br /> Dove GG \= Giorni, HH \= Ore, MM \= Minuti, SS \= Secondi|  
|Enumerazioni|Valore di enumerazione che definisce l'enumerazione come illustrato nel codice seguente.<br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> Nella stringa di query è possibile specificare uno qualsiasi dei singoli valori di enumerazione \(o i valori integer corrispondenti\).|  
|Tipi con `TypeConverterAttribute` in grado di convertire il tipo in e da una rappresentazione di stringa.|Dipende dal convertitore del tipo.|  
  
## Formati e modello di programmazione HTTP Web WCF  
 Nel modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono disponibili nuove funzionalità che consentono di utilizzare numerosi formati di dati diversi.A livello di associazione, <xref:System.ServiceModel.WebHttpBinding> è in grado di leggere e scrivere i diversi tipi di dati seguenti:  
  
-   XML  
  
-   JSON  
  
-   Flussi binari opachi  
  
 Questo significa che il modello di programmazione HTTP WEb di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è in grado di gestire qualsiasi tipo di dati WEB HTTP, ma la programmazione potrebbe essere eseguita rispetto a <xref:System.IO.Stream>.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] fornisce supporto sia per i dati JSON \(AJAX\) sia per i feed di diffusione \(inclusi ATOM e RSS\).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] queste funzionalità, vedere [Formattazione di HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)[Panoramica sulla diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md) e [Integrazione AJAX e supporto JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md).  
  
## Modello di programmazione HTTP Web WCF e sicurezza  
 Poiché il modello di programmazione HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta i protocolli WS\-\*, l'unico modo per proteggere un servizio HTTP Web di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consiste nell'esporre il servizio su HTTPS tramite SSL.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] configurazione di SSL con [!INCLUDE[iisver](../../../../includes/iisver-md.md)], vedere la pagina relativa all'[implementazione di SSL in IIS](http://go.microsoft.com/fwlink/?LinkId=131613)  
  
## Risoluzione dei problemi nel modello di programmazione HTTP WEb WCF  
 Quando si chiamano i servizi HTTP Web WCF utilizzando un oggetto <xref:System.ServiceModel.Channels.ChannelFactory%601> per creare un canale, l'oggetto <xref:System.ServiceModel.Description.WebHttpBehavior> utilizza l'oggetto <xref:System.ServiceModel.EndpointAddress> impostato nel file di configurazione anche se un oggetto <xref:System.ServiceModel.EndpointAddress> viene passato all'oggetto <xref:System.ServiceModel.Channels.ChannelFactory%601>.  
  
## Vedere anche  
 [Diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)   
 [Modello a oggetti per la programmazione HTTP Web di WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)   
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)