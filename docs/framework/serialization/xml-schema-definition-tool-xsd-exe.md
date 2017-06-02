---
title: "Strumento XML Schema Definition (Xsd.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6e6e65c-347f-4494-9457-653bf29baac2
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Strumento XML Schema Definition (Xsd.exe)
Lo strumento XML Schema Definition \(Xsd.exe\) consente di generare classi Common Language Runtime o XML Schema da file XDR, XML e XSD o da classi di un assembly di runtime.  
  
## Sintassi  
  
```  
  
xsd file.xdr [/outputdir:directory][/parameters:file.xml]  
xsd file.xml [/outputdir:directory] [/parameters:file.xml]  
xsd file.xsd {/classes | /dataset} [/element:element]   
             [/enableLinqDataSet] [/language:language]   
                          [/namespace:namespace] [/outputdir:directory] [URI:uri]   
                          [/parameters:file.xml]  
xsd {file.dll | file.exe} [/outputdir:directory] [/type:typename [...]][/parameters:file.xml]  
```  
  
## Argomento  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|*file.extension*|Specifica il file di input da convertire.  È necessario specificare un'estensionedi tipo xdr, xml, xsd, dll o exe.<br /><br /> Se si specifica un file di schema XDR \(estensione xrd\), lo schema XRD verrà convertito in uno schema XSD.  Il file di output avrà lo stesso nome dello schema XDR, ma un'estensione xsd.<br /><br /> Se si specifica un file XML \(estensione xml\), verrà dedotto uno schema dai dati del file e prodotto uno schema XSD.  Il file di output avrà lo stesso nome del file XML, ma un'estensione xsd.<br /><br /> Se si specifica un file di XML Schema \(estensione xsd\), verrà generato codice sorgente per gli oggetti di runtime corrispondenti allo schema XML.<br /><br /> Se si specifica un file di assembly di runtime \(estensione EXE o DLL\), verranno generati schemi per uno o più tipi di questo assembly.  È possibile usare l'opzione **\/type** per specificare i tipi per i quali generare schemi.  Gli schemi di output vengono denominati schema0.xsd, schema1.xsd e così via.  In Xsd.exe vengono prodotti più schemi solo se i tipi forniti specificano uno spazio dei nomi con l'attributo personalizzato **XMLRoot**.|  
  
## Opzioni generali  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/h**\[**elp**\]|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**\/o**\[**utputdir**\]**:***directory*|Specifica la directory per i file di output.  Questo argomento può apparire una sola volta.  Il valore predefinito è la directory corrente.|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**\/P\[arameters\]:** *file.xml*|Legge le opzioni per diverse modalità operative dal file con estensione xml specificato.  La forma abbreviata è \/p:.  Per altre informazioni, vedere la sezione Osservazioni successiva.|  
  
## Opzioni per i file XSD  
 È necessario specificare una sola delle opzioni elencate di seguito per i file XSD.  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/c**\[**lasses**\]|Genera classi che corrispondono allo schema specificato.  Per leggere dati XML nell'oggetto, usare il metodo [System.Xml.Serialization.XmlSerializer.Deserializer](frlrfSystemXmlSerializationXmlSerializerClassDeserializeTopic).|  
|**\/d**\[**ataset**\]|Genera una classe derivata da <xref:System.Data.DataSet> che corrisponde allo schema specificato.  Per leggere dati XML nella classe derivata, usare il metodo [System.Data.DataSet.ReadXml](frlrfSystemDataDataSetClassReadXmlTopic).|  
  
 È inoltre possibile specificare una o più opzioni tra quelle riportate di seguito per i file XSD.  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/e**\[**lement**\]**:***element*|Specifica l'elemento dello schema per il quale generare codice.  Per impostazione predefinita, sono specificati tutti gli elementi.  È possibile specificare questo argomento più volte.|  
