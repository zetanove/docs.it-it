---
title: "Esempio di serializzazione JSON con tipizzazione debole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b30e501-4ef5-474d-9fad-a9d559cf9c52
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Esempio di serializzazione JSON con tipizzazione debole
Quando si serializza un tipo definito dall'utente in un formato di trasmissione specificato o si deserializza un formato di trasmissione in un tipo definito dall'utente, il tipo definito dall'utente specificato deve essere disponibile sia nel servizio che nel client. Per eseguire questa operazione, in genere l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> viene applicato ai tipi definiti dall'utente e l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> viene applicato ai relativi membri. Questo meccanismo viene applicato anche quando si usano oggetti JSON \(JavaScript Object Notation\), come descritto nell'argomento [Procedura: serializzare e deserializzare dati JSON](../../../../docs/framework/wcf/feature-details/how-to-serialize-and-deserialize-json-data.md).  
  
 In alcuni scenari, un servizio o un client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] deve accedere a oggetti JSON generati da un servizio o un client non controllabili dallo sviluppatore. Poiché il numero di servizi Web che espone pubblicamente API JSON è in aumento, può diventare arduo per lo sviluppatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] costruire tipi definiti dall'utente locali nei quali deserializzare gli oggetti JSON arbitrari. In questo esempio viene illustrato un meccanismo che consente agli sviluppatori [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di utilizzare oggetti JSON arbitrari deserializzati, senza creare tipi definiti dall'utente. Questo meccanismo è noto come *serializzazione con tipizzazione debole* di oggetti JSON, perché il tipo nel quale viene deserializzato un oggetto JSON non è noto in fase di compilazione.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Ad esempio, l'API di un servizio Web pubblico restituisce l'oggetto JSON seguente che fornisce alcune informazioni su un utente del servizio.  
  
```  
{"personal": {"name": "Paul", "age": 23, "height": 1.7, "isSingle": true, "luckyNumbers": [5,17,21]}, "favoriteBands": ["Band ABC", "Band XYZ"]}  
```  
  
 Per deserializzare questo oggetto, un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve implementare i tipi definiti dall'utente seguenti.  
  
```  
[DataContract]  
 public class MemberProfile  
 {  
     [DataMember]  
     public PersonalInfo personal;  
  
     [DataMember]  
     public string[] favoriteBands;  
 }  
  
 [DataContract]  
 public class PersonalInfo  
 {  
     [DataMember]  
     public string name;  
  
     [DataMember]  
     public int age;  
  
     [DataMember]  
     public double height;  
  
     [DataMember]  
     public bool isSingle;  
  
     [DataMember]  
     public int[] luckyNumbers;  
 }  
  
```  
  
 Questa operazione può risultare ardua, specialmente se il client deve gestire più di un tipo di oggetto JSON.  
  
 Il tipo `JsonObject` fornito in questo esempio introduce una rappresentazione con tipizzazione debole dell'oggetto JSON deserializzato.`JsonObject` si basa sul mapping naturale tra oggetti JSON e dizionari [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] e sul mapping tra matrici JSON e matrici [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Nel codice seguente viene illustrato il tipo `JsonObject`.  
  
```  
// Instantiation of JsonObject json omitted  
  
string name = json["root"]["personal"]["name"];  
int age = json["root"]["personal"]["age"];  
double height = json["root"]["personal"]["height"];  
bool isSingle = json["root"]["personal"]["isSingle"];  
int[] luckyNumbers = {  
                                     json["root"]["personal"]["luckyNumbers"][0],  
                                     json["root"]["personal"]["luckyNumbers"][1],  
                                     json["root"]["personal"]["luckyNumbers"][2]   
                                 };  
string[] favoriteBands = {  
                                        json["root"]["favoriteBands"][0],  
                                        json["root"]["favoriteBands"][1]  
                                    };  
```  
  
 Si noti che è possibile "esplorare" oggetti JSON e matrici senza doverne dichiarare il tipo in fase di compilazione. Per una spiegazione dei requisiti per l'oggetto `["root"]` di primo livello, vedere l'argomento [Mapping tra JSON e XML](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md).  
  
> [!NOTE]
>  La classe `JsonObject` viene fornita a solo scopo esemplificativo. Non è stata testata completamente e non deve essere utilizzata negli ambienti di produzione. Un'implicazione ovvia della serializzazione JSON con tipizzazione debole è la mancanza di indipendenza dai tipi quando si utilizza `JsonObject`.  
  
 Per utilizzare il tipo `JsonObject`, il contratto dell'operazione client deve utilizzare <xref:System.ServiceModel.Channels.Message> come tipo restituito.  
  
```  
[ServiceContract]  
    interface IClientSideProfileService  
    {  
        // There is no need to write a DataContract for the complex type returned by the service.  
        // The client will use a JsonObject to browse the JSON in the received message.  
  
        [OperationContract]  
        [WebGet(ResponseFormat = WebMessageFormat.Json)]  
        Message GetMemberProfile();  
    }  
  
```  
  
 Viene quindi creata un'istanza di `JsonObject` come illustrato nel codice seguente.  
  
```  
// Code to instantiate IClientSideProfileService channel omitted…  
  
// Make a request to the service and obtain the Json response  
XmlDictionaryReader reader = channel.GetMemberProfile().GetReaderAtBodyContents();  
  
// Go through the Json as though it is a dictionary. There is no need to map it to a .NET CLR type.  
JsonObject json = new JsonObject(reader);  
  
```  
  
 Il costruttore `JsonObject` accetta una classe <xref:System.Xml.XmlDictionaryReader>, ottenuta tramite il metodo <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents%2A>. Il lettore contiene una rappresentazione XML del messaggio JSON ricevuto dal client.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Mapping tra JSON e XML](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md).  
  
 Il programma produce l'output seguente:  
  
```  
Service listening at http://localhost:8000/.  
To view the JSON output from the sample, navigate to http://localhost:8000/GetMemberProfile  
This is Paul's page. I am 23 years old and I am 1.7 meters tall.  
I am single.  
My lucky numbers are 5, 17, and 21.  
My favorite bands are Band ABC and Band XYZ.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Compilare la soluzione WeaklyTypedJson.sln come descritto in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)]. Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Scenario\Ajax\WeaklyTypedJson`  
  
## Vedere anche