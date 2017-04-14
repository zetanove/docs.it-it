---
title: "DiffGram | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 037f3991-7bbc-424b-b52e-8b03585d3e34
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DiffGram
DiffGram è un formato XML che consente di identificare le versioni correnti e originali degli elementi di dati.  Il formato DiffGram viene usato dal tipo <xref:System.Data.DataSet> per caricare e conservare il contenuto e per serializzare tale contenuto in modo da consentirne il trasporto tramite una connessione di rete.  Quando un tipo <xref:System.Data.DataSet> viene scritto in formato DiffGram, tale DiffGram viene compilato con tutte le informazioni necessarie per ricreare accuratamente il contenuto, ma non lo schema, del tipo <xref:System.Data.DataSet>, inclusi i valori di colonna per le versioni di riga **Original** e **Current**, le informazioni relative agli errori delle righe e l'ordine delle righe.  
  
 Quando si invia e si recupera un tipo <xref:System.Data.DataSet> da un servizio Web XML, il formato DiffGram viene usato implicitamente.  Inoltre, quando si carica il contenuto di un oggetto <xref:System.Data.DataSet> da XML usando il metodo **ReadXml** o quando si scrive il contenuto di un oggetto <xref:System.Data.DataSet> in XML usando il metodo **WriteXml**, è possibile specificare che il contenuto deve essere letto o scritto come DiffGram.  Per altre informazioni, vedere [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md) e [Scrittura del contenuto di DataSet come dati XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md).  
  
 Benché il formato DiffGram venga usato principalmente da .NET Framework come formato di serializzazione per il contenuto di un tipo <xref:System.Data.DataSet>, è possibile usare i DiffGram per modificare i dati delle tabelle di un database Microsoft SQL Server.  
  
 Un Diffgram viene generato scrivendo il contenuto di tutte le tabelle in un elemento **\<diffgram\>**.  
  
### Per generare un Diffgram  
  
1.  Generare un elenco di tabelle radice, ovvero senza elementi padre.  
  
2.  Per ogni tabella e per i relativi discendenti nell'elenco, scrivere la versione corrente di tutte le righe nella prima sezione del Diffgram.  
  
3.  Per ogni tabella in <xref:System.Data.DataSet>, scrivere la versione originale di tutte le righe, se disponibile, nella sezione **\<before\>** del Diffgram.  
  
4.  Per le righe che contengono errori, scrivere il contenuto dell'errore nella sezione **\<errors\>** del Diffgram.  
  
 Un Diffgram viene elaborato nell'ordine a partire dal file XML fino alla fine.  
  
### Per elaborare un Diffgram  
  
1.  Elaborare la prima sezione del Diffgram che contiene la versione corrente delle righe.  
  
2.  Elaborare la seconda sezione, ovvero**\<before\>**, che contiene la versione originale delle righe modificate ed eliminate.  
  
    > [!NOTE]
    >  Se una riga è contrassegnata come eliminata, con l'operazione di eliminazione è possibile che vengano rimossi anche i relativi discendenti, a seconda della proprietà `Cascade` dell'oggetto <xref:System.Data.DataSet> corrente.  
  
3.  Elaborare la sezione **\<errors\>**.  Impostare le informazioni sull'errore per la riga e la colonna specificate per ogni elemento di questa sezione.  
  
> [!NOTE]
>  Se si imposta <xref:System.Data.XmlWriteMode> su Diffgram, il contenuto dell'oggetto <xref:System.Data.DataSet> di destinazione può essere diverso da quello dell'oggetto <xref:System.Data.DataSet> originale.  
  
## Formato DiffGram  
 Il formato DiffGram è suddiviso in tre sezioni: i dati correnti, i dati originali \(o "precedenti"\) e una sezione relativa agli errori, come illustrato nell'esempio seguente.  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  
   <DataInstance>  
   </DataInstance>  
  
  <diffgr:before>  
  </diffgr:before>  
  
  <diffgr:errors>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
 Il formato DiffGram è costituito dai seguenti blocchi di dati:  
  
 **\<**  ***DataInstance***  **\>**  
 Il nome di questo elemento, ***DataInstance***, viene usato a scopo esplicativo nella presente documentazione.  Un elemento ***DataInstance*** rappresenta un tipo <xref:System.Data.DataSet> o una riga di un tipo <xref:System.Data.DataTable>.  Il termine *DataInstance* viene sostituito nell'elemento dal nome del tipo <xref:System.Data.DataSet> o <xref:System.Data.DataTable>.  In questo blocco del formato DiffGram sono contenuti i dati correnti, indipendentemente dalle eventuali modifiche a tali dati.  L'annotazione **diffgr:hasChanges** consente di identificare un elemento o una riga a cui sono state apportate modifiche.  
  
 **\<diffgr:before\>**  
 In questo blocco del formato DiffGram è contenuta la versione originale di una riga.  Gli elementi di questo blocco corrispondono agli elementi del blocco ***DataInstance*** mediante l'annotazione **diffgr:id** .  
  
 **\<diffgr:errors\>**  
 In questo blocco del formato DiffGram sono contenute informazioni relative agli errori per una particolare riga del blocco ***DataInstance***.  Gli elementi di questo blocco corrispondono agli elementi del blocco ***DataInstance*** mediante l'annotazione **diffgr:id** .  
  
