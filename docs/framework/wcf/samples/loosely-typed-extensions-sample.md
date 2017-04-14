---
title: "Esempio di estensioni non fortemente tipizzate | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56ce265b-8163-4b85-98e7-7692a12c4357
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Esempio di estensioni non fortemente tipizzate
Il modello a oggetti di diffusione fornisce supporto dettagliato per lavorare con dati dell'estensione: informazioni presenti nella rappresentazione XML di un feed ma non esposte in modo esplicito da classi quali <xref:System.ServiceModel.Syndication.SyndicationFeed> e <xref:System.ServiceModel.Syndication.SyndicationItem>.In questo esempio vengono illustrate le tecniche di base per lavorare con i dati dell'estensione.  
  
 Nell'esempio seguente viene utilizzata la classe <xref:System.ServiceModel.Syndication.SyndicationFeed> a scopo esemplificativo.Tuttavia, i modelli illustrati in questo esempio possono essere utilizzati con tutte le classi di diffusione che supportano dati di estensione:  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
 <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
 <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
 <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
## Esempio XML  
 A scopo di riferimento, in questo esempio viene utilizzato il documento XML seguente.  
  
```  
<?xml version="1.0" encoding="IBM437"?>  
<feed myAttribute="someValue" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text"></title>  
  <id>uuid:8f60c7b3-a3c0-4de7-a642-2165d77ce3c1;id=1</id>  
  <updated>2007-09-07T22:15:34Z</updated>  
  <simpleString xmlns="">hello, world!</simpleString>  
  <simpleString xmlns="">another simple string</simpleString>  
  <DataContractExtension xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.d  
atacontract.org/2004/07/Microsoft.Syndication.Samples">  
    <Key>X</Key>  
    <Value>4</Value>  
  </DataContractExtension>  
  <XmlSerializerExtension xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://ww  
w.w3.org/2001/XMLSchema" xmlns="">  
    <Key>Y</Key>  
    <Value>8</Value>  
  </XmlSerializerExtension>  
  <xElementExtension xmlns="">  
    <Key attr1="someValue">Z</Key>  
    <Value attr1="someValue">15</Value>  
  </xElementExtension>  
</feed>  
  
```  
  
 Questo documento contiene le seguenti porzioni di dati dell'estensione:  
  
-   Attributo `myAttribute` dell'elemento `<feed>`.  
  
-   Elemento `<simpleString>`.  
  
-   Elemento `<DataContractExtension>`.  
  
-   Elemento `<XmlSerializerExtension>`.  
  
-   Elemento `<xElementExtension>`.  
  
## Scrittura dati dell'estensione  
 Le estensioni dell'attributo vengono create aggiungendo voci alla raccolta <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> come mostra il codice di esempio seguente.  
  
```  
//Attribute extensions are stored in a dictionary indexed by   
// XmlQualifiedName  
feed.AttributeExtensions.Add(new XmlQualifiedName("myAttribute", ""), "someValue");  
  
```  
  
 Le estensioni dell'elemento vengono create aggiungendo voci alla raccolta <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A>.Queste estensioni possono essere valori di base quali stringhe, serializzazioni XML di oggetti .NET Framework o nodi XML codificati a mano.  
  
 Il codice di esempio seguente crea un elemento dell'estensione denominato `simpleString`.  
  
```  
feed.ElementExtensions.Add("simpleString", "", "hello, world!");  
  
```  
  
 Lo spazio dei nomi XML per questo elemento è lo spazio dei nomi vuoto \(""\) e il valore è un nodo di testo che contiene la stringa "hello, world\!".  
  
 Un modo per creare estensioni dell'elemento complesse costituite da molti elementi annidati, consiste nell'utilizzare le API .NET Framework per la serializzazione \(sia <xref:System.Runtime.Serialization.DataContractSerializer> sia <xref:System.Xml.Serialization.XmlSerializer> sono supportate\), come illustrato negli esempi seguenti.  
  
```  
feed.ElementExtensions.Add( new DataContractExtension() { Key = "X", Value = 4 } );  
feed.ElementExtensions.Add( new XmlSerializerExtension { Key = "Y", Value = 8 }, new XmlSerializer( typeof( XmlSerializerExtension ) ) );  
  
```  
  
 In questo esempio, `DataContractExtension` e `XmlSerializerExtension` sono tipi personalizzati scritti per l'utilizzo con un serializzatore.  
  
 La classe <xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection> può essere utilizzata anche per creare estensioni dell'elemento da un'istanza <xref:System.Xml.XmlReader>.Ciò consente una facile integrazione con l'elaborazione API XML ad esempio <xref:System.Xml.Linq.XElement> come mostra il codice di esempio seguente.  
  
```  
feed.ElementExtensions.Add(new XElement("xElementExtension",  
        new XElement("Key", new XAttribute("attr1", "someValue"), "Z"),  
        new XElement("Value", new XAttribute("attr1", "someValue"),   
        "15")).CreateReader());  
  
```  
  
## Lettura dati dell'estensione  
 I valori per le estensioni dell'attributo possono essere ottenuti cercando l'attributo nella raccolta <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> tramite la classe <xref:System.Xml.XmlQualifiedName> come mostra il codice di esempio seguente.  
  
```  
Console.WriteLine( feed.AttributeExtensions[ new XmlQualifiedName( "myAttribute", "" )]);  
  
```  
  
 L'accesso alle estensioni dell'elemento viene effettuato utilizzando il metodo `ReadElementExtensions<T>`.  
  
```  
foreach( string s in feed2.ElementExtensions.ReadElementExtensions<string>("simpleString", ""))  
{  
    Console.WriteLine(s);  
}  
  
foreach (DataContractExtension dce in feed2.ElementExtensions.ReadElementExtensions<DataContractExtension>("DataContractExtension",  
"http://schemas.datacontract.org/2004/07/SyndicationExtensions"))  
{  
    Console.WriteLine(dce.ToString());  
}  
  
foreach (XmlSerializerExtension xse in feed2.ElementExtensions.ReadElementExtensions<XmlSerializerExtension>("XmlSerializerExtension", "", new XmlSerializer(typeof(XmlSerializerExtension))))  
{  
    Console.WriteLine(xse.ToString());  
}  
  
```  
  
 È anche possibile ottenere un `XmlReader` per estensioni dell'elemento singole utilizzando il metodo <xref:System.ServiceModel.Syndication.SyndicationElementExtension.GetReader>.  
  
```  
  
foreach (SyndicationElementExtension extension in feed2.ElementExtensions.Where<SyndicationElementExtension>(x => x.OuterName == "xElementExtension"))  
{  
    XNode xelement = XElement.ReadFrom(extension.GetReader());  
    Console.WriteLine(xelement.ToString());  
}  
  
```  
  
#### Per impostare, compilare ed eseguire l'esempio DIBLOOK  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Syndication\LooselyTypedExtensions`  
  
## Vedere anche  
 [Estensioni fortemente tipizzate](../../../../docs/framework/wcf/samples/strongly-typed-extensions-sample.md)   
 [Diffusione WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)