|**\/enableDataBinding**|Implementa l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> su tutti i tipi generati per consentire l'associazione dati.  La forma abbreviata è **\/edb**.|  
|**\/enableLinqDataSet**|\(forma abbreviata: **\/eld**\). Specifica che il dataset generato può essere sottoposto a query mediante LINQ to DataSet.  Questa opzione viene usata quando è specificata anche l'opzione per i \/dataset .  Per altre informazioni, vedere [Cenni preliminari su LINQ to DataSet](../../../docs/framework/data/adonet/linq-to-dataset-overview.md) e [Esecuzione di query su DataSet tipizzati](../../../docs/framework/data/adonet/querying-typed-datasets.md).  Per informazioni generali sull'utilizzo di LINQ, vedere [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md).|  
|**\/f**\[**ields**\]|Genera campi anziché proprietà.  Per impostazione predefinita, vengono generate le proprietà.|  
|**\/l**\[**anguage**\]**:***language*|Specifica il linguaggio di programmazione da usare.  È possibile scegliere tra **CS** \(C\#, il linguaggio predefinito\), **VB** \(Visual Basic\), **JS** \(JScript\) o **VJS** \(Visual J\#\).  È anche possibile specificare un nome completo per una classe che implementa <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=fullName>|  
|**\/n**\[**amespace**\]**:***namespace*|Specifica lo spazio dei nomi del runtime per i tipi generati.  Lo spazio dei nomi predefinito è **Schemas**.|  
|**\/nologo**|Evita la visualizzazione del messaggio di avvio.|  
|**\/order**|Genera identificatori di ordine espliciti su tutti i membri particella.|  
|**\/o\[ut\]:** *directoryName*|Specifica la directory di output in cui inserire i file.  Il valore predefinito è la directory corrente.|  
|**\/u**\[**ri**\]**:***uri*|Specifica l'URI degli elementi dello schema per il quale generare codice.  Questo URI, se presente, viene applicato a tutti gli elementi specificati con l'opzione **\/element**.|  
  
## Opzioni per i file DLL ed EXE  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/t**\[**ype**\]**:***typename*|Specifica il nome del tipo per il quale creare uno schema.  È possibile specificare più argomenti type.  Se *typename* non specifica alcuno spazio dei nomi, il tipo specificato verrà associato a tutti i tipi dell'assembly.  Se *typename* specifica uno spazio dei nomi, il tipo specificato verrà associato solo a tale tipo.  Se *typename* termina con un asterisco \(\*\), verrà creata un'associazione con tutti i tipi che iniziano con la stringa che precede l'asterisco.  Se si omette l'opzione **\/type**, verranno generati schemi per tutti i tipi dell'assembly.|  
  
## Note  
 Nella tabella riportata di seguito vengono illustrate le operazioni eseguite da Xsd.exe.  
  
 Da XDR a XSD  
 Generare uno schema XML da un file di schema con dati XML ridotti.  XDR è un precedente formato di schema basato su XML.  
  
 Da XML a XSD  
 Generare uno schema XML da un file XML.  
  
 Da XSD a dataset  
 Generare classi <xref:System.Data.DataSet> di Common Language Runtime da un file di schema XSD.  Le classi generate forniscono un modello a oggetti elaborato per i dati XML regolari.  
  
 Da XSD a classi  
 Generare classi di runtime da un file di schema XSD.  Le classi generate possono essere usate con <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> per leggere e scrivere il codice XML basato sullo schema.  
  
 Da classi a XSD  
 Generare uno schema XML da uno o più tipi presenti in un file di assembly di runtime.  Lo schema generato definisce il formato XML usato da **System.Xml.Serialization.XmlSerializer**.  
  
 Xsd.exe consente solo di modificare gli schemi XML che seguono il linguaggio XSD \(XML Schema Definition\) proposto da W3C \(World Wide Web Consortium\).  Per altre informazioni sulla proposta XSD o sullo standard XML, visitare il sito http:\/\/w3.org \(informazioni in lingua inglese\).  
  
## Impostazione delle opzioni con un file XML  
 Mediante l'opzione **\/parameters** è possibile specificare un unico file XML in cui sono impostate diverse opzioni.  Le opzioni che è possibile impostare dipendono dalla modalità di utilizzo dello strumento XSD.exe.  È possibile scegliere di generare schemi, file di codice o file di codice con funzionalità **DataSet**.  Ad esempio, è possibile impostare l'elemento **\<assembly\>** sul nome di un file eseguibile \(.exe\) o di una libreria di tipi \(.dll\) durante la generazione di uno schema, ma non durante la generazione di un file di codice.  Nel codice XML riportato di seguito viene illustrato come usare l'elemento **\<generateSchemas\>** con un determinato file eseguibile:  
  
```  
<!-- This is in a file named GenerateSchemas.xml. -->  
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>  
<generateSchemas>  
   <assembly>ConsoleApplication1.exe</assembly>  
</generateSchemas>  
</xsd>  
```  
  
 Se il codice XML riportato sopra è contenuto in un file denominato GenerateSchemas.xml, usare l'opzione **\/parameters** digitando la seguente stringa al prompt dei comandi e premendo INVIO:  
  
 **xsd \/p:GenerateSchemas.xml**  
  
 Se invece si genera uno schema per un singolo tipo trovato nell'assembly, è possibile usare il codice XML riportato di seguito:  
  
```  
<!-- This is in a file named GenerateSchemaFromType.xml. -->  
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>  
<generateSchemas>  
   <type>IDItems</type>  
</generateSchemas>  
</xsd>  
```  
  
 Per usare il codice riportato sopra è necessario specificare anche il nome dell'assembly al prompt dei comandi.  Se il file XML è denominato GenerateSchemaFromType.xml, digitare la seguente stringa:  
  
 **xsd \/p:GenerateSchemaFromType.xml ConsoleApplication1.exe**  
  
 Per l'elemento **\<generateSchemas\>** è necessario specificare solo una delle seguenti opzioni.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<assembly\>|Specifica un assembly dal quale generare lo schema.|  
|\<type\>|Specifica un tipo trovato in un assembly per il quale generare uno schema.|  
|\<xml\>|Specifica un file XML per il quale generare uno schema.|  
|\<xdr\>|Specifica un file XDR per il quale generare uno schema.|  
  
 Per generare un file di codice, usare l'elemento **\<generateClasses\>**.  Nell'esempio riportato di seguito viene generato un file di codice.  Sono presenti anche due attributi che consentono di impostare il linguaggio di programmazione e lo spazio dei nomi del file generato.  
  
```  
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>  
<generateClasses language='VB' namespace='Microsoft.Serialization.Examples'/>  
</xsd>  
<!-- You must supply an .xsd file when typing in the command line.-->  
<!-- For example: xsd /p:genClasses mySchema.xsd -->  
```  
  
 Per l'elemento **\<generateClasses\>** è possibile impostare le seguenti opzioni.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<element\>|Specifica un elemento nel file XSD per il quale generare codice.|  
|\<schemaImporterExtensions\>|Specifica un tipo derivato dalla classe <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension>.|  
|\<schema\>|Specifica un file di XML Schema per il quale generare un codice.  Possono essere specificati più file di XML Schema usando più elementi di \<schema\>.|  
  
 Nella tabella riportata di seguito sono descritti gli attributi che è possibile usare con l'elemento **\<generateClasses\>**.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|linguaggio|Specifica il linguaggio di programmazione da usare.  È possibile scegliere tra **CS** \(C\#, il linguaggio predefinito\), **VB** \(Visual Basic\), **JS** \(JScript\) o **VJS** \(Visual J\#\).  È anche possibile specificare un nome completo per una classe che implementa <xref:System.CodeDom.Compiler.CodeDomProvider>.|  
|namespace|Specifica lo spazio dei nomi per il codice generato.  Lo spazio dei nomi deve essere conforme agli standard CLR, ad esempio non devono essere presenti spazi o barre rovesciate.|  
|Opzioni|Uno dei seguenti valori: **none**, **properties** \(genera proprietà anziché campi pubblici\), **order** o **enableDataBinding**. Per informazioni, vedere le opzioni **\/order** e **\/enableDataBinding** nella sezioni precedente "Opzioni per i file XSD".|  
  
 È anche possibile controllare la modalità di generazione del codice **DataSet** usando l'elemento **\<generateDataSets\>**.  Nel codice XML seguente viene specificato che il codice generato ``  usa strutture **DataSet**, ad esempio la classe <xref:System.Data.DataTable>, per creare codice Visual Basic per un elemento specifico.  Le strutture di DataSet generate supporteranno le query LINQ.  
  
 `\<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>`  
  
 `<generateDataSet language='VB' namespace='Microsoft.Serialization.Examples' enableLinqDataSet='true'>`  
  
 `</generateDataSet>`  
  
 `</xsd>`  
  
 Per l'elemento **\<generateDataSet\>** è possibile impostare le seguenti opzioni.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<schema\>|Specifica un file di XML Schema per il quale generare un codice.  Possono essere specificati più file di XML Schema usando più elementi di \<schema\>.|  
  
 Nella tabella riportata di seguito sono descritti gli attributi che è possibile usare con l'elemento **\<generateDataSet\>**.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enableLinqDataSet|Specifica che il dataset generato può essere sottoposto a query mediante LINQ to DataSet.  Il valore predefinito è false.|  
|linguaggio|Specifica il linguaggio di programmazione da usare.  È possibile scegliere tra **CS** \(C\#, il linguaggio predefinito\), **VB** \(Visual Basic\), **JS** \(JScript\) o **VJS** \(Visual J\#\).  È anche possibile specificare un nome completo per una classe che implementa <xref:System.CodeDom.Compiler.CodeDomProvider>.|  
|spazio dei nomi|Specifica lo spazio dei nomi per il codice generato.  Lo spazio dei nomi deve essere conforme agli standard CLR, ad esempio non devono essere presenti spazi o barre rovesciate.|  
  
 Alcuni attributi possono essere impostati sull'elemento **\<xsd\>** di livello più alto.  È possibile usare queste opzioni con uno qualsiasi degli elementi figlio \(**\<generateSchemas\>**,**\<generateClasses\>** o **\<generateDataSet\>**\).  Nell'esempio di codice XML riportato di seguito viene generato codice per un elemento denominato IDItems nella directory di output MyOutputDirectory.  
  
```  
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/' output='MyOutputDirectory'>  
<generateClasses>  
<element>IDItems</element>  
</generateClasses>  
</xsd>  
```  
  
 Nella tabella riportata di seguito sono descritti gli attributi che è possibile usare con l'elemento **\<xsd\>**.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|output|Nome della directory in cui verrà inserito lo schema o il file di codice generato.|  
|\/nologo|Evita la visualizzazione del messaggio di avvio.  Impostare su **true** o **false**.|  
|guida|Visualizza la sintassi e le opzioni di comando dello strumento.  Impostare su **true** o **false**.|  
  
```  
  
```  
  
## Esempi  
 Il comando che segue genera uno schema XML da `myFile.xdr` e lo salva nella directory corrente.  
  
```  
xsd myFile.xdr   
```  
  
 Il comando che segue genera uno schema XML da `myFile.xml` e lo salva nella directory specificata.  
  
```  
xsd myFile.xml /outputdir:myOutputDir  
```  
  
 Il comando che segue genera un set di dati che corrisponde allo schema specificato nel linguaggio C\# e lo salva con il nome `XSDSchemaFile.cs` nella directory corrente.  
  
```  
xsd /dataset /language:CS XSDSchemaFile.xsd  
```  
  
 Il comando che segue genera schemi XML per tutti i tipi dell'assembly `myAssembly.dll` e li salva con il nome `schema0.xsd` nella directory corrente.  
  
```  
xsd myAssembly.dll    
```  
  
## Vedere anche  
 <xref:System.Data.DataSet>   
 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>   
 [Tools](../../../docs/framework/tools/index.md)   
 [System.Xml.Serialization.XmlSerializer.Deserializer](frlrfSystemXmlSerializationXmlSerializerClassDeserializeTopic)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)   
 [Cenni preliminari su LINQ to DataSet](../../../docs/framework/data/adonet/linq-to-dataset-overview.md)   
 [Esecuzione di query su DataSet tipizzati](../../../docs/framework/data/adonet/querying-typed-datasets.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)