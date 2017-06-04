---
title: "XmlSchemaSet per la compilazione di schemi | Microsoft Docs"
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
ms.assetid: 55c4b175-3170-4071-9d60-dd5a42f79b54
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XmlSchemaSet per la compilazione di schemi
Viene descritto <xref:System.Xml.Schema.XmlSchemaSet>, ovvero una cache in cui è possibile archiviare e convalidare gli schemi XSD \(XML Schema Definition Language\).  
  
## La classe XmlSchemaSet  
 Il tipo <xref:System.Xml.Schema.XmlSchemaSet> è una cache in cui è possibile archiviare e convalidare gli schemi XSD \(XML Schema Definition Language\).  
  
 In <xref:System.Xml?displayProperty=fullName> versione 1.0, gli schemi XML venivano caricati in una classe <xref:System.Xml.Schema.XmlSchemaCollection> come una libreria di schemi.  In <xref:System.Xml?displayProperty=fullName> versione 2.0, le classi <xref:System.Xml.XmlValidatingReader> e <xref:System.Xml.Schema.XmlSchemaCollection> sono obsolete e sono state sostituite dai metodi <xref:System.Xml.XmlReader.Create%2A> e dalla classe <xref:System.Xml.Schema.XmlSchemaSet> rispettivamente.  
  
 Il tipo <xref:System.Xml.Schema.XmlSchemaSet> è stato introdotto per risolvere una serie di problemi che includono la compatibilità con gli standard, le prestazioni e il formato obsoleto dello schema XDR \(XML\-Data Reduced\) di Microsoft.  
  
 Di seguito viene riportato un confronto tra le classi <xref:System.Xml.Schema.XmlSchemaCollection> e <xref:System.Xml.Schema.XmlSchemaSet>.  
  
|XmlSchemaCollection|XmlSchemaSet|  
|-------------------------|------------------|  
|Supporta gli schemi XDR di Microsoft e gli schemi XML di W3C.|Supporta solo gli schemi XML di W3C.|  
|Gli schemi vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A>.|Gli schemi non vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>.  Questo fornisce prestazioni migliori durante la creazione della libreria di schemi.|  
|Ogni schema consente di generare una singola versione compilata che può creare "isole di schemi". Di conseguenza, tutte le operazioni di inclusione e importazione vengono eseguite nell'ambito di tale schema.|Gli schemi compilati consentono di generare un singolo schema logico, ovvero un "set" di schemi.  Gli schemi importati all'interno di uno schema vengono aggiunti direttamente al set.  Ciò significa che tutti i tipi sono disponibili per tutti gli schemi.|  
|Nella raccolta può essere presente solo uno schema per un determinato spazio dei nomi di destinazione.|È possibile aggiungere più schemi per lo stesso spazio dei nomi di destinazione, a condizione che non si verifichino conflitti di tipi.|  
  
## Migrazione a XmlSchemaSet  
 Nel seguente esempio di codice viene fornita una guida per eseguire la migrazione alla nuova classe <xref:System.Xml.Schema.XmlSchemaSet> dalla classe obsoleta <xref:System.Xml.Schema.XmlSchemaCollection>.  Nell'esempio di codice vengono illustrate le seguenti differenze principali tra le due classi.  
  
-   A differenza del metodo <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> della classe <xref:System.Xml.Schema.XmlSchemaCollection>, gli schemi non vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> viene chiamato in modo esplicito nel codice di esempio.  
  
-   Per scorrere un tipo <xref:System.Xml.Schema.XmlSchemaSet>, è necessario usare la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  
  
 Di seguito è riportato l'esempio di codice obsoleto del tipo <xref:System.Xml.Schema.XmlSchemaCollection>.  
  
```vb  
Dim schemaCollection As XmlSchemaCollection = New XmlSchemaCollection()  
schemaCollection.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaCollection.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema in schemaCollection  
  
   Console.WriteLine(schema.TargetNamespace)  
  
Next  
```  
  
```csharp  
XmlSchemaCollection schemaCollection = new XmlSchemaCollection();  
schemaCollection.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaCollection.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
  
foreach(XmlSchema schema in schemaCollection)  
{  
   Console.WriteLine(schema.TargetNamespace);  
}  
```  
  
 Di seguito è riportato l'esempio di codice equivalente del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Compile()  
  
Dim schema As XmlSchema  
  
For Each schema in schemaSet.Schemas()  
  
   Console.WriteLine(schema.TargetNamespace)  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Compile();  
  
