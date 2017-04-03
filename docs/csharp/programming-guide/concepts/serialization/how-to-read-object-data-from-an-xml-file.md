---
title: 'Procedura: Leggere dati oggetto in un file XML (C#) | Documentazione Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 6ad60d96-a4d9-48e6-a8b0-d7f6f803cafa
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c5f8c23a86c7a09d6f8d0b8c6f1684a38d0336a3
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-object-data-from-an-xml-file-c"></a>Procedura: Leggere dati oggetto in un file XML (C#)
Questo esempio illustra in che modo è possibile leggere i dati oggetto precedentemente scritti in un file XML usando la classe <xref:System.Xml.Serialization.XmlSerializer>.  
  
## <a name="example"></a>Esempio  
  
```csharp  
public class Book  
{  
    public String title;  
}         
  
public void ReadXML()  
{  
    // First write something so that there is something to read ...  
    var b = new Book { title = "Serialization Overview" };  
    var writer = new System.Xml.Serialization.XmlSerializer(typeof(Book));  
    var wfile = new System.IO.StreamWriter(@"c:\temp\SerializationOverview.xml");  
    writer.Serialize(wfile, b);  
    wfile.Close();  
  
    // Now we can read the serialized book ...  
    System.Xml.Serialization.XmlSerializer reader =   
        new System.Xml.Serialization.XmlSerializer(typeof(Book));  
    System.IO.StreamReader file = new System.IO.StreamReader(  
        @"c:\temp\SerializationOverview.xml");  
    Book overview =  (Book)reader.Deserialize(file);  
    file.Close();  
  
    Console.WriteLine(overview.title);  
  
}  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Sostituire il nome di file "c:\temp\SerializationOverview.xml" con il nome del file contenente i dati serializzati. Per altre informazioni sulla serializzazione dei dati, vedere [Procedura: Scrivere i dati di un oggetto in un file XML (C#)](../../../../csharp/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md).  
  
 La classe deve avere un costruttore public senza parametri.  
  
 Solo le proprietà e i campi pubblici vengono deserializzati.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   La classe da serializzare non ha un costruttore pubblico senza parametri.  
  
-   I dati nel file non rappresentano i dati della classe da deserializzare.  
  
-   Il file non esiste (<xref:System.IO.IOException>).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Verificare sempre gli input e non deserializzare mai i dati proveniente da un'origine non attendibile. L'oggetto ricreato viene eseguito in un computer locale con le autorizzazioni del codice che ha eseguito la deserializzazione. Prima di usare i dati nell'applicazione verificare tutti gli input.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO.StreamWriter>   
 [Procedura: Scrivere i dati di un oggetto in un file XML (C#)](../../../../csharp/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)   
 [Serializzazione (C#)](../../../../csharp/programming-guide/concepts/serialization/index.md)   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)
