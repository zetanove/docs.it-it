---
title: "Indirizzi endpoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "indirizzi [WCF]"
  - "WCF [WCF], indirizzi"
  - "Windows Communication Foundation [WCF], indirizzi"
ms.assetid: 13f269e3-ebb1-433c-86cf-54fbd866a627
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Indirizzi endpoint
A ogni endpoint è associato un indirizzo, che è utilizzato per individuarlo e identificarlo.L'indirizzo è costituito principalmente da un URI \(Uniform Resource Identifier\) che specifica il percorso dell'endpoint.L'indirizzo endpoint è rappresentato nel modello di programmazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] tramite la classe <xref:System.ServiceModel.EndpointAddress>. Questa contiene una proprietà <xref:System.ServiceModel.EndpointAddress.Identity%2A> facoltativa che consente l'autenticazione dell'endpoint tramite altri endpoint che scambiano messaggi con esso e un set di proprietà <xref:System.ServiceModel.EndpointAddress.Headers%2A> facoltative. Tali proprietà definiscono qualsiasi altra intestazione SOAP richiesta per raggiungere il servizio.Le intestazioni facoltative forniscono dettagli aggiuntivi e più precisi sull'indirizzo per identificare o interagire con l'endpoint del servizio.L'indirizzo di un endpoint è rappresentato in transito come riferimento all'endpoint di WS\-Addressing \(EPR\).  
  
## Struttura URI di un indirizzo  
 L'indirizzo URI per la maggior parte dei trasporti è costituito da quattro parti.Le quattro parti dell'URI http:\/\/www.fabrikam.com:322\/mathservice.svc\/secureEndpoint, ad esempio, possono essere specificate come segue:  
  
-   Schema: http:  
  
-   Computer: www.fabrikam.com  
  
-   \(facoltativo\) Porta: 322  
  
-   Percorso: \/mathservice.svc\/secureEndpoint  
  
## Definizione di un indirizzo per un servizio  
 L'indirizzo endpoint per un servizio può essere specificato in modo imperativo mediante l'utilizzo di codice oppure in modo dichiarativo mediante la configurazione.In genere definire endpoint nel codice non è pratico in quanto le associazioni e gli indirizzi di un servizio distribuito sono solitamente diversi da quelli utilizzati durante lo sviluppo del servizio.In genere è più pratico definire endpoint di servizio mediante la configurazione piuttosto che mediante codice.Se le informazioni sull'associazione e sull'indirizzo non vengono incluse nel codice, tali dati possono essere modificati senza dover compilare o distribuire nuovamente l'applicazione.  
  
### Definizione di un indirizzo nella configurazione  
 Per definire un endpoint in un file di configurazione, utilizzare l'elemento [\<endpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md).Per ulteriori informazioni e per un esempio, vedere [Specifica di un indirizzo endpoint](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
### Definizione di un indirizzo nel codice  
 È possibile creare un indirizzo endpoint nel codice con la classe <xref:System.ServiceModel.EndpointAddress>.Per ulteriori informazioni e per un esempio, vedere [Specifica di un indirizzo endpoint](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
### Endpoint in WSDL  
 Un indirizzo endpoint può essere rappresentato anche in WSDL come elemento EPR di WS\-Addressing all'interno dell'elemento `wsdl:port` dell'endpoint corrispondente.L'EPR contiene l'indirizzo dell'endpoint e qualsiasi proprietà dell'indirizzo.Per ulteriori informazioni e per un esempio, vedere [Specifica di un indirizzo endpoint](../../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
## Supporto per più binding IIS in .NET Framework 3.5  
 I provider di servizi Internet consentono spesso di ospitare diverse applicazioni nello stesso server e nello stesso sito per aumentare la densità del sito e ridurre il costo totale di proprietà.Queste applicazioni sono in genere associate a indirizzi di base diversi.Un sito Web IIS \(Internet Information Services\) può contenere più applicazioni.Alle applicazioni in un sito è possibile accedere tramite una o più associazioni IIS.  
  
 Le associazioni IIS forniscono due tipi di informazioni: un protocollo di associazione e informazioni di associazione.Il protocollo di associazione definisce lo schema sul quale ha luogo la comunicazione, mentre le informazioni di associazione sono utilizzate per accedere al sito.  
  
 Nell'esempio seguente vengono illustrati i componenti che possono essere presenti in un'associazione IIS:  
  
-   Protocollo di associazione: HTTP  
  
-   Informazioni di associazione: indirizzo IP, porta, intestazione host  
  
 IIS può specificare più associazioni per ogni sito, il che comporta più indirizzi di base per ogni schema.Prima di [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)], in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non erano supportati più indirizzi per uno schema e, nel caso venissero specificati, veniva generata un'eccezione <xref:System.ArgumentException> durante l'attivazione.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] consente ai provider di servizi Internet di ospitare più applicazioni con indirizzi di base diversi per lo stesso schema sullo stesso sito.  
  
 Un sito potrebbe contenere, ad esempio, gli indirizzi di base seguenti:  
  
