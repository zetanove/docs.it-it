---
title: "Gestione degli eventi di DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5675663-fc91-4e0d-87a9-481b25b64c0f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Gestione degli eventi di DataView
Per determinare se una visualizzazione è stata aggiornata, è possibile usare l'evento <xref:System.Data.DataView.ListChanged> del <xref:System.Data.DataView>.  Gli aggiornamenti che generano l'evento includono l'aggiunta, l'eliminazione o la modifica di una riga nella tabella sottostante; l'aggiunta o l'eliminazione di una colonna nello schema della tabella sottostante e una modifica in una relazione padre o figlio.  Se l'elenco di righe visualizzato è stato modificato in modo significativo a causa dell'applicazione di un nuovo criterio di ordinamento o un nuovo filtro, l'evento **ListChanged** invierà una notifica.  
  
 L'evento **ListChanged** implementa il delegato **ListChangedEventHandler** dello spazio dei nomi <xref:System.ComponentModel> e accetta come input un oggetto <xref:System.ComponentModel.ListChangedEventArgs>.  È possibile determinare il tipo di modifica apportato mediante il valore dell'enumerazione <xref:System.ComponentModel.ListChangedType> nella proprietà **ListChangedType** dell'oggetto **ListChangedEventArgs**.  Nel caso di modifiche che implicano l'aggiunta, l'eliminazione o lo spostamento di righe, è possibile accedere al nuovo indice della riga aggiunta o spostata e all'indice precedente della riga eliminata mediante la proprietà **NewIndex** dell'oggetto **ListChangedEventArgs**.  Nel caso di una riga spostata, è possibile accedere all'indice precedente della riga spostata mediante la proprietà **OldIndex** dell'oggetto **ListChangedEventArgs**.  
  
 Un evento **ListChanged** viene esposto anche dal **DataViewManager** per avvisare l'utente nel caso in cui una tabella sia stata aggiunta o rimossa o nel caso in cui siano state apportate modifiche alla raccolta **Relations** del **DataSet** sottostante.  
  
 Nell'esempio di codice seguente viene illustrata l'aggiunta di un gestore di eventi **ListChanged**.  
  
```vb  
AddHandler custView.ListChanged, _  
  New System.ComponentModel.ListChangedEventHandler( _  
  AddressOf OnListChanged)  
  
Private Shared Sub OnListChanged( _  
  sender As Object, args As System.ComponentModel.ListChangedEventArgs)  
  Console.WriteLine("ListChanged:")  
  Console.WriteLine(vbTab & "    Type = " & _  
    System.Enum.GetName(args.ListChangedType.GetType(), _  
    args.ListChangedType))  
  Console.WriteLine(vbTab & "OldIndex = " & args.OldIndex)  
  Console.WriteLine(vbTab & "NewIndex = " & args.NewIndex)  
End Sub  
  
```  
  
```csharp  
custView.ListChanged  += new   
  System.ComponentModel.ListChangedEventHandler(OnListChanged);  
  
protected static void OnListChanged(object sender,   
  System.ComponentModel.ListChangedEventArgs args)  
{  
  Console.WriteLine("ListChanged:");  
  Console.WriteLine("\t    Type = " + args.ListChangedType);  
  Console.WriteLine("\tOldIndex = " + args.OldIndex);  
  Console.WriteLine("\tNewIndex = " + args.NewIndex);  
}  
```  
  
## Vedere anche  
 <xref:System.Data.DataView>   
 <xref:System.ComponentModel.ListChangedEventHandler>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)