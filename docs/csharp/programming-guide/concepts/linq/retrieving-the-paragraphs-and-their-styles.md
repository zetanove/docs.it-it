---
title: Recupero dei paragrafi e dei relativi stili (C#) | Microsoft Docs
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
ms.assetid: c2f767f8-57b1-4b4b-af04-89ffb1f7067d
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fddaa5e25befc40278888c0b401ad39a61e8e9d4
ms.lasthandoff: 03/13/2017


---
# <a name="retrieving-the-paragraphs-and-their-styles-c"></a>Recupero dei paragrafi e dei relativi stili (C#)
In questo esempio viene scritta una query che recupera i nodi dei paragrafi da un documento WordprocessingML. Viene inoltre identificato lo stile di ciascun paragrafo.  
  
 Questa query si basa sulla query dell'esempio precedente, [Ricerca dello stile di paragrafo predefinito (C#)](../../../../csharp/programming-guide/concepts/linq/finding-the-default-paragraph-style.md), che recupera lo stile predefinito dall'elenco degli stili. Queste informazioni sono necessarie per consentire alla query di identificare gli stili dei paragrafi per i quali non è stato impostato uno stile in modo esplicito. Gli stili dei paragrafi vengono impostati tramite l'elemento `w:pPr`. Se un paragrafo non contiene tale elemento, verrà formattato con lo stile predefinito.  
  
 In questo argomento viene spiegata l'importanza di alcune parti della query e quindi viene illustrata la query in un esempio completo e funzionante.  
  
## <a name="example"></a>Esempio  
 L'origine della query per recuperare tutti i paragrafi di un documento e i relativi stili è la seguente:  
  
```csharp  
xDoc.Root.Element(w + "body").Descendants(w + "p")  
```  
  
 Questa espressione è simile all'origine della query dell'esempio precedente, [Ricerca dello stile di paragrafo predefinito (C#)](../../../../csharp/programming-guide/concepts/linq/finding-the-default-paragraph-style.md). La differenza principale è che viene usato l'asse <xref:System.Xml.Linq.XContainer.Descendants%2A> anziché l'asse <xref:System.Xml.Linq.XContainer.Elements%2A>. La query usa l'asse <xref:System.Xml.Linq.XContainer.Descendants%2A> perché nei documenti suddivisi in sezioni i paragrafi non saranno elementi figlio diretti dell'elemento del corpo, ma si troveranno due livelli più sotto nella gerarchia. Usando l'asse <xref:System.Xml.Linq.XContainer.Descendants%2A> il codice verrà eseguito correttamente anche se nel documento vengono usate sezioni.  
  
## <a name="example"></a>Esempio  
 La query usa una clausola `let` per determinare l'elemento che contiene il nodo dello stile. Se non è presente nessun elemento, `styleNode` viene impostato su `null`.  
  
```csharp  
let styleNode = para.Elements(w + "pPr").Elements(w + "pStyle").FirstOrDefault()  
```  
  
 La clausola `let` usa in primo luogo l'asse <xref:System.Xml.Linq.XContainer.Elements%2A>per trovare tutti gli elementi denominati `pPr`, quindi usa il metodo di estensione <xref:System.Xml.Linq.Extensions.Elements%2A> per trovare tutti gli elementi figlio denominati `pStyle` e infine usa l'operatore di query standard <xref:System.Linq.Enumerable.FirstOrDefault%2A> per convertire la raccolta in un singleton. Se la raccolta è vuota, `styleNode` viene impostato su `null`. Si tratta di un idioma utile per cercare il nodo dell'elemento discendente `pStyle`. Notare che se il nodo figlio `pPr` non esiste, il codice non viene eseguito e viene generata un'eccezione. `styleNode` viene invece impostato su `null`, che corrisponde al comportamento desiderato della clausola `let`.  
  
 La query proietta una raccolta di un tipo anonimo con due membri, `StyleName` e `ParagraphNode`.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene elaborato un documento WordprocessingML, recuperandone i nodi dei paragrafi da un documento WordprocessingML. Viene inoltre identificato lo stile di ciascun paragrafo. Questo esempio si basa su esempi precedenti di questa esercitazione. La nuova query è indicata nei commenti del codice riportato di seguito.  
  
 Per istruzioni per la creazione del documento di origine di questo esempio, vedere [Creazione del documento Office Open XML di origine (C#)](../../../../csharp/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md).  
  
 In questo esempio vengono usate classi dell'assembly WindowsBase Usa i tipi nello spazio dei nomi <xref:System.IO.Packaging?displayProperty=fullName>.  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative), docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
string defaultStyle =   
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
// Following is the new query that finds all paragraphs in the  
// document and their styles.  
var paragraphs =  
    from para in xDoc  
                 .Root  
                 .Element(w + "body")  
                 .Descendants(w + "p")  
    let styleNode = para  
                    .Elements(w + "pPr")  
                    .Elements(w + "pStyle")  
                    .FirstOrDefault()  
    select new  
    {  
        ParagraphNode = para,  
        StyleName = styleNode != null ?  
            (string)styleNode.Attribute(w + "val") :  
            defaultStyle  
    };  
  
foreach (var p in paragraphs)  
    Console.WriteLine("StyleName:{0}", p.StyleName);  
```  
  
 Questo esempio consente di ottenere il seguente output quando viene applicato al documento descritto in [Creazione del documento Office Open XML di origine (C#)](../../../../csharp/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md).  
  
```  
StyleName:Heading1  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
```  
  
## <a name="next-steps"></a>Passaggi successivi  
 Nell'argomento successivo, [Recupero del testo dei paragrafi (C#)](../../../../csharp/programming-guide/concepts/linq/retrieving-the-text-of-the-paragraphs.md), verrà creata una query per recuperare il testo dei paragrafi.  
  
## <a name="see-also"></a>Vedere anche  
 [Tutorial: Manipulating Content in a WordprocessingML Document (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md) (Esercitazione sulla modifica del contenuto in un documento WordprocessingML (C#))
