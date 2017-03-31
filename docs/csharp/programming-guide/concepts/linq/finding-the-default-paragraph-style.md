---
title: Ricerca dello stile di paragrafo predefinito (C#) | Microsoft Docs
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
ms.assetid: be102177-8ab0-444a-b671-7023e555ffdb
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 71aa37ffc086298470b713470afb4c28d3c5fcca
ms.lasthandoff: 03/13/2017


---
# <a name="finding-the-default-paragraph-style-c"></a>Ricerca dello stile di paragrafo predefinito (C#)
La prima attività dell'esercitazione Modifica di informazioni in un documento WordprocessingML consiste nell'individuare lo stile predefinito dei paragrafi del documento.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene aperto un documento WordprocessingML di Office Open XML, vengono individuate le parti del package relative a documento e stile, quindi viene eseguita una query che trova il nome dello stile predefinito. Per informazioni sui pacchetti di documenti Office Open XML e sulle parti da cui sono costituiti, vedere [Dettagli di documenti WordprocessingML Office Open XML (C#)](../../../../csharp/programming-guide/concepts/linq/details-of-office-open-xml-wordprocessingml-documents.md).  
  
 La query cerca un nodo denominato `w:style` che ha un attributo denominato `w:type` con il valore "paragraph" e un attributo denominato `w:default` con il valore "1". Poiché sarà disponibile un solo nodo XML con questi attributi, la query usa l'operatore <xref:System.Linq.Enumerable.First%2A?displayProperty=fullName> per convertire una raccolta in un singleton. Ottiene quindi il valore dell'attributo con il nome `w:styleId`.  
  
 In questo esempio vengono usate classi dell'assembly WindowsBase Usa i tipi nello spazio dei nomi <xref:System.IO.Packaging?displayProperty=fullName>.  
  
### <a name="code"></a>Codice  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship =  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
          docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation =  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
// The following query finds all the paragraphs that have the default style.  
string defaultStyle =   
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
Console.WriteLine("The default style is: {0}", defaultStyle);  
```  
  
### <a name="comments"></a>Commenti  
 Questo esempio produce il seguente output:  
  
```  
The default style is: Normal  
```  
  
## <a name="next-steps"></a>Passaggi successivi  
 Nell'esempio successivo verrà creata una query simile che trova tutti i paragrafi in un documento e i relativi stili:  
  
-   [Recupero dei paragrafi e dei relativi stili (C#)](../../../../csharp/programming-guide/concepts/linq/retrieving-the-paragraphs-and-their-styles.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione: manipolazione di contenuto in un documento WordprocessingML](http://msdn.microsoft.com/library/2696355e-4f83-4eaf-91b2-baa721f42fb4)
