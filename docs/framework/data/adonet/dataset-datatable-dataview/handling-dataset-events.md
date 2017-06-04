---
title: "Gestione di eventi dataset | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54edefe0-bc38-419b-b486-3d8a0c356f13
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Gestione di eventi dataset
L'oggetto <xref:System.Data.DataSet> fornisce tre eventi: <xref:System.ComponentModel.MarshalByValueComponent.Disposed>, <xref:System.Data.DataSet.Initialized> e <xref:System.Data.DataSet.MergeFailed>.  
  
## Evento MergeFailed  
 L'evento dell'oggetto `DataSet` usato più di frequente è `MergeFailed`, che viene generato quando gli schemi degli oggetti `DataSet` sono in conflitto. Questo problema si verifica quando gli oggetti <xref:System.Data.DataRow> di origine e di destinazione presentano lo stesso valore di chiave primaria e la proprietà <xref:System.Data.DataSet.EnforceConstraints%2A> è impostata su `true`. Se ad esempio le colonne relative alla chiave primaria di una tabella da unire sono uguali tra le tabelle dei due oggetti `DataSet`, si verifica un'eccezione e viene generato un evento `MergeFailed`. L'oggetto <xref:System.Data.MergeFailedEventArgs> passato all'evento `MergeFailed` include una proprietà <xref:System.Data.MergeFailedEventArgs.Conflict%2A> che identifica il conflitto di schema tra i due oggetti `DataSet` e una proprietà <xref:System.Data.MergeFailedEventArgs.Table%2A> che identifica il nome della tabella in conflitto.  
  
 Nel frammento di codice riportato di seguito viene illustrato come aggiungere un gestore per l'evento `MergeFailed`.  
  
```vb  
AddHandler workDS.MergeFailed, New MergeFailedEventHandler( _  
  AddressOf DataSetMergeFailed)  
  
Private Shared Sub DataSetMergeFailed(  _  
  sender As Object,args As MergeFailedEventArgs)  
  Console.WriteLine("Merge failed for table " & args.Table.TableName)  
  Console.WriteLine("Conflict = " & args.Conflict)  
End Sub  
  
```  
  
```csharp  
workDS.MergeFailed += new MergeFailedEventHandler(DataSetMergeFailed);  
  
private static void DataSetMergeFailed(  
  object sender, MergeFailedEventArgs args)  
{  
  Console.WriteLine("Merge failed for table " + args.Table.TableName);  
  Console.WriteLine("Conflict = " + args.Conflict);  
}  
```  
  
## Evento Initialized  
 L'evento <xref:System.Data.DataSet.Initialized> viene generato dopo che il costruttore di `DataSet` inizializza una nuova istanza del `DataSet`.  
  
 La proprietà <xref:System.Data.DataSet.IsInitialized%2A> restituisce `true` se l'inizializzazione del `DataSet` è stata completata; in caso contrario, restituisce `false`. Il metodo <xref:System.Data.DataSet.BeginInit%2A>, che avvia l'inizializzazione di un `DataSet`, imposta <xref:System.Data.DataSet.IsInitialized%2A> su `false`. Il metodo <xref:System.Data.DataSet.EndInit%2A>, che termina l'inizializzazione del `DataSet`, lo imposta su `true`. Questi metodi vengono usati nell'ambiente di progettazione di [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] per inizializzare un `DataSet` usato da un altro componente. Non vengono comunemente usati nel codice.  
  
## Evento Disposed  
 `DataSet` è derivato dalla classe <xref:System.ComponentModel.MarshalByValueComponent>, che espone il metodo <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> e l'evento <xref:System.ComponentModel.MarshalByValueComponent.Disposed>. L'evento <xref:System.ComponentModel.MarshalByValueComponent.Disposed> aggiunge un gestore eventi per restare in attesa dell'evento eliminato sul componente. È possibile usare l'evento <xref:System.ComponentModel.MarshalByValueComponent.Disposed> di un oggetto `DataSet` se si vuole eseguire il codice quando viene chiamato il metodo <xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A>.<xref:System.ComponentModel.MarshalByValueComponent.Dispose%2A> rilascia le risorse usate da <xref:System.ComponentModel.MarshalByValueComponent>.  
  
> [!NOTE]
>  Gli oggetti `DataSet` e `DataTable` ereditano da <xref:System.ComponentModel.MarshalByValueComponent> e supportano l'interfaccia <xref:System.Runtime.Serialization.ISerializable> per l'esecuzione in remoto. Si tratta degli unici oggetti ADO.NET che è possibile eseguire in remoto. Per altre informazioni, vedere [Remote Objects](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58).  
  
 Per informazioni sugli altri eventi disponibili quando si usa un `DataSet`, vedere [Gestione degli eventi di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md) e [Gestione degli eventi di DataAdapter](../../../../../docs/framework/data/adonet/handling-dataadapter-events.md).  
  
## Vedere anche  
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Convalida dei dati](../Topic/Validating%20Data.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)