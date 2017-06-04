---
title: "Procedura: serializzare e deserializzare dati JSON | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 88abc1fb-8196-4ee3-a23b-c6934144d1dd
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: serializzare e deserializzare dati JSON
JSON (JavaScript Object Notation) è un efficiente formato di codifica dati che consente scambi rapidi di piccole quantità di dati tra browser client e servizi Web compatibili con AJAX.  
  
 In questo argomento viene illustrato come serializzare oggetti di tipo .NET in dati con codifica JSON e quindi come deserializzare i dati in formato JSON in istanze di tipi .NET utilizzando il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>. In questo esempio viene utilizzato un contratto dati per illustrare la serializzazione e la deserializzazione di un tipo `Person` definito dall'utente.  
  
 In genere, la serializzazione e la deserializzazione JSON vengono gestite automaticamente da [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] quando si utilizzano tipi di contratto dati nelle operazioni del servizio esposte su endpoint compatibili con AJAX. Tuttavia, in alcuni casi potrebbe essere necessario utilizzare direttamente dati JSON, come nel caso dello scenario descritto in questo argomento.  
  
> [!NOTE]
>  Se si verifica un errore durante la serializzazione di una risposta in uscita nel server o se l'operazione di risposta genera un'eccezione per qualche altro motivo, è possibile che l'errore non venga restituito al client.  
  
 Questo argomento è basato sul [la serializzazione JSON](../../../../docs/framework/wcf/samples/json-serialization.md) esempio.  
  
### <a name="to-define-the-data-contract-for-a-person"></a>Per definire il contratto dati per Person  
  
1.  Definire il contratto dati per `Person` collegando il <xref:System.Runtime.Serialization.DataContractAttribute> alla classe e <xref:System.Runtime.Serialization.DataMemberAttribute> attributo ai membri da serializzare. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]contratti dati, vedere [la progettazione di contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md).  
  
    ```  
    [DataContract]  
        internal class Person  
        {  
            [DataMember]  
            internal string name;  
  
            [DataMember]  
            internal int age;  
        }  
    ```  
  
### <a name="to-serialize-an-instance-of-type-person-to-json"></a>Per serializzare un'istanza di tipo Person in JSON  
  
1.  Creare un'istanza del tipo `Person`.  
  
    ```  
    Person p = new Person();  
    p.name = "John";  
    p.age = 42;  
    ```  
  
2.  Serializzare il `Person` oggetto in un flusso di memoria utilizzando il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.  
  
    ```  
    MemoryStream stream1 = new MemoryStream();  
    DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(Person));  
    ```  
  
3.  Utilizzare il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A> metodo per scrivere dati JSON nel flusso.  
  
    ```  
    ser.WriteObject(stream1, p);  
    ```  
  
4.  Visualizzare l'output JSON.  
  
    ```  
    stream1.Position = 0;  
    StreamReader sr = new StreamReader(stream1);  
    Console.Write("JSON form of Person object: ");  
    Console.WriteLine(sr.ReadToEnd());  
    ```  
  
### <a name="to-deserialize-an-instance-of-type-person-from-json"></a>Per deserializzare un'istanza di tipo Person da JSON  
  
1.  Deserializzare i dati con codifica JSON in una nuova istanza della `Person` utilizzando il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject%2A> metodo il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>.  
  
    ```  
    stream1.Position = 0;  
    Person p2 = (Person)ser.ReadObject(stream1);  
    ```  
  
2.  Visualizzare i risultati.  
  
    ```  
    Console.Write("Deserialized back, got name=");  
    Console.Write(p2.name);  
    Console.Write(", age=");  
    Console.WriteLine(p2.age);  
    ```  
  
## <a name="example"></a>Esempio  
  
```  
// Create a User object and serialize it to a JSON stream.  
public static string WriteFromObject()  
{  
    //Create User object.  
    User user = new User("Bob", 42);  
  
    //Create a stream to serialize the object to.  
    MemoryStream ms = new MemoryStream();  
  
    // Serializer the User object to the stream.  
    DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(User));  
    ser.WriteObject(ms, user);  
    byte[] json = ms.ToArray();  
    ms.Close();  
    return Encoding.UTF8.GetString(json, 0, json.Length);  
  
}  
  
// Deserialize a JSON stream to a User object.  
public static User ReadToObject(string json)  
{  
    User deserializedUser = new User();  
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(json));  
    DataContractJsonSerializer ser = new DataContractJsonSerializer(deserializedUser.GetType());  
    deserializedUser = ser.ReadObject(ms) as User;  
    ms.Close();  
    return deserializedUser;  
}  
  
```  
  
> [!NOTE]
>  Il serializzatore JSON genera un'eccezione di serializzazione per i contratti dati che dispongono di più membri con lo stesso nome, come illustrato nel codice di esempio seguente.  
  
```  
[DataContract]  
public class TestDuplicateDataBase  
{  
    [DataMember]  
    public int field1 = 123;  
}  
[DataContract]  
public class TestDuplicateDataDerived : TestDuplicateDataBase  
{  
    [DataMember]  
    public new int field1 = 999;  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Serializzazione JSON autonoma](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md)   
 [Supporto per JSON e altri dati formati di trasferimento](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)