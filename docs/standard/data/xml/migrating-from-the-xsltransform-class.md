---
title: "Migrazione dalla classe XslTransform | Microsoft Docs"
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
ms.assetid: 9404d758-679f-4ffb-995d-3d07d817659e
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Migrazione dalla classe XslTransform
L'architettura XSLT è stata ridisegnata nella versione di [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)].  La classe <xref:System.Xml.Xsl.XslTransform> è stata sostituita dalla classe <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
 Nelle sezioni seguenti vengono descritte alcune delle principali differenze tra <xref:System.Xml.Xsl.XslCompiledTransform> e le classi di <xref:System.Xml.Xsl.XslTransform>.  
  
## Prestazioni  
 La classe <xref:System.Xml.Xsl.XslCompiledTransform> presenta numerosi miglioramenti a livello di prestazioni.  Il nuovo processore XSLT consente di compilare il foglio di stile XSLT in un formato comune intermedio analogamente a ciò che esegue CLR \(Common Language Runtime\) per altri linguaggi di programmazione.  Una volta compilato, il foglio di stile può essere memorizzato nella cache e riusato.  
  
 Inoltre, la classe <xref:System.Xml.Xsl.XslCompiledTransform> include altre ottimizzazioni che rendono molto più veloce la classe <xref:System.Xml.Xsl.XslTransform>.  
  
> [!NOTE]
>  Sebbene le prestazioni complessive della classe <xref:System.Xml.Xsl.XslCompiledTransform> siano migliori rispetto alla classe <xref:System.Xml.Xsl.XslTransform>, l'esecuzione del metodo <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> della classe <xref:System.Xml.Xsl.XslCompiledTransform> potrebbe risultare più lenta di quella del metodo <xref:System.Xml.Xsl.XslTransform.Load%2A> della classe <xref:System.Xml.Xsl.XslTransform> la prima volta che tale metodo viene chiamato su una trasformazione.  Questa situazione si verifica perché il file XSLT deve essere compilato prima del caricamento.  Per altre informazioni, vedere il post di blog seguente: [XslCompiledTransform Slower che XslTransform?](http://go.microsoft.com/fwlink/?LinkId=130590)  
  