foreach(XmlSchema schema in schemaSet.Schemas())  
{  
   Console.WriteLine(schema.TargetNamespace);  
}  
```  
  
## Aggiunta e recupero di schemi  
 Gli schemi vengono aggiunti a un tipo <xref:System.Xml.Schema.XmlSchemaSet> mediante il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Quando viene aggiunto a un tipo <xref:System.Xml.Schema.XmlSchemaSet>, uno schema viene associato a un URI dello spazio dei nomi di destinazione.  L'URI dello spazio dei nomi può essere specificato sia come parametro per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> oppure, se non viene specificato alcuno spazio dei nomi, il tipo <xref:System.Xml.Schema.XmlSchemaSet> usa lo spazio dei nomi definito nello schema.  
  
 Gli schemi vengono recuperati da un tipo <xref:System.Xml.Schema.XmlSchemaSet> mediante la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  La proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> consente di scorrere gli oggetti <xref:System.Xml.Schema.XmlSchema> contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet>.  La proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> restituisce tutti gli oggetti <xref:System.Xml.Schema.XmlSchema> contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet> oppure, se viene fornito un parametro per lo spazio dei nomi di destinazione, restituisce tutti gli oggetti <xref:System.Xml.Schema.XmlSchema> che appartengono allo spazio dei nomi di destinazione.  Se è specificato `null` come parametro per lo spazio dei nomi di destinazione, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> restituisce tutti gli schemi privi di uno spazio dei nomi.  
  
 Nell'esempio seguente viene aggiunto lo schema `books.xsd` dello spazio dei nomi `http://www.contoso.com/books` a un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vengono recuperati tutti gli schemi appartenenti allo spazio dei nomi `http://www.contoso.com/books` dal tipo <xref:System.Xml.Schema.XmlSchemaSet>, quindi vengono scritti tali schemi nel tipo <xref:System.Console>.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet  
