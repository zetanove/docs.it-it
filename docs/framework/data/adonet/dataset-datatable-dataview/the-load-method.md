---
title: "Metodo Load | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e22e5812-89c6-41f0-9302-bb899a46dbff
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Metodo Load
È possibile usare il metodo <xref:System.Data.DataTable.Load%2A> per caricare un tipo <xref:System.Data.DataTable> con righe provenienti da un'origine dati.  Si tratta di un metodo di overload che, nella forma più semplice, accetta un singolo parametro, **DataReader**.  In questa forma, viene semplicemente caricata la **DataTable** con le righe.  Facoltativamente, è possibile specificare il parametro **LoadOption** per controllare il modo in cui vengono aggiunti i dati alla **DataTable**.  
  
 Il parametro **LoadOption** è particolarmente utile nei casi in cui la **DataTable** contenga già righe di dati, in quanto descrive in che modo i dati in arrivo dall'origine dati verranno combinati con i dati già presenti nella tabella.  Ad esempio, **PreserveCurrentValues**, ovvero l'impostazione predefinita, specifica che nei casi in cui una riga è contrassegnata come **Added** nella **DataTable**, il valore **Original** di ciascuna colonna è impostato sul contenuto della riga corrispondente dell'origine dati.  Il valore **Current** conserverà i valori assegnati quando la riga è stata aggiunta mentre il valore della riga relativo a **RowState** verrà impostato su **Changed**.  
  
 Nella tabella seguente viene fornita una breve descrizione dei valori di enumerazione di <xref:System.Data.LoadOption>.  
  
|Valore LoadOption|Descrizione|  
|-----------------------|-----------------|  
|**OverwriteRow**|Se le righe in arrivo presentano lo stesso valore **PrimaryKey** di una riga già presente nella **DataTable**, i valori **Original** e **Current** di ciascuna colonna vengono sostituiti dai valori della riga in arrivo e la proprietà **RowState** viene impostata su **Unchanged**.<br /><br /> Le righe provenienti da un'origine dati e non ancora presenti nella **DataTable** vengono aggiunte con il valore di **RowState** pari a **Unchanged**.<br /><br /> Se questa opzione è attiva, il contenuto della **DataTable** viene aggiornato in modo da corrispondere al contenuto dell'origine dati.|  
|**PreserveCurrentValues \(impostazione predefinita\)**|Se le righe in arrivo presentano lo stesso valore **PrimaryKey** di una riga già presente nella **DataTable**, il valore **Original** viene impostato sul contenuto della riga in arrivo e il valore **Current** non viene modificato.<br /><br /> Se il valore relativo a **RowState** è **Added** o **Modified**, verrà impostato su **Modified**.<br /><br /> Se il valore relativo a **RowState** era **Deleted**, rimarrà **Deleted**.<br /><br /> Le righe provenienti da un'origine dati non ancora presenti nella **DataTable** vengono aggiunte e **RowState** viene impostato su **Unchanged**.|  
|**UpdateCurrentValues**|Se le righe in arrivo presentano lo stesso valore **PrimaryKey** della riga già presente nella **DataTable**, il valore **Current** viene copiato nel valore **Original** e viene quindi impostato sul contenuto della riga in arrivo.<br /><br /> Se il valore relativo a **RowState** nella **DataTable** era **Added**, **RowState** rimarrà **Added**.  Per le righe contrassegnate come **Modified** o **Deleted**, il valore relativo a **RowState** sarà **Modified**.<br /><br /> Le righe provenienti da un'origine dati non ancora presenti nella **DataTable** vengono aggiunte e **RowState** viene impostato su **Added**.|  
  
 Nell'esempio seguente viene usato il metodo **Load** per visualizzare un elenco delle date di nascita dei dipendenti nel database **Northwind**.  
  
 \[Visual Basic\]  
  
```  
Private Sub LoadBirthdays(ByVal connectionString As String)  
    ' Assumes that connectionString is a valid connection string  
    ' to the Northwind database on SQL Server.  
    Dim queryString As String = _  
    "SELECT LastName, FirstName, BirthDate " & _  
      " FROM dbo.Employees " & _  
      "ORDER BY BirthDate, LastName, FirstName"  
  
    ' Open and fill a DataSet.   
    Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
        queryString, connectionString)  
    Dim employees As New DataSet  
    adapter.Fill(employees, "Employees")  
  
    ' Create a SqlDataReader for use with the Load Method.  
    Dim reader As DataTableReader = employees.GetDataReader()  
  
    ' Create an instance of DataTable and assign the first  
    ' DataTable in the DataSet.Tables collection to it.  
    Dim dataTableEmp As DataTable = employees.Tables(0)  
  
    ' Fill the DataTable with data by calling Load and  
    ' passing the SqlDataReader.  
    dataTableEmp.Load(reader, LoadOption.OverwriteRow)  
  
    ' Loop through the rows collection and display the values  
    ' in the console window.  
    Dim employeeRow As DataRow  
    For Each employeeRow In dataTableEmp.Rows  
        Console.WriteLine("{0:MM\\dd\\yyyy}" & ControlChars.Tab & _  
          "{1}, {2}", _  
          employeeRow("BirthDate"), _  
          employeeRow("LastName"), _  
          employeeRow("FirstName"))  
    Next employeeRow  
  
    ' Keep the window opened to view the contents.  
    Console.ReadLine()  
End Sub  
```  
  
## Vedere anche  
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)