---
title: 'Procedura: leggere dati oggetto in un File XML (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 1e1423bf-74a4-4dde-a3bb-ae1bfc0a68ed
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c448d79a88517925712f79ed061aa90933e3f6d1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-object-data-from-an-xml-file-visual-basic"></a>Procedura: leggere dati oggetto in un File XML (Visual Basic)
In questo esempio legge i dati oggetto precedentemente scritti in un file XML utilizzando la <xref:System.Xml.Serialization.XmlSerializer>classe.</xref:System.Xml.Serialization.XmlSerializer>  
  
## <a name="example"></a>Esempio  
  
```vb  
Public Class Book  
    Public Title As String  
End Class  
  
Public Sub ReadXML()  
    Dim reader As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
    Dim file As New System.IO.StreamReader(  
        "c:\temp\SerializationOverview.xml")  
    Dim overview As Book  
    overview = CType(reader.Deserialize(file), Book)  
    Console.WriteLine(overview.Title)  
End Sub  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Sostituire il nome di file "c:\temp\SerializationOverview.xml" con il nome del file contenente i dati serializzati. Per ulteriori informazioni sulla serializzazione dei dati, vedere [procedura: scrivere dati oggetto in un File XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md).  
  
 La classe deve avere un costruttore pubblico senza parametri.  
  
 Solo i campi e proprietà pubbliche vengono deserializzati.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   La classe da serializzare non dispone di un costruttore pubblico senza parametri.  
  
-   I dati nel file non rappresentano i dati della classe da deserializzare.  
  
-   Il file non esiste (<xref:System.IO.IOException>).</xref:System.IO.IOException>  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Verificare sempre gli input e di non deserializzare mai dati da un'origine non attendibile. L'oggetto ricreato viene eseguito in un computer locale con le autorizzazioni del codice che viene deserializzato. Prima di usare i dati nell'applicazione verificare tutti gli input.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO.StreamWriter></xref:System.IO.StreamWriter>   
 [Procedura: scrivere dati oggetto in un File XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)   
 [Serializzazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)
