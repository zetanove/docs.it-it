---
title: Forma dei documenti WordprocessingML (C#) | Documentazione Microsoft
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
ms.assetid: 3791b5e0-c502-469b-bb75-a7bf6fdd0a94
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 29c8555df695f9e1a93256ea3a25ed22d441fd6d
ms.lasthandoff: 03/13/2017


---
# <a name="shape-of-wordprocessingml-documents-c"></a>Forma dei documenti WordprocessingML (C#)
In questo argomento viene descritta la forma XML di un documento WordprocessingML.  
  
## <a name="microsoft-office-formats"></a>Formati di Microsoft Office  
 Il formato di file nativo per Microsoft Office System 2007 è Office Open XML (più comunemente, Open XML). Open XML è un formato basato su XML conforme allo standard ECMA e attualmente in approvazione per gli standard ISO-IEC. Il linguaggio di markup per i file di elaborazione testi all'interno di Open XML è denominato WordprocessingML. In questa esercitazione vengono usati file di origine WordprocessingML come di input per gli esempi.  
  
 Se si usa Microsoft Office 2003, possibile salvare i documenti nel formato Office Open XML se è stato installato il pacchetto di compatibilità di Microsoft Office per i formati di file Word, Excel e PowerPoint 2007.  
  
## <a name="the-shape-of-wordprocessingml-documents"></a>Forma dei documenti WordprocessingML  
 Il primo aspetto da considerare è la forma dei documenti WordprocessingML. Un documento WordprocessingML contiene un elemento corpo, denominato `w:body`, che contiene i paragrafi del documento. Ogni paragrafo contiene una o più sequenze di testo, denominate `w:r`. Ogni sequenza di testo contiene uno o più parti di testo, denominate `w:t`.  
  
 Di seguito è riportato un documento WordprocessingML molto semplice:  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<w:document  
xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"  
xmlns:o="urn:schemas-microsoft-com:office:office"  
xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"  
xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"  
xmlns:v="urn:schemas-microsoft-com:vml"  
xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"  
xmlns:w10="urn:schemas-microsoft-com:office:word"  
xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">  
  <w:body>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is a paragraph.</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is another paragraph.</w:t>  
      </w:r>  
    </w:p>  
  </w:body>  
</w:document>  
```  
  
 Questo documento contiene due paragrafi. Entrambi contengono una sola sequenza di testo e ogni sequenza di testo contiene una sola parte di testo.  
  
 Il modo più semplice per visualizzare il contenuto di un documento WordprocessingML in formato XML consiste nel crearne uno usando Microsoft Word, salvarlo e quindi eseguire il programma seguente che stampa l'XML nella console.  
  
 In questo esempio vengono usate classi dell'assembly WindowsBase Usa i tipi nello spazio dei nomi <xref:System.IO.Packaging?displayProperty=fullName>.  
  
```csharp  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
using (Package wdPackage = Package.Open("SampleDoc.docx", FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship relationship =  
        wdPackage  
        .GetRelationshipsByType(documentRelationshipType)  
        .FirstOrDefault();  
    if (relationship != null)  
    {  
        Uri documentUri =  
            PackUriHelper.ResolvePartUri(  
                new Uri("/", UriKind.Relative),  
                relationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Get the officeDocument part from the package.  
        //  Load the XML in the part into an XDocument instance.  
        XDocument xdoc =  
            XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
        Console.WriteLine(xdoc.Root);  
    }  
}  
```  
  
## <a name="external-resources"></a>Risorse esterne  
 [Introduzione ai formati file Office (2007) Open XML](http://go.microsoft.com/fwlink/?LinkId=98093)  
  
 [Overview of WordprocessingML](http://go.microsoft.com/fwlink/?LinkId=98094) (Panoramica di WordprocessingML)  
  
 [Pagina di download Office 2003: XML Reference Schemas page](http://go.microsoft.com/fwlink/?LinkId=98095) (Schemi di riferimento XML)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: Manipolazione di contenuto in un documento WordprocessingML (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
