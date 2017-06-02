---
title: "Surrogato di DataContract | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b0188f3c-00a9-4cf0-a887-a2284c8fb014
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Surrogato di DataContract
In questo esempio viene illustrato come la serializzazione, la deserializzazione, l'esportazione e l'importazione di schemi possano essere personalizzate utilizzando una classe surrogata del contratto dati.Il questo esempio viene descritto come utilizzare un surrogato in uno scenario client e server in cui i dati vengono serializzati e trasmessi tra un client e un servizio di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Nell'esempio di codice seguente viene utilizzato il contratto di servizio seguente:  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
[AllowNonSerializableTypes]  
public interface IPersonnelDataService  
{  
    [OperationContract]  
    void AddEmployee(Employee employee);  
  
    [OperationContract]  
    Employee GetEmployee(string name);  
}  
```  
  
 L'operazione `AddEmployee` consente agli utenti di aggiungere dati relativi ai nuovi dipendenti e l'operazione `GetEmployee` supporta la ricerca dei dipendenti in base al nome.  
  
 Queste operazioni utilizzano il tipo di dati seguente:  
  
```  
[DataContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
class Employee  
{  
    [DataMember]  
    public DateTime dateHired;  
  
    [DataMember]  
    public Decimal salary;  
  
    [DataMember]  
    public Person person;  
}  
  
```  
  
 Nel tipo `Employee`, la classe `Person` \(descritta nell'esempio di codice seguente\) non può essere serializzata da <xref:System.Runtime.Serialization.DataContractSerializer> perché non è una classe del contratto dati valida.  
  
```  
public class Person  
{  
    public string firstName;  
  
    public string lastName;  
  
    public int age;  
  
    public Person() { }  
}  
```  
  
 È possibile applicare l'attributo `DataContract` alla classe `Person`, ma questa operazione non è sempre possibile.Ad esempio, la classe `Person` può essere definita in un assembly separato sul quale non si ha alcun controllo.  
  
 Data questa restrizione, un modo di serializzare la classe `Person` è di sostituirla con un'altra classe contrassegnata con `DataContractAttribute` e copiare i dati necessari nella nuova classe.L'obiettivo è che la classe `Person` appaia come una classe DataContract per <xref:System.Runtime.Serialization.DataContractSerializer>.Si noti che questo è un modo di serializzare classi diverse da DataContract.  
  
 L'esempio sostituisce logicamente la classe `Person` con una classe diversa denominata `PersonSurrogated`.  
  
```  
[DataContract(Name="Person", Namespace = "http://Microsoft.ServiceModel.Samples")]  
public class PersonSurrogated  
{  
    [DataMember]  
    public string FirstName;  
  
    [DataMember]  
    public string LastName;  
  
    [DataMember]  
    public int Age;  
}  
  
```  
  
 Per eseguire questa sostituzione, viene utilizzato il surrogato del contratto dati.Un surrogato di un contratto dati rappresenta una classe che implementa <xref:System.Runtime.Serialization.IDataContractSurrogate>.In questo esempio, la classe `AllowNonSerializableTypesSurrogate` implementa questa interfaccia.  
  
 Nell'implementazione dell'interfaccia, la prima attività consiste nello stabilire un mapping dei tipi da `Person` a `PersonSurrogated`.Questo mapping viene utilizzato sia al momento della serializzazione che al momento dell'esportazione degli schemi.Questo mapping viene realizzato implementando il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%28System.Type%29>.  
  
```  
public Type GetDataContractType(Type type)  
{  
    if (typeof(Person).IsAssignableFrom(type))  
    {  
        return typeof(PersonSurrogated);  
    }  
    return type;  
}  
  
```  
  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%28System.Object%2CSystem.Type%29> esegue il mapping di un'istanza `Person` a un'istanza `PersonSurrogated` durante il serializzazione, come illustrato nell'esempio di codice seguente.  
  
```  
public object GetObjectToSerialize(object obj, Type targetType)  
{  
    if (obj is Person)  
    {  
        Person person = (Person)obj;  
        PersonSurrogated personSurrogated = new PersonSurrogated();  
        personSurrogated.FirstName = person.firstName;  
        personSurrogated.LastName = person.lastName;  
        personSurrogated.Age = person.age;  
        return personSurrogated;  
    }  
    return obj;  
}  
  
```  
  
 Il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%28System.Object%2CSystem.Type%29> fornisce il mapping inverso per la deserializzazione, come illustrato nell'esempio di codice seguente.  
  
```  
public object GetDeserializedObject(object obj,   
Type targetType)  
{  
    if (obj is PersonSurrogated)  
    {  
        PersonSurrogated personSurrogated = (PersonSurrogated)obj;  
        Person person = new Person();  
        person.firstName = personSurrogated.FirstName;  
        person.lastName = personSurrogated.LastName;  
        person.age = personSurrogated.Age;  
        return person;  
    }  
    return obj;  
}  
  
```  
  
 Per eseguire il mapping del contratto dati `PersonSurrogated` alla classe `Person` esistente durante l'importazione degli schemi, l'esempio implementa il metodo <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%28System.String%2CSystem.String%2CSystem.Object%29>, come illustrato nell'esempio di codice seguente.  
  
```  
public Type GetReferencedTypeOnImport(string typeName,   
               string typeNamespace, object customData)  
{  
if (  
typeNamespace.Equals("http://schemas.datacontract.org/2004/07/DCSurrogateSample")  
)  
    {  
         if (typeName.Equals("PersonSurrogated"))  
        {  
             return typeof(Person);  
        }  
     }  
     return null;  
}  
  
```  
  
 Nell'esempio di codice seguente viene completata l'implementazione dell'interfaccia <xref:System.Runtime.Serialization.IDataContractSurrogate>.  
  
```  
public System.CodeDom.CodeTypeDeclaration ProcessImportedType(  
          System.CodeDom.CodeTypeDeclaration typeDeclaration,   
          System.CodeDom.CodeCompileUnit compileUnit)  
{  
    return typeDeclaration;  
}  
public object GetCustomDataToExport(Type clrType,   
                               Type dataContractType)  
{  
    return null;  
}  
  
public object GetCustomDataToExport(  
System.Reflection.MemberInfo memberInfo, Type dataContractType)  
{  
    return null;  
}  
public void GetKnownCustomDataTypes(  
        KnownTypeCollection customDataTypes)  
{  
    // It does not matter what we do here.  
    throw new NotImplementedException();  
}  
  
```  
  
 In questo esempio, il surrogato viene attivato in ServiceModel da un attributo denominato `AllowNonSerializableTypesAttribute`.Gli sviluppatori devono applicare questo attributo al contratto di servizio, come illustrato nel contratto di servizio `IPersonnelDataService` precedente.Questo attributo implementa `IContractBehavior` e configura il surrogato sulle operazioni nei metodi `ApplyClientBehavior` e `ApplyDispatchBehavior`.  
  
 In questo caso l'attributo non è necessario: in questo esempio viene utilizzato solo per scopi dimostrativi.In alternativa gli utenti possono attivare un surrogato aggiungendo manualmente `IContractBehavior`, `IEndpointBehavior` o `IOperationBehavior` simili utilizzando il codice o la configurazione.  
  
 L'implementazione `IContractBehavior` cerca le operazioni che utilizzano DataContract verificando se hanno registrato un `DataContractSerializerOperationBehavior`.In questo caso, imposta la proprietà `DataContractSurrogate` su quel comportamento.Nell'esempio di codice seguente, viene illustrato come eseguire questa operazione.L'impostazione del surrogato su questo comportamento dell'operazione lo abilita per la serializzazione e la deserializzazione.  
  
```  
public void ApplyClientBehavior(ContractDescription description, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.ClientRuntime proxy)  
{  
    foreach (OperationDescription opDesc in description.Operations)  
    {  
        ApplyDataContractSurrogate(opDesc);  
    }  
}  
  
public void ApplyDispatchBehavior(ContractDescription description, ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.DispatchRuntime dispatch)  
{  
    foreach (OperationDescription opDesc in description.Operations)  
    {  
        ApplyDataContractSurrogate(opDesc);  
    }  
}  
  
private static void ApplyDataContractSurrogate(OperationDescription description)  
{  
    DataContractSerializerOperationBehavior dcsOperationBehavior = description.Behaviors.Find<DataContractSerializerOperationBehavior>();  
    if (dcsOperationBehavior != null)  
    {  
        if (dcsOperationBehavior.DataContractSurrogate == null)  
            dcsOperationBehavior.DataContractSurrogate = new AllowNonSerializableTypesSurrogate();  
    }  
}  
```  
  
 È necessario eseguire altri passaggi per inserire il surrogato perché possa essere utilizzato durante la generazione di metadati.Un modo di eseguire questa operazione è di fornire un `IWsdlExportExtension`, come illustrato in questo esempio.Un altro modo è di modificare direttamente `WsdlExporter`.  
  
 L'attributo `AllowNonSerializableTypesAttribute`  implementa `IWsdlExportExtension` e `IContractBehavior`.In questo caso, l'estensione può essere `IContractBehavior` o `IEndpointBehavior` .L'implementazione del metodo `IWsdlExportExtension.ExportContract` abilita il surrogato aggiungendolo al `XsdDataContractExporter` utilizzato durante la generazione degli schemi DataContract.Nel frammento di codice seguente viene illustrato come eseguire questa operazione.  
  
```  
public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)  
{  
    if (exporter == null)  
        throw new ArgumentNullException("exporter");  
  
    object dataContractExporter;  
    XsdDataContractExporter xsdDCExporter;  
    if (!exporter.State.TryGetValue(typeof(XsdDataContractExporter), out dataContractExporter))  
    {  
        xsdDCExporter = new XsdDataContractExporter(exporter.GeneratedXmlSchemas);  
        exporter.State.Add(typeof(XsdDataContractExporter), xsdDCExporter);  
    }  
    else  
    {  
        xsdDCExporter = (XsdDataContractExporter)dataContractExporter;  
    }  
    if (xsdDCExporter.Options == null)  
        xsdDCExporter.Options = new ExportOptions();  
  
    if (xsdDCExporter.Options.DataContractSurrogate == null)  
        xsdDCExporter.Options.DataContractSurrogate = new AllowNonSerializableTypesSurrogate();  
}  
```  
  
 Quando si esegue l'esempio, il client chiama AddEmployee, quindi chiama GetEmployee per verificare se la prima chiamata è stata completata correttamente.Il risultato della richiesta di un'operazione GetEmployee viene visualizzato nella finestra della console client.Se l'operazione GetEmployee riesce a individuare il dipendente, stampa "found".  
  
> [!NOTE]
>  In questo esempio viene illustrato come inserire un surrogato per la serializzazione, la deserializzazione e la generazione di metadati.Non viene descritto come inserire un surrogato per la generazione di codice dai metadati.Per sapere come utilizzare un surrogato per inserire la generazione di codice client, vedere l'esempio [Pubblicazione WSDL personalizzata](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md).  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\DataContract`  
  
## Vedere anche