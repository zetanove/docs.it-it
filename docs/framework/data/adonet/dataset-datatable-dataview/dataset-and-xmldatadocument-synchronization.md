---
title: "Sincronizzazione di DataSet e XmlDataDocument | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0ce3793d-54b2-47e4-8cf7-b0591cc4dd21
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Sincronizzazione di DataSet e XmlDataDocument
Il tipo <xref:System.Data.DataSet> di ADO.NET fornisce una rappresentazione relazionale dei dati.  Per un accesso gerarchico ai dati, è possibile usare le classi XML disponibili in .NET Framework.  Questi due tipi di rappresentazione dei dati sono sempre stati usati separatamente.  .NET Framework consente tuttavia l'accesso sincrono, in tempo reale sia alla rappresentazione relazionale che alla rappresentazione gerarchica dei dati mediante, rispettivamente, l'oggetto **DataSet** e l'oggetto <xref:System.Xml.XmlDataDocument>.  
  
 Quando un **DataSet** viene sincronizzato con un **XmlDataDocument**, entrambi gli oggetti usano un unico set di dati.  Se viene apportata una modifica al **DataSet**, tale modifica verrà quindi riflessa nell'oggetto **XmlDataDocument** e viceversa.  La relazione tra **DataSet** e **XmlDataDocument** fornisce una notevole flessibilità, consentendo a una singola applicazione, che usa un singolo set di dati, di accedere all'intero gruppo di servizi compilati per l'oggetto **DataSet** \(ad esempio i controlli Web Form e Windows Form e le finestre di progettazione di Visual Studio .NET\), oltre al gruppo di servizi XML, inclusi XSL \(Extensible Stylesheet Language\), XSLT \(XSL Transformation\) e XPath \(XML Path Language\).  Non è necessario stabilire il set di servizi a cui è destinata l'applicazione poiché sono entrambi disponibili.  
  
 Per sincronizzare un **DataSet** e un oggetto **XmlDataDocument** sono disponibili numerose modalità.  È possibile:  
  
