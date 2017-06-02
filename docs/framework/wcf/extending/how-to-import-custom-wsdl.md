---
title: "Procedura: importare informazioni WSDL personalizzate | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ddc3718d-ce60-44f6-92af-a5c67477dd99
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: importare informazioni WSDL personalizzate
In questo argomento viene descritto come importare informazioni WSDL personalizzate.  Per gestire le informazioni WSDL personalizzate, è necessario implementare l'interfaccia <xref:System.ServiceModel.Description.IWsdlImportExtension>.  
  
### Per importare informazioni WSDL personalizzate  
  
1.  Implementare <xref:System.ServiceModel.Description.IWsdlImportExtension>.  Implementare il metodo <xref:System.ServiceModel.Description.IWsdlImportExtension.BeforeImport%28System.Web.Services.Description.ServiceDescriptionCollection%2CSystem.Xml.Schema.XmlSchemaSet%2CSystem.Collections.Generic.ICollection%7BSystem.Xml.XmlElement%7D%29> per modificare i metadati prima che siano importati.  Implementare i metodi <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportEndpoint%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlEndpointConversionContext%29> e <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> per modificare i contratti e gli endpoint importati dai metadati.  Per accedere al contratto o all'endpoint personalizzato, usare l'oggetto contesto corrispondente \(<xref:System.ServiceModel.Description.WsdlContractConversionContext> o <xref:System.ServiceModel.Description.WsdlEndpointConversionContext>\):  
  
    ```  
    public class WsdlDocumentationImporter : IWsdlImportExtension  
       {  
          public void ImportContract(WsdlImporter importer, WsdlContractConversionContext context)  
    {  
            // Contract documentation  
         if (context.WsdlPortType.Documentation != null)  
         {  
               context.Contract.Behaviors.Add(new WsdlDocumentationImporter(context.WsdlPortType.Documentation));  
    }  
    // Operation documentation  
    foreach (Operation operation in context.WsdlPortType.Operations)  
    {  
    if (operation.Documentation != null)  
    {  
    OperationDescription operationDescription = context.Contract.Operations.Find(operation.Name);  
    if (operationDescription != null)  
    {  
                            operationDescription.Behaviors.Add(new WsdlDocumentationImporter(operation.Documentation));  
    }  
    }  
    }  
    }  
  
    public void BeforeImport(ServiceDescriptionCollection wsdlDocuments, XmlSchemaSet xmlSchemas, ICollection<XmlElement> policy)   
            {  
                Console.WriteLine("BeforeImport called.");  
            }  
  
    public void ImportEndpoint(WsdlImporter importer, WsdlEndpointConversionContext context)   
            {  
                Console.WriteLine("ImportEndpoint called.");  
            }  
       }  
    ```  
  
2.  Configurare l'applicazione client per l'uso dell'unità di importazione WSDL personalizzata.  Si noti che se si sta usando Svcutil.exe, è necessario aggiungere questa configurazione al file di configurazione di Svcutil.exe \(Svcutil.exe.config\):  
  
    ```  
    <system.serviceModel>  
          <client>  
            <endpoint   
              address="http://localhost:8000/Fibonacci"   
              binding="wsHttpBinding"  
              contract="IFibonacci"  
            />  
            <metadata>  
              <wsdlImporters>  
                <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
              </wsdlImporters>  
            </metadata>  
          </client>  
        </system.serviceModel>  
  
    ```  
  
3.  Creare una nuova istanza di <xref:System.ServiceModel.Description.WsdlImporter> \(passando l'istanza di <xref:System.ServiceModel.Description.MetadataSet> che contiene i documenti WSDL che si desidera importare\) e chiamare <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>:  
  
    ```  
    WsdlImporter importer = new WsdlImporter(metaDocs);          System.Collections.ObjectModel.Collection<ContractDescription> contracts  = importer.ImportAllContracts();  
  
    ```  
  
## Vedere anche  
 [Metadata](../../../../docs/framework/wcf/feature-details/metadata.md)   
 [Esportazione e importazione di metadati](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)   
 [Pubblicazione WSDL personalizzata](../../../../docs/framework/wcf/samples/custom-wsdl-publication.md)