-   http:\/\/payroll.myorg.com\/Service.svc  
  
-   http:\/\/shipping.myorg.com\/Service.svc  
  
 Con [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)], si specifica un filtro del prefisso a livello di AppDomain nel file di configurazione.A tale scopo, utilizzare l'elemento [\<FiltriPrefissoIndirizzoBase\>](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md) che contiene un elenco di prefissi.Gli indirizzi di base in ingresso, forniti da IIS, sono filtrati in base all'elenco di prefissi facoltativo.Per impostazione predefinita, quando non è specificato un prefisso, vengono passati tutti gli indirizzi.La specifica del prefisso fa sì che venga passato solo l'indirizzo di base corrispondente per quello schema.  
  
 Quello che segue è un esempio di codice di configurazione che utilizza i filtri del prefisso.  
  
```  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://payroll.myorg.com:8000"/>  
        <add prefix="http://shipping.myorg.com:8000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 Nell'esempio precedente, net.tcp:\/\/payroll.myorg.com:8000 e http:\/\/shipping.myorg.com:8000 sono gli unici indirizzi di base, per i rispettivi schemi, che vengono passati.  
  
 `baseAddressPrefixFilter` non supporta caratteri jolly.  
  
 Gli indirizzi di base forniti da IIS possono disporre di indirizzi associati ad altri schemi non presenti nell'elenco `baseAddressPrefixFilters`.Questi indirizzi non vengono filtrati.  
  
## Supporto per più binding IIS in .NET Framework 4 e versione successiva  
 A partire da .NET 4, è possibile abilitare il supporto di più binding in IIS senza dover scegliere un indirizzo di base unico, impostando la proprietà <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> dell'oggetto <xref:System.ServiceModel.ServiceHostingEnvironment> su true.Questo supporto è limitato agli schemi del protocollo HTTP.  
  
 Di seguito è riportato un esempio di codice di configurazione in cui viene utilizzata la proprietà multipleSiteBindingsEnabled in [\<serviceHostingEnvironment\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md).  
  
```  
  
<system.serviceModel>  
  <serviceHostingEnvironment multipleSiteBindingsEnabled=”true” >  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 Quando questa impostazione viene utilizzata per abilitare più binding di siti, tutte le impostazioni baseAddressPrefixFilters vengono ignorate, sia per i protocolli HTTP sia per quelli non HTTP.  
  
 Per dettagli ed esempi, vedere [Supporto delle associazioni a più siti IIS](../../../../docs/framework/wcf/feature-details/supporting-multiple-iis-site-bindings.md) e la proprietà <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A>.  
  
## Estensione dell'indirizzamento nei servizi WCF  
 Nel modello di indirizzamento predefinito dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene utilizzato l'indirizzo URI dell'endpoint per gli scopi seguenti:  
  
-   Per specificare l'indirizzo di ascolto del servizio, il percorso su cui l'endpoint resta in ascolto dei messaggi.  
  
-   Per specificare il filtro dell'indirizzo SOAP, l'indirizzo che un endpoint si aspetta come intestazione SOAP.  
  
 I valori per ognuno di questi scopi possono essere specificati separatamente, consentendo numerose estensioni di indirizzamento a copertura di scenari utili:  
  
