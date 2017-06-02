---
title: "Ricerca di righe | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5da300e2-74c0-4d13-9202-fc20ed8212d8
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Ricerca di righe
È possibile eseguire ricerche di righe in base ai relativi valori della chiave di ordinamento usando i metodi <xref:System.Data.DataView.Find%2A> e <xref:System.Data.DataView.FindRows%2A> del tipo <xref:System.Data.DataView>.  La distinzione tra maiuscole e minuscole nei valori di ricerca dei metodi **Find** e **FindRows** viene determinata dalla proprietà **CaseSensitive** del tipo <xref:System.Data.DataTable> sottostante.  Per restituire un risultato, è necessario che i valori di ricerca corrispondano interamente ai valori della chiave di ordinamento esistenti.  
  
 Il metodo **Find** restituisce un numero intero con l'indice del tipo <xref:System.Data.DataRowView> che corrisponde ai criteri di ricerca.  Se più righe corrispondono ai criteri di ricerca, verrà restituito solo l'indice del primo **DataRowView** corrispondente.  Se non viene trovata alcuna corrispondenza, il metodo **Find** restituirà \-1.  
  
 Per restituire risultati di ricerca corrispondenti a più righe, usare il metodo **FindRows**.  Il metodo **FindRows** esegue le stesse operazioni del metodo **Find**, ma restituisce una matrice **DataRowView** contenente riferimenti a tutte le righe corrispondenti nel **DataView**.  Se non viene rilevata alcuna corrispondenza, la matrice **DataRowView** risulterà vuota.  
  
 Per usare i metodi **Find** o **FindRows**, è necessario specificare un ordinamento impostando **ApplyDefaultSort** su **true** o usando la proprietà **Sort**.  Se non viene specificato alcun ordinamento, verrà generata un'eccezione.  
  
 I metodi **Find** e **FindRows** accettano come input una matrice di valori, la cui lunghezza corrisponde al numero di colonne dell'ordinamento.  In caso di ordinamento di una singola colonna, è possibile passare un unico valore.  In caso di ordinamenti contenenti più colonne, viene passata una matrice di oggetti.  Notare che nel caso di un ordinamento di più colonne è necessario che i valori della matrice di oggetti corrispondano all'ordinamento delle colonne specificato nella proprietà **Sort** di **DataView**.  
  
 Nell'esempio di codice seguente viene illustrata la chiamata del metodo **Find** per un **DataView** con un ordinamento di una singola colonna.  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName", DataViewRowState.CurrentRows)  
  
Dim rowIndex As Integer = custView.Find("The Cracker Box")  
  
If rowIndex = -1 Then  
  Console.WriteLine("No match found.")  
Else  
  Console.WriteLine("{0}, {1}", _  
    custView(rowIndex)("CustomerID").ToString(), _  
    custView(rowIndex)("CompanyName").ToString())  
End If  
  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",   
  "CompanyName", DataViewRowState.CurrentRows);  
  
int rowIndex = custView.Find("The Cracker Box");  
  
if (rowIndex == -1)  
  Console.WriteLine("No match found.");  
else  
  Console.WriteLine("{0}, {1}",  
    custView[rowIndex]["CustomerID"].ToString(),  
    custView[rowIndex]["CompanyName"].ToString());  
```  
  
 Se nella proprietà **Sort** sono specificate più colonne, è necessario passare una matrice di oggetti con i valori di ricerca per ogni colonna nell'ordine specificato dalla proprietà **Sort**, come illustrato nell'esempio di codice seguente.  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName, ContactName", _  
  DataViewRowState.CurrentRows)  
  
Dim foundRows() As DataRowView = _  
  custView.FindRows(New object() {"The Cracker Box", "Liu Wong"})  
  
If foundRows.Length = 0 Then  
  Console.WriteLine("No match found.")  
Else  
  Dim myDRV As DataRowView  
  For Each myDRV In foundRows  
    Console.WriteLine("{0}, {1}", _  
      myDRV("CompanyName").ToString(), myDRV("ContactName").ToString())  
  Next  
End If  
  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",  
  "CompanyName, ContactName",  
  DataViewRowState.CurrentRows);  
  
DataRowView[] foundRows =   
  custView.FindRows(new object[] {"The Cracker Box", "Liu Wong"});  
  
if (foundRows.Length == 0)  
  Console.WriteLine("No match found.");  
else  
  foreach (DataRowView myDRV in foundRows)  
    Console.WriteLine("{0}, {1}", myDRV["CompanyName"].ToString(),   
      myDRV["ContactName"].ToString());  
```  
  
## Vedere anche  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)