---
title: "Caricamento delle informazioni relative allo schema di un DataSet da XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 43dfb23b-5cef-46f2-8d87-78f0fba1eb8c
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Caricamento delle informazioni relative allo schema di un DataSet da XML
È possibile definire a livello di programmazione lo schema di un <xref:System.Data.DataSet> \(le tabelle, le colonne, le relazioni e i vincoli\), creare tale schema mediante i metodi **Fill** o **FillSchema** di un <xref:System.Data.Common.DataAdapter> oppure caricarlo da un documento XML.  Per caricare informazioni relative allo schema di un **DataSet** da un documento XML, è possibile usare il metodo **ReadXmlSchema** o il metodo **InferXmlSchema** del **DataSet**.  Il metodo **ReadXmlSchema** consente di caricare o inferire le informazioni relative allo schema del **DataSet** dal documento contenente lo schema XSD \(XML Schema Definition Language\) o da un documento XML con XML Schema inline.  Il metodo **InferXmlSchema** consente di inferire lo schema dal documento XML, ignorando allo stesso tempo determinati spazi dei nomi XML specificati dall'utente.  
  
> [!NOTE]
>  L'ordine delle tabelle in un **DataSet** potrebbe non essere mantenuto quando si usano i servizi Web o la serializzazione XML per trasferire un **DataSet** creato in memoria usando costrutti XSD \(ad esempio relazioni annidate\).  Pertanto, il destinatario del **DataSet** non deve dipendere dall'ordine delle tabelle in questo caso.  Tuttavia, l'ordine delle tabelle viene sempre mantenuto se lo schema del **DataSet** da trasferire è stato letto da file XSD anziché essere creato in memoria.  
  
## ReadXmlSchema  
 Per caricare lo schema di un **DataSet** da un documento XML senza caricare alcun dato, è possibile usare il metodo **ReadXmlSchema** del **DataSet**.  Tale metodo consente di creare uno schema di **DataSet** definito tramite lo schema XSD \(XML Schema Definition Language\).  
  
 Il metodo **ReadXmlSchema** accetta come unico argomento un nome file, un flusso o un **XmlReader** contenente il documento XML da caricare.  È possibile che nel documento XML sia contenuto solo lo schema, oppure che in tale documento sia contenuto lo schema inline con elementi XML contenenti dati.  Per altre informazioni sulla scrittura di uno schema inline come XML Schema, vedere [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md).  
  
 Se nel documento XML passato a **ReadXmlSchema** non sono contenute informazioni relative allo schema inline, lo schema viene inferito da **ReadXmlSchema** sulla base degli elementi presenti nel documento XML.  Se nel **DataSet** è già presente uno schema, lo schema corrente viene esteso tramite l'aggiunta di nuove tabelle, se non sono già esistenti.  Nelle tabelle esistenti non verranno aggiunte nuove colonne.  Se una colonna aggiunta esiste già nel **DataSet** ma il tipo di tale colonna non è compatibile con la colonna rilevata nel documento o flusso XML, verrà generata un'eccezione.  Per altre informazioni su come **ReadXmlSchema** inferisce uno schema da un documento XML, vedere [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md).  
  
 Mentre **ReadXmlSchema** consente di caricare o inferire solo lo schema di un **DataSet**, il metodo **ReadXml** del **DataSet** consente di caricare o inferire sia lo schema che i dati contenuti nel documento XML.  Per altre informazioni, vedere [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md).  
  
 Nell'esempio di codice seguente viene illustrato il caricamento dello schema di un **DataSet** da un documento o flusso XML.  Nel primo esempio viene mostrato il passaggio di un nome file di XML Schema al metodo **ReadXmlSchema**.  Nel secondo esempio viene mostrato un oggetto **System.IO.StreamReader**.  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema("schema.xsd")  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema("schema.xsd");  
```  
  
```vb  
Dim xmlStream As System.IO.StreamReader = New System.IO.StreamReader ("schema.xsd");  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema(xmlStream)  
xmlStream.Close()  
```  
  
```csharp  
System.IO.StreamReader xmlStream = new System.IO.StreamReader("schema.xsd");  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema(xmlStream);  
xmlStream.Close();  
```  
  
## InferXmlSchema  
 È inoltre possibile impostare l'oggetto **DataSet** in modo che lo schema venga dedotto da un documento XML mediante il metodo **InferXmlSchema** di **DataSet**.  L'utilizzo di tale metodo è simile all'utilizzo di **ReadXml** con **XmlReadMode** pari a **InferSchema** \(consente il caricamento dei dati e l'inferenza dello schema\) e di **ReadXmlSchema**, nel caso in cui nel documento letto non sia presente alcuno schema inline.  Tuttavia, il metodo **InferXmlSchema** offre un'ulteriore possibilità, consentendo di specificare dei particolari spazi dei nomi XML da ignorare durante l'inferenza dello schema.  **InferXmlSchema** accetta due argomenti necessari: la posizione del documento XML, specificata da un nome file, un flusso o un oggetto **XmlReader** e una matrice di stringhe degli spazi dei nomi XML che verranno ignorati dall'operazione.  
  
 Ad esempio, si consideri il seguente codice XML:  
  
```  
<NewDataSet xmlns:od="urn:schemas-microsoft-com:officedata">  
<Categories>  
  <CategoryID od:adotype="3">1</CategoryID>   
  <CategoryName od:maxLength="15" od:adotype="130">Beverages</CategoryName>   
  <Description od:adotype="203">Soft drinks and teas</Description>   
</Categories>  
<Products>  
  <ProductID od:adotype="20">1</ProductID>   
  <ReorderLevel od:adotype="3">10</ReorderLevel>   
  <Discontinued od:adotype="11">0</Discontinued>   
</Products>  
</NewDataSet>  
```  
  
 A causa degli attributi specificati per gli elementi nel documento XML precedente, il metodo **ReadXmlSchema** e il metodo **ReadXml** con un oggetto **XmlReadMode** di **InferSchema** creeranno tabelle per ogni elemento del documento: **Categories**, **CategoryID**, **CategoryName**, **Description**, **Products**, **ProductID**, **ReorderLevel** e **Discontinued**.  Per altre informazioni, vedere [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md). Una struttura più appropriata implicherebbe tuttavia la creazione delle sole tabelle **Categories** e **Products**, seguita dalla creazione delle colonne **CategoryID**, **CategoryName** e **Description** nella tabella **Categories** e delle colonne **ProductID**, **ReorderLevel** e **Discontinued** nella tabella **Products**.  Per assicurarsi che gli attributi specificati negli elementi XML vengano ignorati dallo schema inferito, usare il metodo **InferXmlSchema** e fare in modo che lo spazio dei nomi XML per **officedata** venga ignorato, come illustrato nell'esempio seguente.  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.InferXmlSchema("input_od.xml", New String() {"urn:schemas-microsoft-com:officedata"})  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.InferXmlSchema("input_od.xml", new string[] "urn:schemas-microsoft-com:officedata");  
```  
  
## Vedere anche  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)   
 [Inferenza della struttura relazionale del DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)