schemaSet.Add("http://www.contoso.com/books", "books.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema In schemaSet.Schemas("http://www.contoso.com/books")  
  
   schema.Write(Console.Out)  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/books", "books.xsd");  
  
foreach (XmlSchema schema in schemaSet.Schemas("http://www.contoso.com/books"))  
{  
   schema.Write(Console.Out);  
}  
```  
  
 Per altre informazioni sull'aggiunta e sul recupero di schemi da un oggetto <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> e per la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>.  
  
## Compilazione di schemi  
 Gli schemi di un tipo <xref:System.Xml.Schema.XmlSchemaSet> vengono compilati in un singolo schema logico dal metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  
  
> [!NOTE]
>  A differenza della classe obsoleta <xref:System.Xml.Schema.XmlSchemaCollection>, gli schemi non vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>.  
  
 Se il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> viene eseguito correttamente, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> viene impostata su `true`.  
  
> [!NOTE]
>  La proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> non viene influenzata se si apportano modifiche agli schemi contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Non viene tenuta traccia degli aggiornamenti dei singoli schemi del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Di conseguenza, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> può essere `true` anche se viene modificato uno degli schemi contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet>, a condizione che non venga aggiunto o rimosso alcuno schema dal tipo <xref:System.Xml.Schema.XmlSchemaSet>.  
  
 Nell'esempio seguente viene aggiunto il file `books.xsd` al tipo <xref:System.Xml.Schema.XmlSchemaSet>, quindi viene chiamato il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/books", "books.xsd")  
schemaSet.Compile()  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/books", "books.xsd");  
schemaSet.Compile();  
```  
  
 Per altre informazioni sulla compilazione di schemi di un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>.  
  
## Rielaborazione di schemi  
 Nella rielaborazione di uno schema di un tipo <xref:System.Xml.Schema.XmlSchemaSet> vengono eseguiti tutti i passaggi di pre\-elaborazione eseguiti su uno schema quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Se la chiamata al metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> viene eseguita correttamente, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> viene impostata su `false`.  
  
 È necessario usare il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> quando uno schema del tipo <xref:System.Xml.Schema.XmlSchemaSet> è stato modificato dopo la compilazione del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  
  
 Nel seguente esempio viene illustrata la rielaborazione di uno schema aggiunto al tipo <xref:System.Xml.Schema.XmlSchemaSet> mediante il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>.  Dopo aver compilato il tipo <xref:System.Xml.Schema.XmlSchemaSet> usando il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> e dopo aver modificato lo schema aggiunto al tipo <xref:System.Xml.Schema.XmlSchemaSet>, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> viene impostata su `true` benché sia stato modificato uno schema del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Se si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> verranno eseguiti tutti i passaggi di pre\-elaborazione eseguiti dal metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> e la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> verrà impostata su `false`.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
Dim schema As XmlSchema = schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Compile()  
  
Dim element As XmlSchemaElement = New XmlSchemaElement()  
schema.Items.Add(element)  
element.Name = "book"  
element.SchemaTypeName = New XmlQualifiedName("string", "http://www.w3.org/2001/XMLSchema")  
  
schemaSet.Reprocess(schema)  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
XmlSchema schema = schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Compile();  
  
XmlSchemaElement element = new XmlSchemaElement();  
schema.Items.Add(element);  
element.Name = "book";  
element.SchemaTypeName = new XmlQualifiedName("string", "http://www.w3.org/2001/XMLSchema");  
  
schemaSet.Reprocess(schema);  
```  
  
 Per altre informazioni sulla rielaborazione di uno schema di un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>.  
  
## Verifica di uno schema  
 È possibile usare il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> per verificare se uno schema è contenuto in un tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Per eseguire la verifica, il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> accetta uno spazio dei nomi di destinazione oppure un oggetto <xref:System.Xml.Schema.XmlSchema>.  In entrambi i casi, il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> restituisce `true` se lo schema è contenuto in un tipo <xref:System.Xml.Schema.XmlSchemaSet>; in caso contrario, restituisce `false`.  
  
 Per altre informazioni sulla verifica di uno schema, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A>.  
  
## Rimozione di schemi  
 Gli schemi vengono rimossi da un tipo <xref:System.Xml.Schema.XmlSchemaSet> usando i metodi <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> e <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Il metodo <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> consente di rimuovere dal tipo <xref:System.Xml.Schema.XmlSchemaSet> lo schema specificato, mentre il metodo <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> consente di rimuovere dal tipo <xref:System.Xml.Schema.XmlSchemaSet> lo schema specificato e tutti gli schemi da esso importati.  
  
 Nell'esempio seguente viene illustrata l'aggiunta di schemi a un tipo <xref:System.Xml.Schema.XmlSchemaSet> e l'uso del metodo <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> per rimuovere uno degli schemi e tutti gli schemi da esso importati.  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Add("http://www.contoso.com/music", "http://www.contoso.com/music.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema In schemaSet.Schemas()  
  
   If schema.TargetNamespace = "http://www.contoso.com/music" Then  
      schemaSet.RemoveRecursive(schema)  
   End If  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Add("http://www.contoso.com/music", "http://www.contoso.com/music.xsd");  
  
foreach (XmlSchema schema in schemaSet.Schemas())  
{  
   if (schema.TargetNamespace == "http://www.contoso.com/music")  
   {  
      schemaSet.RemoveRecursive(schema);  
   }  
}  
```  
  
 Per altre informazioni sulla rimozione di schemi da un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per i metodi <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> e <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A>.  
  
## Risoluzione di schemi e xs:import  
 Nei seguenti esempi viene descritto il comportamento del tipo <xref:System.Xml.Schema.XmlSchemaSet> per l'importazione di schemi quando sono presenti più schemi per un determinato spazio dei nomi in <xref:System.Xml.Schema.XmlSchemaSet>.  
  
 Ad esempio, si consideri un tipo <xref:System.Xml.Schema.XmlSchemaSet> che contenga più schemi per lo spazio dei nomi `http://www.contoso.com`.  Verrà aggiunto al tipo <xref:System.Xml.Schema.XmlSchemaSet> uno schema con la seguente direttiva `xs:import`.  
  
```  
<xs:import namespace="http://www.contoso.com" schemaLocation="http://www.contoso.com/schema.xsd" />  
```  
  
 Il tipo <xref:System.Xml.Schema.XmlSchemaSet> tenterà di importare uno schema per lo spazio dei nomi `http://www.contoso.com` caricandolo dall'URL `http://www.contoso.com/schema.xsd`.  Nello schema di importazione sono disponibili solo la dichiarazione dello schema e i tipi dichiarati nel documento dello schema, anche se sono presenti altri documenti dello schema per lo spazio dei nomi `http://www.contoso.com` nel tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Se non è possibile individuare il file `schema.xsd` nell'URL `http://www.contoso.com/schema.xsd`, non verrà importato alcuno schema per lo spazio dei nomi `http://www.contoso.com`.  
  
## Convalida di documenti XML  
 I documenti XML possono essere convalidati in base agli schemi di un tipo <xref:System.Xml.Schema.XmlSchemaSet>.  Per eseguire la convalida di un documento XML, è necessario aggiungere uno schema alla proprietà <xref:System.Xml.XmlReaderSettings.Schemas%2A> di un oggetto <xref:System.Xml.XmlReaderSettings> del tipo <xref:System.Xml.Schema.XmlSchemaSet> oppure aggiungere un tipo <xref:System.Xml.Schema.XmlSchemaSet> alla proprietà <xref:System.Xml.XmlReaderSettings.Schemas%2A> di un oggetto <xref:System.Xml.XmlReaderSettings>.  Quindi l'oggetto <xref:System.Xml.XmlReaderSettings> verrà usato dal metodo <xref:System.Xml.XmlReader.Create%2A> della classe <xref:System.Xml.XmlReader> per creare un oggetto <xref:System.Xml.XmlReader> e convalidare il documento XML.  
  
 Per altre informazioni sulla convalida di documenti XML usando un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere [Convalida dello schema XML \(XSD\) con XmlSchemaSet](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemaset.md).  
  
## Vedere anche  
 <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>   
 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>   
 <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A>   
 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>   
 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>   
 <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A>   
 <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A>   
 [XmlSchemaSet as a Schema Cache](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)   
 [Convalida dello schema XML \(XSD\) con XmlSchemaSet](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemaset.md)