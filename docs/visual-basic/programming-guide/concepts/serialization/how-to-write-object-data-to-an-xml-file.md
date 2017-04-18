---
title: 'Procedura: scrivere dati oggetto in un File XML (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: f7966480-5ed2-43ac-9894-33427436de2a
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 146ccb7b1999049106d5f0be1ce78e740dfcf060
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-write-object-data-to-an-xml-file-visual-basic"></a>Procedura: scrivere dati oggetto in un File XML (Visual Basic)
TIl esempio scrive l'oggetto da una classe in un file XML utilizzando la <xref:System.Xml.Serialization.XmlSerializer>classe.</xref:System.Xml.Serialization.XmlSerializer>  
  
## <a name="example"></a>Esempio  
  
```vb  
Public Module XMLWrite  
  
    Sub Main()  
        WriteXML()  
    End Sub  
  
    Public Class Book  
        Public Title As String  
    End Class  
  
    Public Sub WriteXML()  
        Dim overview As New Book  
        overview.Title = "Serialization Overview"  
        Dim writer As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
        Dim file As New System.IO.StreamWriter(  
            "c:\temp\SerializationOverview.xml")  
        writer.Serialize(file, overview)  
        file.Close()  
    End Sub  
End Module  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 La classe deve avere un costruttore pubblico senza parametri.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   La classe da serializzare non dispone di un costruttore pubblico senza parametri.  
  
-   Il file esiste ed è di sola lettura (<xref:System.IO.IOException>).</xref:System.IO.IOException>  
  
-   Il percorso è troppo lungo (<xref:System.IO.PathTooLongException>).</xref:System.IO.PathTooLongException>  
  
-   Il disco è pieno (<xref:System.IO.IOException>).</xref:System.IO.IOException>  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Questo esempio crea un nuovo file, se il file non esiste già. Se un'applicazione deve creare un file, l'applicazione deve `Create` accesso per la cartella. Se il file esiste già, l'applicazione deve solo `Write` accedere, un privilegio inferiore. Dove possibile, è più sicuro creare il file durante la distribuzione e concedere solo `Read` accesso a un singolo file, anziché `Create` accesso per una cartella.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.IO.StreamWriter></xref:System.IO.StreamWriter>   
 [Procedura: leggere dati oggetto in un File XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-read-object-data-from-an-xml-file.md)   
 [Serializzazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)
