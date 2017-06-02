---
title: "Caricamento di un DataSet da XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49c083b7-a5ed-41cf-aabc-5aaba96f00e6
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Caricamento di un DataSet da XML
È possibile creare il contenuto di un <xref:System.Data.DataSet> di ADO.NET da un flusso o un documento XML.  Inoltre, .NET Framework consente di definire con grande flessibilità le informazioni da caricare da XML e la modalità di creazione dello schema o struttura relazionale del <xref:System.Data.DataSet>.  
  
 Per compilare un <xref:System.Data.DataSet> con dati provenienti da XML, usare il metodo **ReadXml** dell'oggetto <xref:System.Data.DataSet>.  Il metodo **ReadXml** consente di leggere un file, un flusso o un **XmlReader** e accetta come argomenti l'origine del documento XML, oltre a un argomento **XmlReadMode** facoltativo.  Per altre informazioni su **XmlReader**, vedere [NIB: Reading XML Data with XmlTextReader](http://msdn.microsoft.com/it-it/762c069b-b50c-41b8-936e-39eacfb0d540). Il metodo **ReadXml** consente di leggere il contenuto del flusso o del documento XML e di caricare tali dati nel <xref:System.Data.DataSet>.  Tale metodo consente inoltre la creazione dello schema relazionale del <xref:System.Data.DataSet> in base all'argomento **XmlReadMode** specificato e all'eventuale esistenza di uno schema relazionale.  
  
 Nella tabella seguente vengono illustrate le opzioni disponibili per l'argomento **XmlReadMode**.  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**Auto**|Questa è l'impostazione predefinita.  Consente di esaminare il documento o flusso XML e di selezionare l'opzione più appropriata, nel seguente ordine:<br /><br /> -   Se il documento o flusso XML è in formato DiffGram, viene usato **DiffGram**.<br />-   Se nel <xref:System.Data.DataSet> è presente uno schema o nel documento o flusso XML è presente uno schema inline, viene usato **ReadSchema**.<br />-   Se nel <xref:System.Data.DataSet> non è presente alcuno schema o nel documento o flusso XML non è presente alcuno schema inline, viene usato **InferSchema**.<br /><br /> Se si dispone di informazioni sul formato del documento o flusso XML letto, per ottimizzare le prestazioni si consiglia di impostare un **XmlReadMode** esplicito, anziché usare l'impostazione predefinita **Auto**.|  
|**ReadSchema**|Consente di leggere gli schemi inline e di caricare i dati e lo schema.<br /><br /> Se nel <xref:System.Data.DataSet> è già presente uno schema, vengono aggiunte nuove tabelle dallo schema inline allo schema esistente nel <xref:System.Data.DataSet>.  Se nel <xref:System.Data.DataSet> sono già presenti delle tabelle dello schema inline, viene generata un'eccezione.  Non sarà possibile modificare lo schema di una tabella esistente usando **XmlReadMode.ReadSchema**.<br /><br /> Se nel <xref:System.Data.DataSet> non è presente uno schema e non si dispone di uno schema inline, non verrà letto alcun dato.<br /><br /> È possibile definire lo schema inline usando lo schema XSD \(XML Schema Definition Language\).  Per altre informazioni sulla scrittura di uno schema inline come XML Schema, vedere [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md).|  
|**IgnoreSchema**|Consente di ignorare eventuali schemi inline e di caricare i dati nello schema del <xref:System.Data.DataSet> esistente.  Eventuali dati non corrispondenti allo schema esistente vengono eliminati.  Se nel <xref:System.Data.DataSet> non è presente alcuno schema, non verrà caricato alcun dato.<br /><br /> Se i dati sono di tipo DiffGram, **IgnoreSchema** avrà la stessa funzionalità di **DiffGram** *.*|  
|**InferSchema**|Consente di ignorare eventuali schemi inline e di inferire uno schema in base alla struttura dei dati XML, che vengono quindi caricati.<br /><br /> Se nell'oggetto <xref:System.Data.DataSet> è già contenuto uno schema, lo schema corrente verrà esteso mediante l'aggiunta di colonne alle tabelle esistenti.  Se non sono disponibili tabelle esistenti, non verranno aggiunte altre tabelle.  Se esiste già una tabella inferita con uno spazio dei nomi diverso o se alcune colonne inferite è in conflitto con le colonne esistenti, verrà generata un'eccezione.<br /><br /> Per altre informazioni su come **ReadXmlSchema** inferisce uno schema da un documento XML, vedere [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md).|  
|**DiffGram**|Consente di leggere un DiffGram e di aggiungere i dati allo schema corrente.  Tramite **DiffGram** nuove righe vengono unite a righe esistenti in caso di corrispondenza dei valori dell'identificatore univoco.  Vedere la nota relativa a "Unione di dati da XML" alla fine di questo argomento.  Per altre informazioni sui Diffgram, vedere [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md).|  
|**Fragment**|Consente di continuare a leggere più frammenti XML fino al raggiungimento della fine del flusso.  I frammenti corrispondenti allo schema del <xref:System.Data.DataSet> vengono aggiunti alle tabelle appropriate.  I frammenti non corrispondenti allo schema <xref:System.Data.DataSet> vengono eliminati.|  
  
> [!NOTE]
>  Se si passa un **XmlReader** a un **ReadXml** posizionato in un punto di un documento XML, **ReadXml** leggerà il nodo successivo dell'elemento e lo considererà come elemento radice, leggendo solo fino alla fine del nodo dell'elemento.  Questo comportamento non si verifica se si specifica **XmlReadMode.Fragment**.  
  
## Entità DTD  
 Se nel documento XML sono presenti entità definite in uno schema DTD \(Document Type Definition\), verrà generata un'eccezione nel caso in cui si tenti di caricare un <xref:System.Data.DataSet> passando un nome file, un flusso o un **XmlReader** non di convalida a **ReadXml**.  È invece necessario creare un **XmlValidatingReader**, con **EntityHandling** impostato su **EntityHandling.ExpandEntities** e passare tale **XmlValidatingReader** a **ReadXml**.  Le entità verranno espanse da **XmlValidatingReader** prima di essere lette dal <xref:System.Data.DataSet>.  
  
 Negli esempi di codice seguenti viene illustrato come caricare un <xref:System.Data.DataSet> da un flusso XML.  Nel primo esempio viene mostrato il passaggio di un nome file al metodo **ReadXml**.  Nel secondo esempio viene mostrato il caricamento di una stringa contenente XML tramite <xref:System.IO.StringReader>.  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema);  
