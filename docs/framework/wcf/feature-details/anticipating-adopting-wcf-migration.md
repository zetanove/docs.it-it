---
title: "Preparazione all&#39;adozione di Windows Communication Foundation: facilitazione dell&#39;integrazione futura | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f49664d9-e9e0-425c-a259-93f0a569d01b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Preparazione all&#39;adozione di Windows Communication Foundation: facilitazione dell&#39;integrazione futura
Per garantire una più facile migrazione futura di nuove applicazioni ASP.NET a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], seguire i consigli forniti sopra nonché quelli forniti di seguito.  
  
## Protocolli  
 Disattivare il supporto di ASP.NET 2.0 per SOAP 1.2:  
  
```  
<configuration>  
     <system.web>  
      <webServices >  
          <protocols>  
           <remove name="HttpSoap12"/>  
          </protocols>    
      </webServices>  
     </system.web>   
</configuration>  
  
```  
  
 È consigliabile eseguire questa operazione in quanto in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] i messaggi conformi a protocolli diversi, ad esempio SOAP 1.1 e SOAP 1.2, devono essere passati usando endpoint diversi.  Se un servizio Web di ASP.NET 2.0 è configurato per il supporto di entrambi i protocolli SOAP 1.1 e SOAP 1.2 \(configurazione predefinita\), non è possibile eseguirne la migrazione in avanti a un singolo endpoint [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nell'indirizzo originale che sarebbe certamente compatibile con tutti i client esistenti del servizio Web ASP.NET.  La scelta di SOAP 1.2 anziché la versione 1.1 restringerà inoltre sensibilmente il numero di clienti del servizio.  
  
## Sviluppo del servizio  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di definire contratti di servizio applicando la classe <xref:System.ServiceModel.ServiceContractAttribute> a interfacce o classi.  È consigliabile applicare l'attributo a un'interfaccia piuttosto che a una classe perché in questo modo viene creata una definizione di contratto che può essere implementata in vari modi da un numero qualsiasi di classi.  ASP.NET supporta l'opzione relativa all'applicazione dell'attributo <xref:System.Web.Services.WebService> a interfacce e classi.  Tuttavia, come già menzionato, ASP.NET 2.0 presenta un difetto a causa del quale il parametro Namespace dell'attributo <xref:System.Web.Services.WebService> non produce alcun effetto quando l'attributo viene applicato a un'interfaccia anziché a una classe.  Poiché è generalmente consigliabile modificare lo spazio dei nomi di un servizio sostituendo il valore predefinito, http:\/\/tempuri.org, usando il parametro Namespace dell'attributo <xref:System.Web.Services.WebService>, è necessario continuare a definire servizi Web ASP.NET applicando l'attributo <xref:System.ServiceModel.ServiceContractAttribute> o a interfacce o a classi.  
  
-   Usare meno codice possibile nei metodi mediante i quali vengono definite queste interfacce.  Fare in modo che deleghino il lavoro ad altre classi.  Anche nuovi tipi di servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] potrebbero quindi delegare la maggior parte del lavoro a queste classi.  
  
-   Fornire nomi espliciti per le operazioni di un servizio usando il parametro `MessageName` di <xref:System.Web.Services.WebMethodAttribute>.  
  
    ```  
    [WebMethod(MessageName="ExplicitName")]  
    string Echo(string input);  
    ```  
  
     È importante eseguire questa operazione perché i nomi predefiniti assegnati alle operazioni in ASP.NET sono diversi dai nomi predefiniti forniti da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Fornendo nomi espliciti non è necessario basarsi su quelli predefiniti.  
  
