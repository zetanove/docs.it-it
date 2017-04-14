---
title: "Eliminazione di DataRow | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c34f531d-4b9b-4071-b2d7-342c402aa586
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Eliminazione di DataRow
È possibile usare due metodi per eliminare un oggetto <xref:System.Data.DataRow> da un oggetto <xref:System.Data.DataTable>: il metodo **Remove** dell'oggetto <xref:System.Data.DataRowCollection> e il metodo <xref:System.Data.DataRow.Delete%2A> dell'oggetto **DataRow**.  Il metodo <xref:System.Data.DataRowCollection.Remove%2A> consente di eliminare un **DataRow** da **DataRowCollection**, mentre il metodo <xref:System.Data.DataRow.Delete%2A> consente solo di contrassegnare la riga per l'eliminazione.  La rimozione effettiva si verifica nel momento in cui il metodo **AcceptChanges** viene chiamato dall'applicazione.  L'utilizzo di <xref:System.Data.DataRow.Delete%2A> consente di verificare a livello di programmazione le righe contrassegnate per l'eliminazione prima che vengano eliminate effettivamente.  Quando una riga è contrassegnata per l'eliminazione, la relativa proprietà <xref:System.Data.DataRow.RowState%2A> è impostata su <xref:System.Data.DataRow.Delete%2A>.  
  
 <xref:System.Data.DataRow.Delete%2A> e <xref:System.Data.DataRowCollection.Remove%2A> non devono essere chiamato in un ciclo foreach durante l'iterazione tramite un oggetto <xref:System.Data.DataRowCollection>.  <xref:System.Data.DataRow.Delete%2A> e <xref:System.Data.DataRowCollection.Remove%2A> non modificano lo stato della raccolta.  
  
 Quando si usa un <xref:System.Data.DataSet> o una **DataTable** insieme a un **DataAdapter** e a un'origine dati relazionale, usare il metodo **Delete** di **DataRow** per rimuovere la riga.  Il metodo **Delete** consente di contrassegnare la riga come **Deleted** nel **DataSet** o nella **DataTable**, ma la riga non viene rimossa.  Quando la riga contrassegnata come **Deleted** viene rilevata dal **DataAdapter**, viene eseguito il metodo **DeleteCommand** per eliminare tale riga nell'origine dati.  Sarà quindi possibile rimuovere la riga in modo definitivo mediante il metodo **AcceptChanges**.  Se si usa **Remove** per eliminare la riga, tale riga verrà rimossa completamente dalla tabella, ma non verrà eliminata nell'origine dati dal **DataAdapter**.  
  
 Il metodo **Remove** di **DataRowCollection** accetta **DataRow** come argomento e ne consente l'eliminazione dalla raccolta, come mostrato nell'esempio seguente.  
  
```vb  
workTable.Rows.Remove(workRow)  
  
```  
  
```csharp  
workTable.Rows.Remove(workRow);  
```  
  
 Nell'esempio seguente viene invece illustrato come effettuare la chiamata al metodo **Delete** in un **DataRow** per modificare il valore relativo a **RowState** e impostarlo su **Deleted**.  
  
```vb  
workRow.Delete  
  
```  
  
```csharp  
workRow.Delete();  
```  
  
 Se una riga è contrassegnata per l'eliminazione e si chiama il metodo **AcceptChanges** dell'oggetto **DataTable**, tale riga verrà rimossa dalla **DataTable**.  Se invece si chiama **RejectChanges**, il valore relativo al **RowState** della riga verrà impostato di nuovo sul valore che presentava prima di essere contrassegnato come **Deleted**.  
  
> [!NOTE]
>  Se il valore per **RowState** di un **DataRow** è **Added**, ovvero se la riga è stata appena aggiunta alla tabella ed è stata quindi contrassegnata come **Deleted**, tale riga verrà eliminata dalla tabella.  
  
## Vedere anche  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataRowCollection>   
 <xref:System.Data.DataTable>   
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)