## Sicurezza  
 Per impostazione predefinita, la classe <xref:System.Xml.Xsl.XslCompiledTransform> disabilita il supporto per la funzione `document()` di XSLT e per lo script incorporato.  Queste funzionalità possono essere abilitate creando un oggetto <xref:System.Xml.Xsl.XsltSettings> in cui le funzionalità sono abilitate e passandolo al metodo <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A>.  Nell'esempio seguente viene illustrato come abilitare lo scripting ed eseguire una trasformazione XSLT.  
  
 [!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
 [!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]  
  
 Per altre informazioni, vedere [Considerazioni sulla sicurezza XSLT](../../../../docs/standard/data/xml/xslt-security-considerations.md).  
  
## Nuove funzionalità  
  
### File temporanei  
 I file temporanei vengono talvolta generati durante l'elaborazione XSLT.  Se un foglio di stile contiene blocchi di script o se viene compilato con l'impostazione di debug impostata su true, è possibile creare i file temporanei nella cartella %TEMP%.  In alcuni casi è possibile che alcuni file temporanei non vengano eliminati a causa di problemi di temporizzazione.  Ad esempio, se i file vengono usati nell'AppDomain corrente o dal debugger, il finalizzatore dell'oggetto <xref:System.CodeDom.Compiler.TempFileCollection> non sarà in grado di rimuoverli.  
  
 Per assicurarsi che tutti i file temporanei vengano rimossi dal client, è possibile usare la proprietà <xref:System.Xml.Xsl.XslCompiledTransform.TemporaryFiles%2A> per eseguire una pulizia aggiuntiva.  
  
### Supporto per l'elemento xsl:output e XmlWriter  
 La classe <xref:System.Xml.Xsl.XslTransform> ignora le impostazioni `xsl:output` quando l'output della trasformazione viene inviato a un oggetto <xref:System.Xml.XmlWriter>.  Per la classe <xref:System.Xml.Xsl.XslCompiledTransform> è disponibile una proprietà <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A> che restituisce un oggetto <xref:System.Xml.XmlWriterSettings> contenente le informazioni di output derivate dall'elemento `xsl:output` del foglio di stile.  L'oggetto <xref:System.Xml.XmlWriterSettings> viene usato per creare un oggetto <xref:System.Xml.XmlWriter> con le impostazioni corrette che è possibile passare al metodo <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  Nel codice C\# seguente viene illustrato questo comportamento:  
  
```  
// Create the XslTransform object and load the style sheet.  
XslCompiledTransform xslt = new XslCompiledTransform();  
xslt.Load(stylesheet);  
  
// Load the file to transform.  
XPathDocument doc = new XPathDocument(filename);  
  
// Create the writer.  
XmlWriter writer = XmlWriter.Create(Console.Out, xslt.OutputSettings);  
  
// Transform the file and send the output to the console.  
xslt.Transform(doc, writer);  
writer.Close();  
```  
  
### Opzione di debug  
 La classe <xref:System.Xml.Xsl.XslCompiledTransform> è in grado di generare informazioni di debug che consentono di eseguire il debug del foglio di stile con Microsoft [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] Debugger.  Per altre informazioni, vedere <xref:System.Xml.Xsl.XslCompiledTransform.%23ctor%28System.Boolean%29>.  
  
## Differenze di comportamento  
  
### Trasformazione in XmlReader  
 La classe <xref:System.Xml.Xsl.XslTransform> contiene diversi overload Transform che restituiscono informazioni sulle trasformazioni sotto forma di oggetto <xref:System.Xml.XmlReader>.  È possibile usare questi overload per caricare i risultati delle trasformazioni in una rappresentazione in memoria \(ad esempio <xref:System.Xml.XmlDocument> o <xref:System.Xml.XPath.XPathDocument>\) senza rischiare di sovraccaricare la serializzazione e la deserializzazione dell'albero XML risultante.  Nel codice C\# seguente viene illustrato come caricare i risultati delle trasformazioni in un oggetto <xref:System.Xml.XmlDocument>.  
  
```  
// Load the style sheet  
XslTransform xslt = new XslTransform();  
xslt.Load("MyStylesheet.xsl");  
  
// Transform input document to XmlDocument for additional processing  
XmlDocument doc = new XmlDocument();  
doc.Load(xslt.Transform(input, (XsltArgumentList)null));  
```  
  
 La classe <xref:System.Xml.Xsl.XslCompiledTransform> non supporta la trasformazione in un oggetto <xref:System.Xml.XmlReader>.  È tuttavia possibile eseguire la stessa operazione usando il metodo <xref:System.Xml.XPath.XPathNavigator.CreateNavigator%2A> per caricare l'albero XML risultante direttamente da un oggetto <xref:System.Xml.XmlWriter>.  Nel codice C\# seguente viene illustrato come eseguire la stessa attività usando <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
```  
// Transform input document to XmlDocument for additional processing  
XmlDocument doc = new XmlDocument();  
using (XmlWriter writer = doc.CreateNavigator().AppendChild()) {  
    xslt.Transform(input, (XsltArgumentList)null, writer);  
}  
```  
  
### Comportamento discretionary  
 Nella raccomandazione W3C, XSL Transformations \(XSLT\) Version 1.0, sono incluse aree in cui il provider dell'implementazione può decidere come gestire una determinata situazione.  Queste aree si considerano come aree di comportamento discretionary.  Sono numerose le aree in cui <xref:System.Xml.Xsl.XslCompiledTransform> si comporta in modo diverso rispetto alla classe <xref:System.Xml.Xsl.XslTransform>.  Per altre informazioni, vedere [Errori XSLT risolvibili](../../../../docs/standard/data/xml/recoverable-xslt-errors.md).  
  
### Oggetti di estensione e funzioni di script  
 Con <xref:System.Xml.Xsl.XslCompiledTransform> vengono introdotte due nuove restrizioni relative all'utilizzo di funzioni script:  
  
-   Da espressioni XPath è possibile chiamare solo metodi pubblici.  
  
-   Gli overload si distinguono tra loro in base al numero di argomenti.  Se più di un overload presenta lo stesso numero di argomenti, verrà generata un'eccezione.  
  
 In <xref:System.Xml.Xsl.XslCompiledTransform> si verifica un'associazione \(ricerca del nome del metodo\) alle funzioni di script in fase di compilazione e i fogli di stile usati con XslTranform possono generare un'eccezione quando vengono caricati con <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
 Con <xref:System.Xml.Xsl.XslCompiledTransform> sono supportati gli elementi figlio `msxsl:using` e `msxsl:assembly` all'interno dell'elemento `msxsl:script`.  Gli elementi `msxsl:using` e `msxsl:assembly` sono usati per dichiarare spazi dei nomi e assembly aggiuntivi da usare nel blocco di script.  Per altre informazioni, vedere [Blocchi di script utilizzando msxsl:script](../../../../docs/standard/data/xml/script-blocks-using-msxsl-script.md).  
  
 In <xref:System.Xml.Xsl.XslCompiledTransform> sono proibiti gli oggetti di estensione che presentano più overload con lo stesso numero di argomenti.  
  
### Funzioni MSXML  
 Alla classe <xref:System.Xml.Xsl.XslCompiledTransform> è stato aggiunto il supporto per altre funzioni MSXML.  Nell'elenco seguente vengono descritte le funzionalità nuove o migliorate.  
  
-   msxsl:node\-set: con <xref:System.Xml.Xsl.XslTransform> è necessario che l'argomento della funzione [Funzione node\-set](http://msdn.microsoft.com/it-it/87b6b3f4-16f4-4fa3-8103-d62a679ac2a7) sia un frammento dell'albero dei risultati.  Questo requisito non è invece previsto con la classe <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
-   msxsl:version: questa funzione è supportata in <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
-   Funzioni di estensione XPath: sono ora supportate le funzioni [Funzione ms:string\-compare](http://msdn.microsoft.com/it-it/20616b82-9e27-444c-b714-4f1e09b73aee), [Funzione ms:utc](http://msdn.microsoft.com/it-it/ef26fc88-84c6-4fb9-9c3b-f2f5264b864f), [Funzione ms:namespace\-uri](http://msdn.microsoft.com/it-it/91f9cabf-ab93-4dbe-9c12-e6a75214f4c7), [Funzione ms:local\-name](http://msdn.microsoft.com/it-it/10ed60a1-17a9-4d74-8b98-7940ac97c0b5), [Funzione ms:number](http://msdn.microsoft.com/it-it/b94fc08e-1f31-4f48-b1a8-6d78c1b5d954), [Funzione ms:format\-date](http://msdn.microsoft.com/it-it/51f35609-89a9-4098-a166-88bf01300bf5) e [Funzione ms:format\-time](http://msdn.microsoft.com/it-it/e5c2df2d-e8fb-4a8f-bfc0-db84ea12a5d5).  
  
-   Funzioni di estensione XPath correlate allo schema: queste funzioni non sono supportate in modalità nativa da <xref:System.Xml.Xsl.XslCompiledTransform>.  Tuttavia, possono essere implementate come funzioni di estensione.  
  
## Vedere anche  
 [Trasformazioni XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)   
 [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)