-   Non implementare operazioni di servizi Web ASP.NET con metodi polimorfici in quanto [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta questo tipo di implementazione.  
  
-   Usare <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute> per fornire valori espliciti per le intestazioni HTTP SOAPAction mediante le quali le richieste HTTP verranno indirizzate ai metodi.  
  
    ```  
    [WebMethod]  
    [SoapDocumentMethod(RequestElementName="ExplicitAction")]  
    string Echo(string input);  
    ```  
  
     In questo modo i valori SOAPAction predefiniti usati da ASP.NET e quelli usati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non dovranno essere necessariamente gli stessi.  
  
-   Evitare l'uso di estensioni SOAP.  Se le estensioni SOAP sono obbligatorie, determinare se lo scopo per il quale vengono considerate è una funzionalità già fornita da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  In tal caso, riconsiderare la scelta di non adottare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Gestione dello stato  
 Evitare di dover gestire lo stato nei servizi.  Non solo la gestione dello stato tende a compromettere la scalabilità di un'applicazione, ma i meccanismi di gestione dello stato di ASP.NET e di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono molto diversi, sebbene [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporti i meccanismi ASP.NET nella modalità compatibilità ASP.NET.  
  
## Gestione delle eccezioni  
 Nella progettazione delle strutture dei tipi di dati da inviare e ricevere da un servizio, progettare anche strutture che rappresentino i vari tipi di eccezioni che potrebbero verificarsi all'interno di un servizio che si desidera trasmettere a un client.  
  
```  
[Serializable]  
[XmlRoot(  
     Namespace="ExplicitNamespace", IsNullable=true)]  
    public partial class AnticipatedException {  
  
     private string anticipatedExceptionInformationField;  
  
     public string AnticipatedExceptionInformation {  
      get {  
          return this.anticipatedExceptionInformationField;  
          }  
      set {  
          this.anticipatedExceptionInformationField = value;  
          }  
     }  
}  
```  
  
 Impostare queste classi in modo che siano in grado di serializzarsi in XML:  
  
```  
public XmlNode ToXML()  
{  
     XmlSerializer serializer = new XmlSerializer(  
      typeof(AnticipatedException));  
     MemoryStream memoryStream = new MemoryStream();  
     XmlTextWriter writer = new XmlTextWriter(  
     memoryStream, UnicodeEncoding.UTF8);  
     serializer.Serialize(writer, this);  
     XmlDocument document = new XmlDocument();  
     document.LoadXml(new string(  
     UnicodeEncoding.UTF8.GetChars(  
     memoryStream.GetBuffer())).Trim());  
    return document.DocumentElement;  
}  
```  
  
 Le classi potranno quindi essere usate per fornire i dettagli per le istanze <xref:System.Web.Services.Protocols.SoapException> generate in modo esplicito:  
  
```  
AnctipatedException exception = new AnticipatedException();  
exception.AnticipatedExceptionInformation = "…";  
throw new SoapException(  
     "Fault occurred",  
     SoapException.ClientFaultCode,  
     Context.Request.Url.AbsoluteUri,  
     exception.ToXML());  
  
```  
  
 Queste classi di eccezione potranno essere riutilizzate immediatamente con la classe <xref:System.ServiceModel.FaultException%601> di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per generare una nuova eccezione `FaultException<AnticipatedException>(anticipatedException);`.  
  
## Sicurezza  
 Di seguito sono riportati alcuni consigli sulla protezione.  
  
-   Evitare di usare profili di ASP.NET 2.0 poiché determinerebbe una limitazione dell'utilizzo della modalità di integrazione ASP.NET qualora venisse effettuata la migrazione del servizio a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Evitare di usare elenchi di controllo di accesso \(ACL\) per controllare l'accesso ai servizi. I servizi Web ASP.NET supportano infatti gli ACL usando Internet Information Services \(IIS\), mentre [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] no. I servizi Web ASP.NET dipendono da IIS per l'hosting, mentre WCF non deve essere necessariamente ospitato in IIS.  
  
-   Prendere in considerazione l'uso dei provider di ruoli di ASP.NET 2.0 per l'autorizzazione dell'accesso alle risorse di un servizio.  
  
## Vedere anche  
 [Preparazione all'adozione di Windows Communication Foundation: facilitare l'integrazione futura](../../../../docs/framework/wcf/feature-details/anticipating-adopting-the-wcf-easing-future-integration.md)