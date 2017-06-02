---
title: "DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataView
Un oggetto <xref:System.Data.DataView> consente di creare diverse visualizzazioni dei dati archiviati in un oggetto <xref:System.Data.DataTable>. Questa funzionalità è usata spesso nelle applicazioni di associazione dati.  Tramite un **DataView** è possibile esporre i dati di una tabella applicando diversi tipi di ordinamento e filtrare i dati per stato di riga o sulla base di un'espressione di filtro.  
  
 Un oggetto **DataView** fornisce una visualizzazione dinamica dei dati nell'oggetto **DataTable** sottostante: il contenuto, l'ordinamento e l'appartenenza riflettono le modifiche non appena vengono apportate.  Questo comportamento è diverso da quello del metodo **Select** dell'oggetto **DataTable** che restituisce una matrice <xref:System.Data.DataRow> da una tabella in base a un filtro e\/o un ordinamento specifici: ilcontenuto riflette le modifiche apportate alla tabella sottostante, ma l'appartenenza e l'ordinamento restano statici.  Le caratteristiche dinamiche del **DataView** lo rendono ideale per applicazioni di associazione dati.  
  
 Tramite un **DataView** è possibile ottenere una visualizzazione dinamica di un singolo set di dati, in modo simile a una visualizzazione di database, a cui è possibile applicare diversi criteri di ordinamento e di filtro.  A differenza di una visualizzazione di database, tuttavia, un **DataView** non può essere considerato come una tabella e non fornisce una visualizzazione di tabelle unite.  Inoltre, non è possibile escludere colonne presenti nella tabella di origine, né aggiungere colonne, quali le colonne computazionali, che non sono presenti nella tabella di origine.  
  
 È possibile usare una proprietà <xref:System.Data.DataView.DataViewManager%2A> per gestire le impostazioni di visualizzazione per tutte le tabelle di un **DataSet**.  Il **DataViewManager** facilita la gestione delle impostazioni di visualizzazione predefinite per ogni tabella.  Quando si associa un controllo a più di una tabella di un **DataSet**, la soluzione ideale è costituita dall'associazione a un **DataViewManager**.  
  
## In questa sezione  
 [Creazione di un DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-dataview.md)  
 Viene descritta la creazione di un **DataView** per una **DataTable**.  
  
 [Ordinamento e filtro dei dati](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)  
 Viene descritto come impostare le proprietà di un **DataView** per restituire subset di righe di dati che soddisfino criteri di filtro specifici o per restituire i dati in una sequenza di ordinamento particolare.  
  
 [DataRows e DataRowViews](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datarows-and-datarowviews.md)  
 Viene descritto come accedere ai dati esposti dal **DataView**.  
  
 [Ricerca di righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)  
 Viene descritto come trovare una determinata riga in un **DataView**.  
  
 [ChildViews e relazioni](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/childviews-and-relations.md)  
 Viene descritto come creare visualizzazioni di dati da una relazione padre\-figlio mediante un **DataView**.  
  
 [Modifica di DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/modifying-dataviews.md)  
 Viene descritto come modificare i dati nell'oggetto **DataTable** sottostante tramite l'oggetto **DataView**, inclusa l'abilitazione o la disabilitazione degli aggiornamenti.  
  
 [Gestione degli eventi di DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataview-events.md)  
 Viene descritto l'uso dell'evento **ListChanged** per ricevere notifiche in caso di aggiornamento del contenuto o dell'ordinamento di un **DataView**.  
  
 [Gestione di DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/managing-dataviews.md)  
 Viene descritto l'uso di **DataViewManager** per la gestione delle impostazioni del **DataView** per ciascuna tabella nel **DataSet**.  
  
## Sezioni correlate  
 [ASP.NET Web Applications](http://msdn.microsoft.com/it-it/a812d7b7-049e-4234-a4c2-6acf690301f6)  
 Vengono fornite informazioni generali e procedure passo passo dettagliate per la creazione di applicazioni, Web Form e servizi Web ASP.NET.  
  
 [Windows Applications](http://msdn.microsoft.com/it-it/a6bb2180-09b1-4738-b9fd-7fb05fc92f23)  
 Vengono fornite informazioni dettagliate sull'utilizzo di Windows Form e di applicazioni console.  
  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 Viene descritto l'oggetto **DataSet** e come usarlo per la gestione dei dati dell'applicazione.  
  
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)  
 Viene descritto l'oggetto **DataTable** e come usarlo per la gestione dei dati dell'applicazione da solo o come parte di un **DataSet**.  
  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)  
 Vengono descritti l'architettura e i componenti di ADO.NET e come usare ADO.NET per l'accesso alle origini dati esistenti e per la gestione dei dati dell'applicazione.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)