## Annotazioni DiffGram  
 I DiffGram usano diverse annotazioni per correlare elementi presenti nei vari blocchi di DiffGram, che rappresentano diverse versioni di riga o informazioni relative agli errori nel tipo <xref:System.Data.DataSet>.  
  
 La tabella seguente descrive le annotazioni DiffGram definite nello spazio dei nomi DiffGram **urn:schemas\-microsoft\-com:xml\-diffgram\-v1**.  
  
|Annotazione|Descrizione|  
|-----------------|-----------------|  
|**id**|Consente di accoppiare gli elementi presenti nei blocchi **\<diffgr:before\>** e **\<diffgr:errors\>** e gli elementi presenti nel blocco **\<** ***DataInstance*** **\>**.  Per i valori dell'annotazione **diffgr:id** viene usato il seguente formato: *\[NomeTabella\]\[IdentificatoreRiga\]*.  Ad esempio: `<Customers diffgr:id="Customers1">`.|  
|**parentId**|Identifica l'elemento padre dell'elemento corrente nel blocco **\<** ***DataInstance*** **\>**.  Per i valori dell'annotazione **diffgr:parentId** viene usato il seguente formato: *\[NomeTabella\]\[IdentificatoreRiga\]*.  Ad esempio: `<Orders diffgr:parentId="Customers1">`.|  
|**hasChanges**|Identifica come modificata una riga del blocco **\<** ***DataInstance*** **\>**.  Per l'annotazione **hasChanges** viene usato uno dei due valori seguenti:<br /><br /> **inserted**<br /> Identifica una riga **Added**.<br /><br /> **modified**<br /> Identifica una riga **Modified** contenente una versione di riga **Original** nel blocco **\<diffgr:before\>**.  Si noti che alle righe **Deleted** viene associata una versione di riga **Original** nel blocco **\<diffgr:before\>**, ma nel blocco **\<** ***DataInstance*** **\>** non è presente alcun elemento annotato.|  
|**hasErrors**|Identifica una riga nel blocco **\<** ***DataInstance*** **\>** con un **RowError**.  L'elemento di errore viene inserito nel blocco **\<diffgr:errors\>**.|  
|**Errore**|In questa annotazione è contenuto il testo del **RowError** per un particolare elemento del blocco **\<diffgr:errors\>**.|  
  
 Quando legge o scrive il proprio contenuto come DiffGram, il tipo <xref:System.Data.DataSet> include ulteriori annotazioni.  La tabella seguente descrive tali annotazioni, definite nello spazio dei nomi **urn:schemas\-microsoft\-com:xml\-msdata**.  
  
|Annotazione|Descrizione|  
|-----------------|-----------------|  
|**RowOrder**|Conserva l'ordine di riga dei dati originali e identifica l'indice di una riga in un particolare tipo <xref:System.Data.DataTable>.|  
|**Hidden**|Identifica una colonna con una proprietà **ColumnMapping** impostata su **MappingType.Hidden**.  L'attributo viene scritto nel formato **msdata:hidden** *\[NomeColonna\]*\="*valore*".  Ad esempio: `<Customers diffgr:id="Customers1" msdata:hiddenContactTitle="Owner">`.<br /><br /> Notare che le colonne nascoste vengono scritte come attributo DiffGram solo se in tali colonne sono presenti dati.  In caso contrario, vengono ignorate.|  
  
## Esempio di DiffGram  
 Di seguito viene riportato un esempio di formato DiffGram.  Questo esempio mostra il risultato di un aggiornamento a una riga prima della conferma delle modifiche.  La riga con CustomerID pari a "ALFKI" è stata modificata, ma non aggiornata.  Una riga **Current** con valore per **diffgr:id** pari a "Customers1" è quindi presente nel blocco **\<** ***DataInstance*** **\>** e una riga **Original** con valore per **diffgr:id** pari a "Customers1" nel blocco **\<diffgr:before\>**.  Nella riga con CustomerID "ANATR" è incluso un **RowError**, quindi nella riga è presente l'annotazione `diffgr:hasErrors="true"` e nel blocco **\<diffgr:errors\>** si trova un elemento correlato.  
  
```  
<diffgr:diffgram xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
  <CustomerDataSet>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0" diffgr:hasChanges="modified">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>New Company</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers2" msdata:rowOrder="1" diffgram:hasErrors="true">  
      <CustomerID>ANATR</CustomerID>  
      <CompanyName>Ana Trujillo Emparedados y Helados</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers3" msdata:rowOrder="2">  
      <CustomerID>ANTON</CustomerID>  
      <CompanyName>Antonio Moreno Taquera</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers4" msdata:rowOrder="3">  
      <CustomerID>AROUT</CustomerID>  
      <CompanyName>Around the Horn</CompanyName>  
    </Customers>  
  </CustomerDataSet>  
  <diffgr:before>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>Alfreds Futterkiste</CompanyName>  
    </Customers>  
  </diffgr:before>  
  <diffgr:errors>  
    <Customers diffgr:id="Customers2" diffgr:Error="An optimistic concurrency violation has occurred for this row."/>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
## Vedere anche  
 [Utilizzo di XML in un DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [Caricamento di un DataSet da XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [Scrittura del contenuto di DataSet come dati XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)