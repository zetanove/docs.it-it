---
title: "Ordinamento e filtro dei dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Ordinamento e filtro dei dati
In <xref:System.Data.DataView> sono disponibili diversi metodi di ordinamento e applicazione di filtri ai dati in una <xref:System.Data.DataTable>:  
  
-   La proprietà <xref:System.Data.DataView.Sort%2A> viene usata per specificare criteri di ordinamento basati su una o più colonne e includere i parametri ASC \(ascendente\) e DESC \(discendente\).  
  
-   La proprietà <xref:System.Data.DataView.ApplyDefaultSort%2A> consente di creare automaticamente un criterio di ordinamento ascendente, basato sulla colonna o sulle colonne di chiave primaria della tabella.  La proprietà <xref:System.Data.DataView.ApplyDefaultSort%2A> viene applicata solo se la proprietà **Sort** è un riferimento null o una stringa vuota e quando nella tabella è stata definita una chiave primaria.  
  
-   La proprietà <xref:System.Data.DataView.RowFilter%2A> consente di specificare subset di righe sulla base dei relativi valori di colonna.  Per informazioni dettagliate sulle espressioni valide per la proprietà **RowFilter**, vedere le informazioni di riferimento per la proprietà <xref:System.Data.DataColumn.Expression%2A> della classe <xref:System.Data.DataColumn>.  
  
     Per restituire i risultati di una particolare query sui dati anziché fornire una visualizzazione dinamica di un subset di dati, si consiglia di usare i metodi <xref:System.Data.DataView.Find%2A> o <xref:System.Data.DataView.FindRows%2A> di **DataView** invece di impostare la proprietà **RowFilter**, se si desidera ottenere prestazioni ottimali.  L'impostazione della proprietà **RowFilter** provoca una ricompilazione dell'indice dei dati, aggiungendo un sovraccarico all'applicazione e riducendo le prestazioni.  L'utilizzo della proprietà **RowFilter** è consigliato in applicazioni con associazioni a dati, in cui i risultati filtrati vengono visualizzati da un controllo associato.  I metodi **Find** e **FindRows** si avvalgono dell'indice corrente, senza che sia necessario ricompilarlo.  Per altre informazioni sui metodi **Find** e **FindRows**, vedere [Ricerca di righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md).  
  
-   La proprietà <xref:System.Data.DataView.RowStateFilter%2A> consente di specificare le versioni di riga da visualizzare.  Le versioni di riga da esporre vengono gestite implicitamente dal **DataView** sulla base del **RowState** della riga sottostante.  Se ad esempio **RowStateFilter** è impostato su **DataViewRowState.Deleted**, il **DataView** esporrà la versione di riga **Original** di tutte le righe **Deleted**, poiché non è disponibile alcuna versione di riga **Current**.  La proprietà **RowVersion** di **DataRowView** consente di determinare la versione di riga di una riga esposta.  
  
     Nella tabella seguente vengono mostrate le opzioni disponibili per **DataViewRowState**.  
  
    |Opzioni di DataViewRowState|Descrizione|  
    |---------------------------------|-----------------|  
    |**CurrentRows**|La versione di riga **Current** di tutte le righe **Unchanged**, **Added** e **Modified**.  Questa è l'impostazione predefinita.|  
    |**Added**|La versione di riga **Current** di tutte le righe **Added**.|  
    |**Eliminato**|La versione di riga **Original** di tutte le righe **Deleted**.|  
    |**ModifiedCurrent**|La versione di riga **Current** di tutte le righe **Modified**.|  
    |**ModifiedOriginal**|La versione di riga **Original** di tutte le righe **Modified**.|  
    |**None**|Nessuna riga.|  
    |**OriginalRows**|La versione di riga **Original** di tutte le righe **Unchanged**, **Modified** e **Deleted**.|  
    |**Unchanged**|La versione di riga **Current** di tutte le righe **Unchanged**.|  
  
 Per altre informazioni sugli stati e sulle versioni delle righe, vedere [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  
  
 Nell'esempio di codice seguente viene creata una visualizzazione in cui vengono mostrati tutti i prodotti il cui numero di unità disponibili in magazzino è inferiore o uguale al livello di riordinamento. I prodotti vengono ordinati prima in base all'identificatore del fornitore, quindi in base al nome del prodotto.  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## Vedere anche  
 <xref:System.Data.DataViewRowState>   
 <xref:System.Data.DataColumn.Expression%2A?displayProperty=fullName>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)