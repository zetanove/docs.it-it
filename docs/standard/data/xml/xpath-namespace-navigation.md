---
title: "Navigazione dello spazio dei nomi XPath | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 06cc7abb-7416-415c-9dd6-67751b8cabd5
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Navigazione dello spazio dei nomi XPath
Per usare le query XPath con i documenti XML, è necessario indirizzare correttamente gli spazi dei nomi XML e gli elementi da questi contenuti.  Gli spazi dei nomi evitano le ambiguità che si possono verificare quando i nomi vengono usati in più contesti; ad esempio il nome `ID` potrebbe far riferimento a più identificatori associati a diversi elementi di un documento XML.  La sintassi dello spazio dei nomi specifica gli URI, i nomi e i prefissi che distinguono gli elementi di un documento XML.  
  
 Nell'esempio di questo argomento viene illustrato l'uso di prefissi nella navigazione di un documento XML con l'oggetto <xref:System.Xml.XPath.XPathNavigator>.  Per altre informazioni sugli spazi dei nomi e sulla sintassi, vedere la [descrizione degli spazi dei nomi XML](http://go.microsoft.com/fwlink/?linkid=140245).  
  
## Dichiarazioni dello spazio dei nomi  
 Le dichiarazioni dello spazio dei nomi consentono di distinguere e indirizzare gli elementi di un documento XML quando si usa un'istanza dell'oggetto <xref:System.Xml.XPath.XPathNavigator>.  I prefissi dello spazio dei nomi forniscono una breve sintassi per l'indirizzamento degli spazi dei nomi.  
  
 I prefissi sono definiti dal formato: `<e:Envelope xmlns:e=http://schemas.xmlsoap.org/soap/envelope/>.` In questa sintassi il prefisso "`e`" è un'abbreviazione dell'URI formale dello spazio dei nomi.  È possibile identificare l'elemento `Body` come membro dello spazio dei nomi `Envelope` tramite la sintassi: `e:Body`.  
  
 Nell'esempio di navigazione della sezione successiva, al seguente documento XML verrà fatto riferimento come `response.xml`.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<e:Envelope xmlns:e="http://schemas.xmlsoap.org/soap/envelope/">  
  <e:Body>  
    <s:Search xmlns:s="http://schemas.microsoft.com/v1/Search">  
      <r:request xmlns:r="http://schemas.microsoft.com/v1/Search/metadata"   
                 xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
      </r:request>  
    </s:Search>  
  </e:Body>  
</e:Envelope>  
  
```  
  
## Navigazione tramite il prefisso dello spazio dei nomi  
 Nel codice di questa sezione vengono usati gli oggetti <xref:System.Xml.XPath.XPathNavigator> e <xref:System.Xml.XmlNamespaceManager> per selezionare l'elemento `Search` dal documento XML della sezione precedente.  La query `xpath` include i prefissi dello spazio dei nomi in ogni elemento del percorso.  Specificando l'esatta identità degli spazi dei nomi che contengono ogni elemento è possibile garantire la corretta navigazione all'elemento `Search` tramite il metodo <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>.  
  
```  
using (XmlReader reader = XmlReader.Create("response.xml"))  
            {  
                XPathDocument doc = new XPathDocument(reader);  
                XPathNavigator nav = doc.CreateNavigator();  
                XmlNamespaceManager nsmgr =  
                         new XmlNamespaceManager(nav.NameTable);  
                nsmgr.AddNamespace("e",   
                         @"http://schemas.xmlsoap.org/soap/envelope/");  
                nsmgr.AddNamespace("s",   
                            @"http://schemas.microsoft.com/v1/Search");  
                nsmgr.AddNamespace("r",   
                   @"http://schemas.microsoft.com/v1/Search/metadata");  
                nsmgr.AddNamespace("i",   
                         @"http://www.w3.org/2001/XMLSchema-instance");  
  
                string xpath = "/e:Envelope/e:Body/s:Search";  
  
                XPathNavigator element = nav.SelectSingleNode(xpath, nsmgr);  
  
                Console.WriteLine("Element Prefix:" + element.Prefix +   
                           " Local name:" + element.LocalName);  
                Console.WriteLine("Namespace URI: " +   
                            element.NamespaceURI);  
  
            }  
  
```  
  
 La precisione assicurata dalla qualifica completa degli spazi dei nomi e dei nomi non è soltanto utile,  infatti da un breve esperimento con la definizione di documento e il codice degli esempi precedenti è possibile constatare che la navigazione senza nomi di elementi completi genera eccezioni.  Ad esempio la definizione di elemento: `<Search xmlns="http://schemas.microsoft.com/v1/Search">` e la query: stringa `xpath = "/s:Envelope/s:Body/Search";` senza il prefisso dello spazio dei nomi nell'elemento `Search` restituisce `null` invece dell'elemento `Search`.  
  
## Vedere anche  
 [Accesso ai dati XML con XPathNavigator](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)   
 [Selezione, valutazione e corrispondenza di dati XML con XPathNavigator](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)