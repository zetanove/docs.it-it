---
title: "Vincoli di DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27c9f2fd-f64d-4b4e-bbf6-1d24f47067cb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Vincoli di DataTable
I vincoli consentono di applicare restrizioni ai dati di una <xref:System.Data.DataTable>, in modo da garantire l'integrità di tali dati.  Un vincolo è una regola automatica applicata a una colonna, o a colonne correlate, che consente di determinare le operazioni da eseguire in caso di modifica del valore di una riga.  I vincoli vengono applicati se la proprietà  `System.Data.DataSet.EnforceConstraints` dell'oggetto <xref:System.Data.DataSet> è impostata su **true**.  Per un esempio di codice che illustra come impostare la proprietà `EnforceConstraints`, vedere l'argomento relativo a <xref:System.Data.DataSet.EnforceConstraints%2A>.  
  
 In ADO.NET sono disponibili due tipi di vincoli: <xref:System.Data.ForeignKeyConstraint> e <xref:System.Data.UniqueConstraint>.  Per impostazione predefinita, entrambi i vincoli vengono creati automaticamente quando si crea una relazione tra due o più tabelle aggiungendo un <xref:System.Data.DataRelation> al **DataSet**.  È tuttavia possibile disabilitare questo comportamento impostando **createConstraints** su **false** quando si crea la relazione.  
  
## ForeignKeyConstraint  
 Un **ForeignKeyConstraint** consente di applicare regole relative alla modalità di propagazione di aggiornamenti ed eliminazioni alle tabelle correlate.  Ad esempio, se un valore di una riga di una tabella viene aggiornato o eliminato e tale valore viene usato anche in una o più tabelle correlate, un vincolo **ForeignKeyConstraint** consentirà di determinare gli effetti di tale modifica sulle tabelle correlate.  
  
 Mediante le proprietà <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> e <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> di **ForeignKeyConstraint** è possibile definire l'operazione da eseguire quando un utente tenta di eliminare o aggiornare una riga in una tabella correlata.  Nella tabella seguente vengono descritte le diverse impostazioni disponibili per le proprietà **DeleteRule** e **UpdateRule** di **ForeignKeyConstraint**.  
  
|Impostazione della regola|Descrizione|  
|-------------------------------|-----------------|  
|**Cascade**|Elimina o aggiorna righe correlate.|  
|**SetNull**|Imposta i valori delle righe correlate su **DBNull**.|  
|**SetDefault**|Imposta i valori delle righe correlate sul valore predefinito.|  
|**None**|Non viene eseguita alcuna operazione sulle righe correlate.  Questa è l'impostazione predefinita.|  
  
 Un vincolo **ForeignKeyConstraint** consente di limitare, oltre che propagare, le modifiche alle colonne correlate.  In base alle proprietà impostate per il vincolo **ForeignKeyConstraint** di una colonna e nel caso in cui la proprietà **EnforceConstraints** del **DataSet** sia impostata su **true**, l'esecuzione di determinate operazioni sulla riga padre provocherà un'eccezione.  Ad esempio, se la proprietà **DeleteRule** del vincolo **ForeignKeyConstraint** è impostata su **None**, non sarà possibile eliminare una riga padre nel caso in cui a tale riga siano associate righe figlio.  
  
 È possibile creare un vincolo di chiave esterna tra singole colonne o tra una matrice di colonne usando il costruttore **ForeignKeyConstraint** e passando l'oggetto **ForeignKeyConstraint** risultante al metodo **Add** della proprietà **Constraints** della tabella, che è un **ConstraintCollection**.  Per creare un **ForeignKeyConstraint**, è inoltre possibile passare argomenti del costruttore a diversi overload del metodo **Add** di un **ConstraintCollection**.  
  
 Quando si crea un vincolo **ForeignKeyConstraint**, è possibile passare i valori **DeleteRule** e **UpdateRule** al costruttore come argomenti o impostare tali valori come proprietà, come illustrato nell'esempio seguente \(dove il valore **DeleteRule** è impostato su **Cascade**\).  
  
```vb  
Dim custOrderFK As ForeignKeyConstraint = New ForeignKeyConstraint("CustOrderFK", _  
  custDS.Tables("CustTable").Columns("CustomerID"), _  
  custDS.Tables("OrdersTable").Columns("CustomerID"))  
custOrderFK.DeleteRule = Rule.None    
' Cannot delete a customer value that has associated existing orders.  
custDS.Tables("OrdersTable").Constraints.Add(custOrderFK)  
  
```  
  
