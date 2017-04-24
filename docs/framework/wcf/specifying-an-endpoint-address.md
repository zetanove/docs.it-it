---
title: "Specifica di un indirizzo endpoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
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
  - "indirizzi endpoint [WCF]"
ms.assetid: ac24f5ad-9558-4298-b168-c473c68e819b
caps.latest.revision: 41
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 41
---
# Specifica di un indirizzo endpoint
Tutta la comunicazione con un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] si verifica tramite i relativi endpoint. Ogni <xref:System.ServiceModel.Description.ServiceEndpoint> contiene un <xref:System.ServiceModel.Description.ServiceEndpoint.Address%2A>, <xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A>e un <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A>. Il contratto specifica quali operazioni sono disponibili. L'associazione specifica come comunicare con il servizio e l'indirizzo specifica dove trovare il servizio. Ogni endpoint deve avere un indirizzo univoco. L'indirizzo dell'endpoint è rappresentato dal <xref:System.ServiceModel.EndpointAddress> classe, che contiene un URI Uniform Resource Identifier () che rappresenta l'indirizzo del servizio, un <xref:System.ServiceModel.EndpointAddress.Identity%2A>, che rappresenta l'identità di sicurezza del servizio e una raccolta di facoltativo <xref:System.ServiceModel.EndpointAddress.Headers%2A>. Le intestazioni facoltative forniscono informazioni di indirizzamento più dettagliate che consentono di identificare o interagire con l'endpoint. Ad esempio, le intestazioni possono indicare come elaborare un messaggio in ingresso, dove l'endpoint deve inviare un messaggio di risposta o quale istanza di un servizio usare per elaborare un messaggio in ingresso di un particolare utente, quando sono disponibili più istanze.  
  
## <a name="definition-of-an-endpoint-address"></a>Definizione di un indirizzo endpoint  
 In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], un <xref:System.ServiceModel.EndpointAddress> Modella un riferimento dell'endpoint (EPR), come definito nello standard WS-Addressing.  
  
 L'indirizzo URI per la maggior parte dei trasporti è costituito da quattro parti. Ad esempio, l'URI "http://www.fabrikam.com:322/mathservice.svc/secureEndpoint" è costituito dalle quattro parti seguenti:  
  
-   Schema: http:  
  
-   Computer: www.fabrikam.com  
  
-   (Facoltativo) Porta: 322  
  
-   Percorso: /mathservice.svc/secureEndpoint  
  
 Il modello di riferimento endpoint prevede che ogni riferimento possa includere alcuni parametri per riferimento che aggiungono ulteriori informazioni di identificazione. In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], questi parametri di riferimento vengono modellati come istanze di <xref:System.ServiceModel.Channels.AddressHeader> (classe).  
  
 L'indirizzo endpoint per un servizio può essere specificato in modo imperativo mediante l'utilizzo di codice oppure in modo dichiarativo mediante la configurazione. In genere definire endpoint nel codice non è pratico in quanto le associazioni e gli indirizzi di un servizio distribuito sono solitamente diversi da quelli usati durante lo sviluppo del servizio. In genere è più pratico definire endpoint di servizio mediante la configurazione piuttosto che mediante codice. Se le informazioni sull'associazione e sull'indirizzo non vengono incluse nel codice, tali dati possono essere modificati senza dover compilare e distribuire nuovamente l'applicazione. Se non è specificato alcun endpoint nel codice o nella configurazione, il runtime ne aggiunge uno predefinito ad ogni indirizzo di base per ciascun contratto di servizio implementato dal servizio.  
  
 Esistono due modo per specificare gli indirizzi degli endpoint per un servizio in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. È possibile specificare un indirizzo assoluto per ogni endpoint associato al servizio oppure è possibile fornire un indirizzo di base per il <xref:System.ServiceModel.ServiceHost> di un servizio e quindi specificare un indirizzo per ogni endpoint associato al servizio che viene definito come relativo all'indirizzo di base. È possibile utilizzare entrambe le procedure per specificare gli indirizzi degli endpoint per un servizio nella configurazione o nel codice. Se non si specifica un indirizzo relativo, il servizio utilizza l'indirizzo di base. È inoltre possibile avere più indirizzi di base per un servizio, ma per ogni servizio è consentito un solo indirizzo di base per ogni trasporto. Se sono presenti più endpoint, ognuno dei quali è configurato con un'associazione diversa, i relativi indirizzi devono essere univoci. Gli endpoint che utilizzano la stessa associazione ma contratti diversi possono utilizzare lo stesso indirizzo.  
  
 Durante l'hosting con IIS, non si gestisce il <xref:System.ServiceModel.ServiceHost> istanza. Nel caso di un servizio ospitato in IIS, l'indirizzo di base è sempre l'indirizzo specificato nel file con estensione svc. Per gli endpoint del servizio ospitato in IIS è quindi necessario utilizzare sempre indirizzi relativi. Fornire un indirizzo endpoint completo può provocare errori nella fase di distribuzione del servizio. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Distribuzione di un servizio WCF ospitato in servizi di Internet Information](../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md).  
  
