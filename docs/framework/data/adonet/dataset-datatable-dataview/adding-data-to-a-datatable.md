---
title: "Aggiunta di dati a una DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d6aa8474-7bde-48f7-949d-20dc38a1625b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Aggiunta di dati a una DataTable
Una volta creata una <xref:System.Data.DataTable> e definita la relativa struttura tramite colonne e vincoli, è possibile aggiungere nuove righe di dati alla tabella.  Per aggiungere una nuova riga, dichiarare una nuova variabile come tipo <xref:System.Data.DataRow>.  Quando si chiama il metodo <xref:System.Data.DataTable.NewRow%2A>, viene restituito un nuovo oggetto **DataRow**.  La **DataTable** consente quindi la creazione dell'oggetto **DataRow** sulla base della struttura della tabella, definita da <xref:System.Data.DataColumnCollection>.  
  
 Nell'esempio seguente viene illustrato come creare una nuova riga tramite una chiamata al metodo **NewRow**.  
  
```vb  
Dim workRow As DataRow = workTable.NewRow()  
  
```  
  
```csharp  
DataRow workRow = workTable.NewRow();  
```  
  
 È quindi possibile modificare la riga appena aggiunta usando un indice o il nome della colonna, come illustrato nell'esempio seguente.  
  
```vb  
workRow("CustLName") = "Smith"  
workRow(1) = "Smith"  
  
```  
  
```csharp  
workRow["CustLName"] = "Smith";  
workRow[1] = "Smith";  
```  
  
 Una volta inseriti i dati nella nuova riga, il metodo **Add** viene usato per aggiungere la riga a <xref:System.Data.DataRowCollection>, come illustrato nel codice seguente.  
  
```vb  
workTable.Rows.Add(workRow)  
  
```  
  
```csharp  
workTable.Rows.Add(workRow);  
```  
  
 È inoltre possibile chiamare il metodo **Add** per aggiungere una nuova riga passando una matrice di valori, tipizzata come <xref:System.Object>, come illustrato nell'esempio seguente.  
  
```vb  
workTable.Rows.Add(new Object() {1, "Smith"})  
  
```  
  
```csharp  
workTable.Rows.Add(new Object[] {1, "Smith"});  
```  
  
 Il passaggio di una matrice di valori, tipizzata come **Object**, al metodo **Add** consente di creare una nuova riga all'interno della tabella e di impostarne i valori di colonna in base ai valori contenuti nella matrice dell'oggetto.  Notare che i valori contenuti nella matrice vengono associati in modo sequenziale alle colonne, in base all'ordine in cui sono presenti nella tabella.  
  
 Nell'esempio seguente vengono aggiunte dieci righe alla tabella **Customers** appena creata.  
  
```vb  
Dim workRow As DataRow  
Dim i As Integer  
  
For i = 0 To 9  
  workRow = workTable.NewRow()  
  workRow(0) = i  
  workRow(1) = "CustName" & I.ToString()  
  workTable.Rows.Add(workRow)  
Next  
  
```  
  
```csharp  
DataRow workRow;  
  
for (int i = 0; i <= 9; i++)   
{  
  workRow = workTable.NewRow();  
  workRow[0] = i;  
  workRow[1] = "CustName" + i.ToString();  
  workTable.Rows.Add(workRow);  
}  
```  
  
## Vedere anche  
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataRowCollection>   
 <xref:System.Data.DataTable>   
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)