```  
  
```vb  
Dim dataSet As DataSet = New DataSet  
Dim dataTable As DataTable = New DataTable("table1")  
dataTable.Columns.Add("col1", Type.GetType("System.String"))  
dataSet.Tables.Add(dataTable)  
  
Dim xmlData As String = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>"  
  
Dim xmlSR As System.IO.StringReader = New System.IO.StringReader(xmlData)  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
DataTable dataTable = new DataTable("table1");  
dataTable.Columns.Add("col1", typeof(string));  
dataSet.Tables.Add(dataTable);  
  
string xmlData = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>";  
  
System.IO.StringReader xmlSR = new System.IO.StringReader(xmlData);  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema);  
```  
  
> [!NOTE]
>  Se si chiama **ReadXml** per caricare un file di grandi dimensioni, può verificarsi una riduzione delle prestazioni.  Per ottenere prestazioni ottimali quando si usa **ReadXml** con file di grandi dimensioni, chiamare il metodo <xref:System.Data.DataTable.BeginLoadData%2A> per ciascuna tabella del <xref:System.Data.DataSet>, quindi chiamare **ReadXml**.  Chiamare infine <xref:System.Data.DataTable.EndLoadData%2A> per ogni tabella del <xref:System.Data.DataSet>, come indicato nell'esempio seguente.  
  
```vb  
Dim dataTable As DataTable  
  
For Each dataTable In dataSet.Tables  
   dataTable.BeginLoadData()  
Next  
  
dataSet.ReadXml("file.xml")  
  
For Each dataTable in dataSet.Tables  
   dataTable.EndLoadData()  
Next  
```  
  
```csharp  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.BeginLoadData();  
  
dataSet.ReadXml("file.xml");   
  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.EndLoadData();  
```  
  
> [!NOTE]
>  Se lo schema XSD per il <xref:System.Data.DataSet> include un **targetNamespace**, è possibile che i dati non vengano letti e che vengano generate eccezioni quando si chiama il metodo **ReadXml** per caricare il <xref:System.Data.DataSet> con XML contenente elementi senza uno spazio dei nomi qualificativo.  In questo caso, per leggere elementi non qualificati, impostare **elementFormDefault** su "qualified" nello schema XSD.  Ad esempio:  
  
```  
<xsd:schema id="customDataSet"   
  elementFormDefault="qualified"  
  targetNamespace="http://www.tempuri.org/customDataSet.xsd"   
  xmlns="http://www.tempuri.org/customDataSet.xsd"   
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
  xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
</xsd:schema>  
```  
  
## Unione di dati da XML  
 Se nell'oggetto <xref:System.Data.DataSet> sono già presenti dati, i nuovi dati provenienti dal flusso o dal documento XML vengono aggiunti ai dati presenti nell'oggetto <xref:System.Data.DataSet>.  Eventuali informazioni sulla riga con chiavi primarie corrispondenti presenti nel flusso o documento XML non vengono unite da **ReadXml** nel <xref:System.Data.DataSet>.  Per sovrascrivere le informazioni sulla riga esistenti con le nuove informazioni provenienti da XML, usare **ReadXml** per creare un nuovo <xref:System.Data.DataSet>, quindi il metodo <xref:System.Data.DataSet.Merge%2A> per unire il nuovo <xref:System.Data.DataSet> al <xref:System.Data.DataSet> esistente.  Notare che il caricamento di un DiffGram tramite **ReadXML** con **XmlReadMode** pari a **DiffGram** consentirà di unire righe a cui è associato lo stesso identificatore univoco.  
  
## Vedere anche  
 <xref:System.Data.DataSet.Merge%2A?displayProperty=fullName>   
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)   
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)   
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento delle informazioni relative allo schema di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)