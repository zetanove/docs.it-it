---
title: "Procedura: serializzare un oggetto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "oggetti, passaggi di serializzazione"
  - "serializzazione di oggetti"
ms.assetid: a1207d05-32b2-4953-8582-959607991227
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: serializzare un oggetto
Per serializzare un oggetto, creare prima l'oggetto da serializzare e impostarne proprietà e campi pubblici.A tale scopo, è necessario determinare il formato di trasporto in cui deve essere archiviato il flusso XML, come flusso o come file.Ad esempio, se il flusso XML deve essere salvato in forma permanente, creare un oggetto [FileStream](frlrfSystemIOFileStreamClassTopic).  
  
> [!NOTE]
>  Per ulteriori esempi di serializzazione XML, vedere [Esempi di serializzazione XML](../../../docs/framework/serialization/examples-of-xml-serialization.md).  
  
### Per serializzare un oggetto  
  
1.  Creare l'oggetto e impostarne le proprietà e i campi pubblici.  
  
2.  Construire un <xref:System.Xml.Serialization.XmlSerializer> che utilizza il tipo dell'oggetto.Per ulteriori informazioni, vedere i costruttori della classe <xref:System.Xml.Serialization.XmlSerializer>.  
  
3.  Chiamare il metodo <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A> per generare un flusso XML o una rappresentazione del file dei campi e delle proprietà pubbliche dell'oggetto.Nell'esempio riportato di seguito viene creato un file.  
  
    ```vb  
    Dim myObject As MySerializableClass = New MySerializableClass()  
    ' Insert code to set properties and fields of the object.  
    Dim mySerializer As XmlSerializer = New XmlSerializer(GetType(MySerializableClass))  
    ' To write to a file, create a StreamWriter object.  
    Dim myWriter As StreamWriter = New StreamWriter("myFileName.xml")  
    mySerializer.Serialize(myWriter, myObject)  
    myWriter.Close()  
    ```  
  
    ```csharp  
    MySerializableClass myObject = new MySerializableClass();  
    // Insert code to set properties and fields of the object.  
    XmlSerializer mySerializer = new   
    XmlSerializer(typeof(MySerializableClass));  
    // To write to a file, create a StreamWriter object.  
    StreamWriter myWriter = new StreamWriter("myFileName.xml");  
    mySerializer.Serialize(myWriter, myObject);  
    myWriter.Close();  
    ```  
  
## Vedere anche  
 [Introduzione alla serializzazione XML](../../../docs/framework/serialization/introducing-xml-serialization.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)