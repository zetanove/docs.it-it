---
title: "Utilizzo di un resolver del contratto dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e68a16c-36f0-4df4-b763-32021bff2b89
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Utilizzo di un resolver del contratto dati
Un resolver del contratto dati consente di configurare tipi noti in modo dinamico.I tipi noti sono necessari se si serializza o deserializza un tipo non previsto da un contratto dati.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] tipi noti, vedere [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).I tipi noti vengono in genere specificati in modo statico.Ciò significa che è necessario conoscere tutti i tipi possibili che un'operazione può ricevere durante l'implementazione dell'operazione.Poiché in alcuni scenari tale condizione non è possibile, è importante specificare i tipi noti in modo dinamico.  
  
## Creazione di un resolver del contratto dati  
 La creazione di un resolver del contratto dati prevede l'implementazione di due metodi, <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> e <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A>.Questi due metodi implementano callback utilizzati rispettivamente durante la serializzazione e la deserializzazione.Il metodo <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> viene richiamato durante la serializzazione, utilizza un tipo di contratto dati e ne esegue il mapping a un nome e a uno spazio dei nomi `xsi:type`.Il metodo <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> viene richiamato durante la deserializzazione, utilizza un nome e uno spazio dei nomi `xsi:type` e lo risolve in un tipo di contratto dati.Entrambi questi metodi dispongono di un parametro `knownTypeResolver` che può essere impiegato per utilizzare il resolver del tipo noto predefinito nell'implementazione.  
  
 Nell'esempio seguente viene mostrato come implementare un <xref:System.Runtime.Serialization.DataContractResolver> con cui eseguire il mapping con un tipo di contratto dati denominato `Customer` derivato da un tipo di contratto dati `Person`.  
  
```csharp  
public class MyCustomerResolver : DataContractResolver  
{  
    public override bool TryResolveType(Type dataContractType, Type declaredType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        if (dataContractType == typeof(Customer))  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add("SomeCustomer");  
            typeNamespace = dictionary.Add("http://tempuri.com");  
            return true;  
        }  
        else  
        {  
            return knownTypeResolver.TryResolveType(dataContractType, declaredType, null, out typeName, out typeNamespace);  
        }  
    }  
  
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        if (typeName == "SomeCustomer" && typeNamespace == "http://tempuri.com")  
        {  
            return typeof(Customer);  
        }  
        else  
        {  
            return knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        }  
    }  
}  
```  
  
 Una volta definito un <xref:System.Runtime.Serialization.DataContractResolver>, è possibile utilizzarlo passandolo al costruttore <xref:System.Runtime.Serialization.DataContractSerializer>, come indicato nell'esempio seguente.  
  
```  
XmlObjectSerializer serializer = new DataContractSerializer(typeof(Customer), null, Int32.MaxValue, false, false, null, new MyCustomerResolver());  
```  
  
 È possibile specificare un <xref:System.Runtime.Serialization.DataContractSerializer> in una chiamata ai metodi <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A> o <xref:System.Runtime.Serialization.DataContractSerializer.WriteObject%2A>, come indicato nell'esempio seguente.  
  
```  
MemoryStream ms = new MemoryStream();  
DataContractSerializer serializer = new DataContractSerializer(typeof(Customer));  
XmlDictionaryWriter writer = XmlDictionaryWriter.CreateDictionaryWriter(XmlWriter.Create(ms));  
serializer.WriteObject(writer, new Customer(), new MyCustomerResolver());  
writer.Flush();  
ms.Position = 0;  
Console.WriteLine(((Customer)serializer.ReadObject(XmlDictionaryReader.CreateDictionaryReader(XmlReader.Create(ms)), false, new MyCustomerResolver()));  
  
```  
  
 È in alternativa possibile impostarlo su <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>, come indicato nell'esempio seguente.  
  
```  
ServiceHost host = new ServiceHost(typeof(MyService));  
  
ContractDescription cd = host.Description.Endpoints[0].Contract;  
OperationDescription myOperationDescription = cd.Operations.Find("Echo");  
  
DataContractSerializerOperationBehavior serializerBehavior = myOperationDescription.Behaviors.Find<DataContractSerializerOperationBehavior>();  
if (serializerBehavior == null)  
{  
    serializerBehavior = new DataContractSerializerOperationBehavior(myOperationDescription);  
    myOperationDescription.Behaviors.Add(serializerBehavior);  
}  
  
SerializerBehavior.DataContractResolver = new MyCustomerResolver();  
  
```  
  
 È possibile specificare in modo dichiarativo un resolver del contratto dati implementando un attributo che possa essere applicato a un servizio.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'esempio [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md).In questo esempio viene implementato un attributo denominato "KnownAssembly" che aggiunge un resolver del contratto dati personalizzato al comportamento del servizio.  
  
## Vedere anche  
 [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [Esempio di DataContractSerializer](../../../../docs/framework/wcf/samples/datacontractserializer-sample.md)   
 [KnownAssemblyAttribute](../../../../docs/framework/wcf/samples/knownassemblyattribute.md)