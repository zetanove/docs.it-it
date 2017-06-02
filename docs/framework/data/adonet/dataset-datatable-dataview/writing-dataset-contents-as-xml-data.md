---
title: "Scrittura del contenuto di dataset come dati XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Scrittura del contenuto di dataset come dati XML
In ADO.NET è possibile scrivere una rappresentazione XML di un <xref:System.Data.DataSet>, con o senza il relativo schema. Se le informazioni relative allo schema sono incluse inline con il flusso o documento XML, tali informazioni verranno scritte usando il linguaggio XSD (XML Schema Definition Language). Lo schema contiene le definizioni delle tabelle di <xref:System.Data.DataSet> oltre alle definizioni delle relazioni e dei vincoli.  
  
 Quando un <xref:System.Data.DataSet> viene scritto come dati XML, le righe di <xref:System.Data.DataSet> vengono scritte le versioni correnti. Tuttavia, il <xref:System.Data.DataSet> può anche essere scritto come DiffGram, in modo che sia corrente e i valori originali delle righe sarà inclusi.  
  
 La rappresentazione XML del <xref:System.Data.DataSet> possono essere scritti in un file, un flusso, un **XmlWriter**, o una stringa. Queste opzioni forniscono una notevole flessibilità per la modalità di trasporto della rappresentazione XML di <xref:System.Data.DataSet>. Per ottenere una rappresentazione XML di <xref:System.Data.DataSet> sotto forma di stringa, utilizzare il **GetXml** metodo come illustrato nell'esempio seguente.  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml** restituisce la rappresentazione XML del <xref:System.Data.DataSet> senza informazioni sullo schema. Per scrivere le informazioni sullo schema di <xref:System.Data.DataSet> (come XML Schema) a una stringa, usare **GetXmlSchema**.  
  
 Per scrivere un <xref:System.Data.DataSet> in un file di flusso, o **XmlWriter**, utilizzare il **WriteXml** metodo. Il primo parametro passato a **WriteXml** rappresenta la destinazione dell'output XML. Ad esempio, passare una stringa contenente un nome file, un **System.IO.TextWriter** oggetto e così via. È possibile passare un secondo parametro facoltativo di un **XmlWriteMode** per specificare come deve essere scritto l'output XML.  
  
 Nella tabella seguente vengono illustrate le opzioni per **XmlWriteMode**.  
  
|Opzione XmlWriteMode|Descrizione|  
|-------------------------|-----------------|  
|**IgnoreSchema**|Scrive il contenuto corrente del <xref:System.Data.DataSet> come dati XML, senza uno Schema XML. Questa è l'impostazione predefinita.|  
|**WriteSchema**|Scrive il contenuto corrente del <xref:System.Data.DataSet> come dati XML con la struttura relazionale come XML Schema inline.|  
|**DiffGram**|Scrive l'intero <xref:System.Data.DataSet> come DiffGram, inclusi i valori originali e correnti. Per ulteriori informazioni, vedere [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md).|  
  
 Quando si scrive una rappresentazione XML di un <xref:System.Data.DataSet> contenente **DataRelation** oggetti, è probabile che si desideri il XML risultante siano presenti le righe figlio di ogni relazione annidata all'interno dei relativi elementi padre. A tale scopo, impostare il **Nested** proprietà del **DataRelation** a **true** quando si aggiunge il **DataRelation** per il <xref:System.Data.DataSet>. Per ulteriori informazioni, vedere [la nidificazione di oggetti DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md).  
  
 Di seguito sono riportati due esempi di scrittura della rappresentazione XML di un <xref:System.Data.DataSet> in un file. Nel primo esempio passa il nome del file per il codice XML risulta come una stringa a **WriteXml**. Il secondo esempio viene passato un **System.IO.StreamWriter** oggetto.  
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>Mapping di colonne a elementi, attributi e testo XML  
 È possibile specificare come una colonna di una tabella è rappresentata in formato XML utilizzando il **ColumnMapping** proprietà del **DataColumn** oggetto. Nella tabella seguente sono riportati i diversi **MappingType** i valori per il **ColumnMapping** proprietà di una colonna di tabella e il codice XML risultante.  
  
|Valore MappingType|Descrizione|  
|-----------------------|-----------------|  
|**Elemento**|Questa è l'impostazione predefinita. La colonna viene scritta sotto forma di elemento XML. ColumnName rappresenta il nome dell'elemento e i contenuti della colonna vengono scritti come testo dell'elemento. Ad esempio:<br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**Attributo**|La colonna viene scritta sotto forma di attributo XML dell'elemento XML per la riga corrente. ColumnName rappresenta il nome dell'attributo e i contenuti della colonna vengono scritti sotto forma di valore dell'attributo. Ad esempio:<br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|I contenuti della colonna vengono scritti sotto forma di testo nell'elemento XML per la riga corrente. Ad esempio:<br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> Si noti che **SimpleContent** non può essere impostata per una colonna di una tabella con **elemento** colonne o relazioni annidate.|  
|**Nascosto**|La colonna non viene scritta nell'output XML.|  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di XML in un set di dati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)   
 [Annidamento di oggetti DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)   
 [Scrittura di informazioni dello Schema di DataSet come XSD](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)