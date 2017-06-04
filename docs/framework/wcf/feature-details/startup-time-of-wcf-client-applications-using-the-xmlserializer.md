---
title: "Procedura: migliorare il tempo di avvio di applicazioni client WCF utilizzando XmlSerializer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21093451-0bc3-4b1a-9a9d-05f7f71fa7d0
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: migliorare il tempo di avvio di applicazioni client WCF utilizzando XmlSerializer
I servizi e le applicazioni client che utilizzano tipi di dati serializzabili tramite <xref:System.Xml.Serialization.XmlSerializer> generano e compilano il codice di serializzazione per tali dati in fase di esecuzione, il che può rallentare le prestazioni all'avvio.  
  
> [!NOTE]
>  Un codice di serializzazione pregenerato può essere utilizzato solamente nelle applicazioni client e non nei servizi.  
  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) può migliorare le prestazioni all'avvio per queste applicazioni generando il codice di serializzazione necessario dagli assembly compilati per l'applicazione.Svcutil.exe genera codice di serializzazione per tutti i tipi di dati utilizzati nei contratti di servizio nell'assembly dell'applicazione compilata che può essere serializzato utilizzando <xref:System.Xml.Serialization.XmlSerializer>.I contratti del servizio e dell'operazione che utilizzano <xref:System.Xml.Serialization.XmlSerializer> sono contrassegnati con <xref:System.ServiceModel.XmlSerializerFormatAttribute>.  
  
### Per generare il codice di serializzazione XmlSerializer  
  
1.  Compilare il codice del servizio o del client in uno o più assembly.  
  
2.  Aprire un prompt dei comandi SDK.  
  
3.  Al prompt dei comandi, avviare lo strumento Svcutil.exe utilizzando il formato seguente.  
  
    ```  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     L'argomento `assemblyPath` specifica il percorso di un assembly che contiene tipi di contratto di servizio.Svcutil.exe genera codice di serializzazione per tutti i tipi di dati utilizzati nei contratti di servizio nell'assembly dell'applicazione compilata che può essere serializzato utilizzando <xref:System.Xml.Serialization.XmlSerializer>.  
  
     Svcutil.exe può generare solo codice di serializzazione C\#.Viene generato un file di codice sorgente per ogni assembly di input.Non è possibile utilizzare l'opzione **\/language** per cambiare il linguaggio del codice generato.  
  
     Per specificare il percorso di assembly dipendenti, utilizzare l'opzione **\/reference**.  
  
4.  Rendere il codice di serializzazione generato disponibile all'applicazione utilizzando una delle opzioni seguenti:  
  
    1.  Compilare il codice di serializzazione generato in un assembly separato con il nome \[*original assembly*\].XmlSerializers.dll, ad esempio, MyApp.XmlSerializers.dll.L'applicazione deve essere in grado di caricare l'assembly che deve essere firmato con la stessa chiave dell'assembly originale.Se si ricompila l'assembly originale, è necessario rigenerare l'assembly di serializzazione.  
  
    2.  Compilare il codice di serializzazione generato in un assembly separato e utilizzare <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute> sul contratto di servizio che utilizza <xref:System.ServiceModel.XmlSerializerFormatAttribute>.Impostare le proprietà <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> o <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> per puntare all'assembly di serializzazione compilato.  
  
    3.  Compilare il codice di serializzazione generato nell'assembly dell'applicazione e aggiungere <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute> al contratto di servizio che utilizza <xref:System.ServiceModel.XmlSerializerFormatAttribute>.Non impostare le proprietà <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> o <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A>.L'assembly corrente viene considerato automaticamente l'assembly di serializzazione predefinito.  
  
## Esempio  
 Nel comando seguente vengono generati i tipi di serializzazione per i tipi `XmlSerializer` utilizzati da qualsiasi contratto di servizio nell'assembly.  
  
```  
svcutil /t:xmlserializer myContractLibrary.exe  
```  
  
## Vedere anche  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)