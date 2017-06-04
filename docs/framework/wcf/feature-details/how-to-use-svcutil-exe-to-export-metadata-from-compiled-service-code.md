---
title: "Procedura: utilizzare Svcutil.exe per esportare metadati dal codice del servizio compilato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 95d0aed3-16a2-4398-89bb-39418eeb7355
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: utilizzare Svcutil.exe per esportare metadati dal codice del servizio compilato
Svcutil.exe è in grado di esportare metadati per servizi, contratti e tipi di dati in assembly compilati, come segue:  
  
-   Per esportare metadati per tutti i contratti di servizio compilati per un set di assembly utilizzando Svcutil.exe, specificare gli assembly come parametri di input.Questo è il comportamento predefinito.  
  
-   Per esportare metadati per un contratto di servizio utilizzando Svcutil.exe, specificare l'assembly o gli assembly del servizio come parametri di input.È necessario utilizzare l'opzione `/serviceName` per indicare il nome di configurazione del servizio che si desidera esportare.Svcutil.exe carica automaticamente il file di configurazione dell'assembly eseguibile specificato.  
  
-   Per esportare tutti i tipi di contratto dati all'interno di un set di assembly, utilizzare l'opzione `/dataContractOnly`.  
  
> [!NOTE]
>  Utilizzare l'opzione `/reference` per specificare il percorso dei file degli eventuali assembly dipendenti.  
  
### Per esportare metadati per contratti di servizio compilati  
  
1.  Compilare le implementazioni del contratto di servizio in una o più librerie di classi.  
  
2.  Eseguire Svcutil.exe sugli assembly compilati.  
  
    > [!NOTE]
    >  Potrebbe essere necessario utilizzare l'opzione `/reference` per specificare il percorso del file di eventuali assembly dipendenti.  
  
    ```  
    svcutil.exe Contracts.dll  
    ```  
  
### Per esportare metadati per un servizio compilato  
  
1.  Compilare l'implementazione del servizio in un assembly eseguibile.  
  
2.  Creare un file di configurazione per l'eseguibile del servizio e aggiungere una configurazione del servizio.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name="MyService" >  
            <endpoint address="finder" contract="IPeopleFinder" binding="wsHttpBinding" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
3.  Eseguire Svcutil.exe sull'eseguibile del servizio compilato utilizzando l'opzione `/serviceName` per specificare il nome di configurazione del servizio.  
  
    > [!NOTE]
    >  Potrebbe essere necessario utilizzare l'opzione `/reference` per specificare il percorso del file di eventuali assembly dipendenti.  
  
    ```  
    svcutil.exe /serviceName:MyService Service.exe /reference:path/Contracts.dll  
    ```  
  
### Per esportare metadati per contratti dati compilati  
  
1.  Compilare le implementazioni del contratto dati in una o più librerie di classi.  
  
2.  Eseguire Svcutil.exe sugli assembly compilati utilizzando l'opzione `/dataContract` per specificare che devono essere generati solo i metadati dei contratti dati.  
  
    > [!NOTE]
    >  Potrebbe essere necessario utilizzare l'opzione `/reference` per specificare il percorso del file di eventuali assembly dipendenti.  
  
    ```  
    svcutil.exe /dataContractOnly Contracts.dll  
    ```  
  
## Esempio  
 Nell'esempio seguente viene dimostrato come generare metadati per un'implementazione semplice del servizio e una configurazione.  
  
 Per esportare metadati per il contratto di servizio  
  
```  
svcutil.exe Contracts.dll  
```  
  
 Per esportare metadati per i contratti dati.  
  
```  
svcutil.exe /dataContractOnly Contracts.dll  
```  
  
 Per esportare metadati per l'implementazione del servizio  
  
```  
svcutil.exe /serviceName:MyService Service.exe /reference:<path>/Contracts.dll  
```  
  
 `<path>` è il percorso di Contracts.dll.  
  
```  
// The following service contract and data contracts are compiled into   
// Contracts.dll.  
[ServiceContract(ConfigurationName="IPeopleFinder")]  
public interface IPersonFinder  
{  
    [OperationContract]  
    Address GetAddress(Person s);  
}  
  
[DataContract]  
public class Person  
{  
    [DataMember]  
    public string firstName;  
    [DataMember]  
    public string lastName;  
    [DataMember]  
    public int age;  
}  
  
[DataContract]  
public class Address  
{  
    [DataMember]  
    public string city;  
    [DataMember]  
    public string state;  
    [DataMember]  
    public string street;  
    [DataMember]  
    public int zipCode;  
    [DataMember]  
    public Person person;  
}  
  
// The following service implementation is compiled into Service.exe.     
// This service uses the contracts specified in Contracts.dll.  
[ServiceBehavior(ConfigurationName = "MyService")]  
public class MyService : IPersonFinder  
{  
    public Address GetAddress(Person person)  
    {  
        Address address = new Address();  
        address.person = person;  
        return address;  
    }  
}  
  
<!-- The following is the configuration file for Service.exe. -->  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="MyService">  
         <endpoint  address="finder"  
                    binding="basicHttpBinding"  
                    contract="IPeopleFinder"/>  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Vedere anche  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Esportazione e importazione di metadati](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)