-   Intermediari SOAP: un messaggio inviato da un client attraversa uno o più servizi aggiuntivi che elaborano il messaggio prima che raggiunga la sua destinazione finale.Gli intermediari SOAP possono eseguire numerose attività, ad esempio memorizzazione nella cache, routing, bilanciamento del carico o convalida dello schema sui messaggi.Per realizzare questo scenario, inviare messaggi a un indirizzo fisico separato \(`via`\) destinato all'intermediario piuttosto che a un indirizzo logico \(`wsa:To`\) per la destinazione finale.  
  
-   L'indirizzo di ascolto dell'endpoint è un URI privato ed è impostato su un valore diverso dalla sua proprietà `listenURI`.  
  
 L'indirizzo di trasporto specificato da `via` è il percorso al quale dovrebbe inizialmente essere inviato un messaggio mentre si sta dirigendo verso un altro indirizzo remoto specificato dal parametro `to` in cui si trova il servizio.Nella maggior parte degli scenari Internet, l'URI `via` corrisponde alla proprietà <xref:System.ServiceModel.EndpointAddress.Uri%2A> dell'indirizzo finale `to` del servizio.La distinzione tra i due indirizzi è necessaria solo quando è richiesto il routing manuale.  
  
### Intestazioni di indirizzamento  
 Un endpoint può essere indirizzato da una o più intestazioni SOAP oltre che dal proprio URI di base.Ciò è utile, ad esempio, in presenza di scenari di intermediari SOAP in cui per un endpoint viene richiesto che nei relativi client siano incluse intestazioni SOAP destinate agli intermediari.  
  
 È possibile definire intestazioni di indirizzo personalizzate in due modi: codice o configurazione:  
  
-   Nel codice, creare intestazioni di indirizzo personalizzate utilizzando la classe <xref:System.ServiceModel.Channels.AddressHeader>, quindi utilizzarle nella costruzione di un oggetto <xref:System.ServiceModel.EndpointAddress>.  
  
-   Nella configurazione, [\<intestazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)[\<endpoint\> personalizzate sono specificate come figli dell'elemento](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017).  
  
 La configurazione è in genere preferibile al codice, poiché consente di modificare le intestazioni dopo la distribuzione.  
  
### Indirizzi di ascolto personalizzati  
 È possibile impostare l'indirizzo di ascolto su un valore diverso dall'URI dell'endpoint.Ciò è utile negli scenari di intermediari in cui l'indirizzo SOAP da esporre è quello di un intermediario SOAP pubblico, mentre l'indirizzo su cui l'endpoint è effettivamente in ascolto è un indirizzo di rete privata.  
  
 È possibile specificare un indirizzo di ascolto personalizzato utilizzando codice o configurazione:  
  
-   Nel codice, specificare un indirizzo di ascolto personalizzato aggiungendo una classe <xref:System.ServiceModel.Description.ClientViaBehavior> alla raccolta di comportamenti dell'endpoint.  
  
-   Nella configurazione, specificare un indirizzo di ascolto personalizzato con l'attributo `ListenUri` dell'elemento [\<endpoint\>](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) del servizio.  
  
### Filtro dell'indirizzo SOAP personalizzato  
 <xref:System.ServiceModel.EndpointAddress.Uri%2A> viene utilizzato insieme a una proprietà <xref:System.ServiceModel.EndpointAddress.Headers%2A> per definire il filtro dell'indirizzo SOAP di un endpoint \(<xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>\).Per impostazione predefinita, questo filtro consente di verificare che un messaggio in arrivo disponga di un'intestazione del messaggio `To` che corrisponde all'URI dell'endpoint e che nel messaggio siano presenti tutte le intestazioni dell'endpoint richieste.  
  
 In alcuni scenari, un endpoint riceve tutti i messaggi che arrivano sul trasporto sottostante e non solo quelli con l'intestazione `To` appropriata.Affinché ciò sia possibile, l'utente può utilizzare la classe <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter>.  
  
## Vedere anche  
 [Specifica di un indirizzo endpoint](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)   
 [Identità del servizio e autenticazione](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)