---
title: "Interoperabilit&#224; con i servizi Web ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 622422f8-6651-442f-b8be-e654a4aabcac
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Interoperabilit&#224; con i servizi Web ASP.NET
Per garantire l'interoperabilità tra i servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e i servizi Web [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è possibile implementare i servizi che utilizzano entrambe le tecnologie in modo che siano conformi alla specifica WS\-I Basic Profile 1.1.Per garantire l'interoperabilità fra i servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] conformi alla specifica WS\-I Basic Profile 1.1 e i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è possibile utilizzare un'associazione di sistema fornita da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ovvero <xref:System.ServiceModel.BasicHttpBinding>.  
  
 Utilizzare l'opzione di [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] che consente di aggiungere gli attributi <xref:System.Web.Services.WebService> e <xref:System.Web.Services.WebMethodAttribute> a un'interfaccia anziché a una classe e di scrivere una classe per implementare l'interfaccia, come mostrato nell'esempio di codice seguente.  
  
```  
[WebService]  
public interface IEcho  
{  
    [WebMethod]  
    string Echo(string input);  
}  
  
public class Service : IEcho  
{  
  
   public string Echo(string input)  
   {  
        return input;  
    }  
}  
```  
  
 È preferibile utilizzare questa opzione. Infatti, l'interfaccia avente l'attributo <xref:System.Web.Services.WebService> costituisce un contratto per le operazioni eseguite dal servizio che può essere riutilizzato con varie classi in grado di implementare tale contratto in modi diversi.  
  
 Evitare di utilizzare l'attributo <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> per instradare i messaggi a metodi basati sul nome completo dell'elemento del corpo del messaggio SOAP anziché sull'intestazione HTTP `SOAPAction`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'intestazione HTTP `SOAPAction` per instradare i messaggi.  
  
 Il codice XML in cui l'oggetto <xref:System.Xml.Serialization.XmlSerializer> serializza un tipo è per impostazione predefinita semanticamente identico al codice XML in cui l'oggetto <xref:System.Runtime.Serialization.DataContractSerializer> serializza un tipo, purché lo spazio dei nomi del codice XML sia stato definito in modo esplicito.Quando si definisce un tipo di dati da utilizzare in servizi Web di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e si prevede di utilizzare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], eseguire le operazioni seguenti:  
  
-   Definire il tipo utilizzando classi .NET Framework anziché l'XML Schema.  
  
-   Aggiungere solo gli attributi <xref:System.SerializableAttribute> e <xref:System.Xml.Serialization.XmlRootAttribute> alla classe, utilizzando quest'ultimo per definire in modo esplicito lo spazio dei nomi del tipo.Evitare di aggiungere attributi aggiuntivi dello spazio dei nomi <xref:System.Xml.Serialization> per controllare la modalità di conversione della classe .NET Framework in XML.  
  
-   Tramite questo approccio è possibile convertire successivamente le classi .NET in contratti di dati aggiungendo gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> senza modificare in modo significativo il codice XML nel quale le classi vengono serializzate per la trasmissione.I tipi utilizzati nei messaggi dai servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] possono essere elaborati come contratti di dati dalle applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Ciò offre diversi vantaggi, fra cui il miglioramento delle prestazioni delle applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Evitare di utilizzare le opzioni di autenticazione fornite in Internet Information Services \(IIS\),poiché i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non le supportano.Se occorre proteggere un servizio, utilizzare le opzioni fornite in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Queste opzioni sono infatti affidabili e sono basate su protocolli standard.  
  
## Impatto sulle prestazioni causato dal caricamento di ServiceModel HttpModule  
 In .NET Framework 3.0, WCF `HttpModule` è stato installato nel file Web.config di primo livello in modo tale che qualsiasi applicazione ASP.NET supporti WCF.Ciò può avere effetti negativi sulle prestazioni, pertanto è possibile eliminare `ServiceModel` per il file Web.config come illustrato nell'esempio seguente.  
  
```  
<httpModules>  
    <remove name=”ServiceModel” />  
<httpModules/>  
  
```  
  
## Vedere anche  
 [Procedura: configurare un servizio WCF che interagisca con client di servizi Web ASP.NET](../../../../docs/framework/wcf/feature-details/config-wcf-service-with-aspnet-web-service.md)