-   Compilare un **DataSet** con uno schema \(ovvero una struttura relazionale\) e con dati, quindi sincronizzarlo con un nuovo oggetto **XmlDataDocument**.  In questo modo si otterrà una visualizzazione gerarchica dei dati relazionali esistenti.  Ad esempio:  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema and data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema and data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    ```  
  
-   Compilare un **DataSet** solo con lo schema \(come nel caso di un **DataSet** tipizzato in modo sicuro\), sincronizzarlo con un oggetto **XmlDataDocument**, quindi caricare l'oggetto **XmlDataDocument** da un documento XML.  In questo modo si otterrà una visualizzazione relazionale dei dati gerarchici esistenti.  È necessario che i nomi di tabella e di colonna presenti nello schema del **DataSet** corrispondano ai nomi degli elementi XML con cui si desidera che siano sincronizzati.  Questo tipo di associazione rileva la differenza tra maiuscole e minuscole.  
  
     Notare che è necessario che nello schema del **DataSet** siano presenti corrispondenze solo agli elementi XML che si desidera esporre nella visualizzazione relazionale.  È quindi possibile disporre di un documento XML di grandi dimensioni e di una "finestra" relazionale molto piccola su tale documento.  Nell'oggetto **XmlDataDocument** viene conservato l'intero documento XML, anche se solo una piccola parte di tale documento viene esposta dal **DataSet**.  Per un esempio dettagliato, vedere [Sincronizzazione di un DataSet con un XmlDataDocument](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/synchronizing-a-dataset-with-an-xmldatadocument.md).  
  
     Nell'esempio di codice seguente vengono illustrati i passaggi per la creazione di un **DataSet**, la compilazione del relativo schema e la sincronizzazione con un **XmlDataDocument**.  Notare che è necessario che nello schema del **DataSet** siano presenti corrispondenze solo agli elementi del **XmlDataDocument** che si desidera esporre mediante il **DataSet**.  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema, but not data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema, but not data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
     Non è possibile caricare un **XmlDataDocument** se tale oggetto è sincronizzato con un **DataSet** contenente dati.  Se si tenta di eseguire tale operazione, verrà generata un'eccezione.  
  
-   Creare un nuovo **XmlDataDocument** e caricarlo da un documento XML, quindi accedere alla visualizzazione relazionale dei dati mediante la proprietà **DataSet** dell'oggetto **XmlDataDocument**.  Prima di visualizzare i dati dell'oggetto **XmlDataDocument** tramite **DataSet**, è necessario impostare lo schema del **DataSet**.  Anche in questo caso è necessario che i nomi di tabella e di colonna presenti nello schema del **DataSet** corrispondano ai nomi degli elementi XML con cui si desidera che siano sincronizzati.  Questo tipo di associazione rileva la differenza tra maiuscole e minuscole.  
  
     Nell'esempio di codice seguente viene illustrata la modalità di accesso alla visualizzazione relazionale dei dati in un oggetto **XmlDataDocument**.  
  
    ```vb  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument  
    Dim dataSet As DataSet = xmlDoc.DataSet  
  
    ' Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml")  
  
    ```  
  
    ```csharp  
    XmlDataDocument xmlDoc = new XmlDataDocument();  
    DataSet dataSet = xmlDoc.DataSet;  
  
    // Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
 Un ulteriore vantaggio della sincronizzazione di un oggetto **XmlDataDocument** con un **DataSet** è che tale procedura consente di conservare la fedeltà al documento XML.  Se il **DataSet** viene compilato da un documento XML usando **ReadXml**, quando i dati vengono riscritti come documento XML usando **WriteXml**, è possibile che il risultato presenti differenze notevoli rispetto al documento XML originale.  Il **DataSet** infatti non conserva la formattazione, ad esempio gli spazi vuoti o le informazioni gerarchiche, quale l'ordine degli elementi, del documento XML.  Il **DataSet**, inoltre, non contiene gli elementi del documento XML che sono stati ignorati in quanto non corrispondenti allo schema del **Dataset**.  La sincronizzazione di un oggetto **XmlDataDocument** con un **DataSet** consente di conservare la formattazione e la struttura gerarchica degli elementi del documento XML originale nell'oggetto **XmlDataDocument**, mentre il **DataSet** contiene solo i dati e le informazioni appropriate per il **DataSet**.  
  
 Quando si sincronizza un oggetto **DataSet** con un oggetto **XmlDataDocument**, si possono ottenere risultati differenti a seconda dell'annidamento o meno degli oggetti <xref:System.Data.DataRelation>.  Per altre informazioni, vedere [DataRelation annidati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md).  
  
## In questa sezione  
 [Sincronizzazione di un DataSet con un XmlDataDocument](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/synchronizing-a-dataset-with-an-xmldatadocument.md)  
 Viene illustrata la sincronizzazione di un **DataSet** tipizzato in modo sicuro, con uno schema minimo, con un **XmlDataDocument**.  
  
 [Esecuzione di una query XPath in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/performing-an-xpath-query-on-a-dataset.md)  
 Viene illustrata l'esecuzione di una query XPath nel contenuto di un **DataSet**.  
  
 [Applicazione di una trasformazione XSLT a un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/applying-an-xslt-transform-to-a-dataset.md)  
 Viene illustrata l'applicazione di una trasformazione XSLT nel contenuto di un **DataSet**.  
  
## Sezioni correlate  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 Viene descritta l'interazione del **DataSet** con XML come origine dati, inclusi il caricamento e la conservazione del contenuto di un **DataSet** sotto forma di dati XML.  
  
 [DataRelation annidati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)  
 Viene illustrata l'importanza degli oggetti **DataRelation** annidati per la rappresentazione del contenuto di un **DataSet** sotto forma di dati XML e viene descritto come creare queste relazioni.  
  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 Viene descritto il **DataSet** e come usarlo per la gestione dei dati dell'applicazione e per l'interazione con origini dati che includono database relazionali e XML.  
  
 [XmlDataDocument, classe](frlrfSystemXmlXmlDataDocumentClassTopic)  
 Vengono fornite informazioni di riferimento relative alla classe **XmlDataDocument**.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)