## <a name="defining-endpoint-addresses-in-configuration"></a>Definizione degli indirizzi endpoint nella configurazione  
 Per definire un endpoint in un file di configurazione, utilizzare il [ <> \> ](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) elemento.  
  
 <!-- TODO: review snippet reference [!code[S_UEHelloWorld#5](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp2.config#5)]  -->  
  
 Quando il <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> viene chiamato (ovvero, quando l'applicazione host tenta di avviare il servizio), il sistema ricerca un [ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/service.md) elemento con un attributo name che specifica "UE. Samples.HelloService". Se il [ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/service.md) elemento viene trovato, il sistema carica la classe specificata e crea gli endpoint utilizzando le definizioni di endpoint specificate nel file di configurazione. Questo meccanismo consente di caricare e avviare un servizio con due righe di codice, mentre tiene le informazioni sull'associazione e l'indirizzamento fuori dal codice. Il vantaggio di tale approccio è che queste modifiche possono essere apportate senza dover ricompilare o ridistribuire l'applicazione.  
  
 Le intestazioni facoltative vengono dichiarate in un [ <> \</> \> ](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md). Di seguito è riportato un esempio degli elementi utilizzati per specificare gli endpoint di un servizio in un file di configurazione in cui vengono distinte due intestazioni: client "Gold" all'indirizzo http://tempuri1.org/ e client "Standard" all'indirizzo http://tempuri2.org/. Il client che chiama questo servizio deve disporre delle appropriate [ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md) nel file di configurazione.  
  
 <!-- TODO: review snippet reference [!code[S_UEHelloWorld#1](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp.config#1)]  -->  
  
 Le intestazioni possono essere impostate anche su singoli messaggi anziché su tutti i messaggi su un endpoint (come illustrato in precedenza). Questa operazione viene eseguita utilizzando <xref:System.ServiceModel.OperationContextScope> per creare un nuovo contesto in un'applicazione client per aggiungere un'intestazione personalizzata al messaggio in uscita, come illustrato nell'esempio seguente.  
  
 [!code-csharp[OperationContextScope#4](../../../samples/snippets/csharp/VS_Snippets_CFX/operationcontextscope/cs/client.cs#4)]
 [!code-vb[OperationContextScope#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationcontextscope/vb/client.vb#4)]  
  
## <a name="endpoint-address-in-metadata"></a>Indirizzo endpoint nei metadati  
 Un indirizzo endpoint viene rappresentato in WSDL (Web Services Description Language) come elemento `EndpointReference` (EPR) WS-Addressing all'interno dell'elemento `wsdl:port` dell'endpoint corrispondente. L'EPR contiene l'indirizzo dell'endpoint e qualsiasi proprietà dell'indirizzo. Si noti che l'EPR in `wsdl:port` sostituisce `soap:Address`, come illustrato nell'esempio seguente.  
  
  
  
## <a name="defining-endpoint-addresses-in-code"></a>Definizione degli indirizzi endpoint nel codice  
 Indirizzo dell'endpoint può essere creato nel codice con il <xref:System.ServiceModel.EndpointAddress> (classe). L'URI specificato per l'indirizzo endpoint può essere un percorso completo o un percorso relativo all'indirizzo di base del servizio. Il codice seguente viene illustrato come creare un'istanza di <xref:System.ServiceModel.EndpointAddress> classe e aggiungerla al <xref:System.ServiceModel.ServiceHost> istanza che ospita il servizio.  
  
 Nell'esempio seguente viene illustrato come specificare l'indirizzo endpoint completo nel codice.  
  
 [!code-csharp[S_UEHelloWorld#2](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#2)]  
  
 Nell'esempio seguente viene illustrato come aggiungere un indirizzo relativo ("MyService") all'indirizzo di base dell'host del servizio.  
  
 [!code-csharp[S_UEHelloWorld#3](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#3)]  
  
> [!NOTE]
>  Proprietà del <xref:System.ServiceModel.Description.ServiceDescription> nel servizio di applicazione non deve essere modificate successivamente il <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> metodo <xref:System.ServiceModel.ServiceHostBase>. Alcuni membri, ad esempio il <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> proprietà e `AddServiceEndpoint` metodi su <xref:System.ServiceModel.ServiceHostBase> e <xref:System.ServiceModel.ServiceHost>, generano un'eccezione se vengono modificati dopo questo punto. Altri consentono la modifica, ma il risultato è indefinito.  
>   
>  Analogamente, sul client di <xref:System.ServiceModel.Description.ServiceEndpoint> valori non devono essere modificati dopo la chiamata a <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> sul <xref:System.ServiceModel.ChannelFactory>. Il <xref:System.ServiceModel.ChannelFactory.Credentials%2A> proprietà genera un'eccezione se viene modificata dopo tale punto. Gli altri valori della descrizione client possono essere modificati senza errore, ma il risultato è indefinito.  
>   
>  Se per il servizio o client, è consigliabile modificare la descrizione prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>.  
  
## <a name="using-default-endpoints"></a>Uso di endpoint predefiniti  
 Se non è specificato alcun endpoint nel codice o nella configurazione, il runtime ne fornisce di predefiniti aggiungendone uno ad ogni indirizzo di base per ciascun contratto di servizio implementato dal servizio. L'indirizzo di base può essere specificato nel codice o nella configurazione e gli endpoint predefiniti vengono aggiunti quando <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> viene chiamato sul <xref:System.ServiceModel.ServiceHost>.  
  
 Se gli endpoint sono forniti in modo esplicito, gli endpoint predefiniti possono ancora essere aggiunti chiamando <xref:System.ServiceModel.ServiceHostBase.AddDefaultEndpoints%2A> sul <xref:System.ServiceModel.ServiceHost> prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>. [!INCLUDE[crabout](../../../includes/crabout-md.md)]gli endpoint predefiniti, associazioni e comportamenti, vedere [configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md) e [configurazione semplificata per i servizi WCF](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.EndpointAddress>   
 [L'autenticazione e identità del servizio](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Hosting](../../../docs/framework/wcf/feature-details/hosting.md)