```csharp  
ForeignKeyConstraint custOrderFK = new ForeignKeyConstraint("CustOrderFK",  
  custDS.Tables["CustTable"].Columns["CustomerID"],   
  custDS.Tables["OrdersTable"].Columns["CustomerID"]);  
custOrderFK.DeleteRule = Rule.None;    
// Cannot delete a customer value that has associated existing orders.  
custDS.Tables["OrdersTable"].Constraints.Add(custOrderFK);  
```  
  
### AcceptRejectRule  
 È possibile accettare le modifiche apportate alle righe usando il metodo **AcceptChanges** o annullare tali modifiche usando il metodo **RejectChanges** di **DataSet**, **DataTable** o **DataRow**.  Se in un **DataSet** sono contenuti vincoli **ForeignKeyConstraints**, la chiamata dei metodi **AcceptChanges** o **RejectChanges** provocherà l'applicazione di **AcceptRejectRule**.  La proprietà **AcceptRejectRule** del vincolo **ForeignKeyConstraint** consente di determinare l'operazione da eseguire nelle righe figlio quando il metodo **AcceptChanges** o **RejectChanges** viene chiamato nella riga padre.  
  
 Nella tabella seguente sono elencate le impostazioni disponibili per **AcceptRejectRule**.  
  
|Impostazione della regola|Descrizione|  
|-------------------------------|-----------------|  
|**Cascade**|Consente di accettare o rifiutare le modifiche alle righe figlio.|  
|**None**|Non viene eseguita alcuna operazione sulle righe figlio.  Questa è l'impostazione predefinita.|  
  
### Esempio  
 Nell'esempio seguente viene creato un oggetto <xref:System.Data.ForeignKeyConstraint>, ne vengono impostate alcune proprietà, tra cui <xref:System.Data.ForeignKeyConstraint.AcceptRejectRule%2A>, nonché viene aggiunto all'oggetto <xref:System.Data.ConstraintCollection> di un oggetto <xref:System.Data.DataTable>.  
  
 [!code-csharp[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/CS/source.cs#1)]
 [!code-vb[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/VB/source.vb#1)]  
  
## UniqueConstraint  
 L'oggetto **UniqueConstraint**, che può essere assegnato a una singola colonna o a una matrice di colonne in un oggetto **DataTable**, consente di assicurare che tutti i dati della colonna o delle colonne specificate siano univoci in ogni riga.  È possibile creare un vincolo univoco per una colonna o una matrice di colonne usando il costruttore **UniqueConstraint** e passando l'oggetto **UniqueConstraint** risultante al metodo **Add** della proprietà **Constraints** della tabella, che è un **ConstraintCollection**.  Per creare un **UniqueConstraint**, è inoltre possibile passare argomenti del costruttore a diversi overload del metodo **Add** di un **ConstraintCollection**.  Quando si crea un vincolo **UniqueConstraint** per una o più colonne, è possibile, se lo si desidera, specificare se la colonna o le colonne sono una chiave primaria.  
  
 È anche possibile creare un vincolo univoco per una colonna impostando la proprietà **Unique** della colonna su **true**.  In alternativa, per rimuovere eventuali vincoli univoci esistenti, è possibile impostare la proprietà **Unique** di una singola colonna su **false**.  La definizione di una o più colonne come chiave primaria per una tabella consentirà di creare automaticamente un vincolo univoco per la colonna o le colonne specificate.  Se si rimuove una colonna dalla proprietà **PrimaryKey** di una **DataTable**, il vincolo **UniqueConstraint** verrà rimosso.  
  
 L'esempio seguente consente di creare un vincolo **UniqueConstraint** per due colonne di una **DataTable**.  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custUnique As UniqueConstraint = _  
    New UniqueConstraint(New DataColumn()   {custTable.Columns("CustomerID"), _  
    custTable.Columns("CompanyName")})  
custDS.Tables("Customers").Constraints.Add(custUnique)  
  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
UniqueConstraint custUnique = new UniqueConstraint(new DataColumn[]   
    {custTable.Columns["CustomerID"],   
    custTable.Columns["CompanyName"]});  
custDS.Tables["Customers"].Constraints.Add(custUnique);  
```  
  
## Vedere anche  
 <xref:System.Data.DataRelation>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.ForeignKeyConstraint>   
 <xref:System.Data.UniqueConstraint>   
 [Definizione dello schema di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)