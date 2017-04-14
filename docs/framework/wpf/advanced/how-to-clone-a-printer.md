---
title: "Procedura: duplicare una stampante | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "duplicazione di code di stampa"
  - "duplicazione di stampanti"
  - "code di stampa"
  - "code di stampa, duplicazione"
  - "stampanti, duplicazione"
ms.assetid: dd6997c9-fe04-40f8-88a6-92e3ac0889eb
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: duplicare una stampante
Molte aziende desiderano, in un determinato momento, comprare più stampanti dello stesso modello.  In genere, queste vengono installate con impostazioni di configurazione praticamente identiche.  L'installazione delle stampanti una ad una può comportare tempi lunghi e un rischio di errori.  Lo spazio dei nomi <xref:System.Printing.IndexedProperties?displayProperty=fullName> e la classe <xref:System.Printing.PrintServer.InstallPrintQueue%2A> esposti con [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)] consentono l'installazione istantanea di un numero di code di stampa indeterminato, che vengono duplicate in base a una coda di stampa esistente.  
  
## Esempio  
 Nell'esempio riportato di seguito, viene duplicata una seconda coda di stampa in base a una coda di stampa esistente.  La seconda differisce dalla prima solo in relazione al nome, alla posizione, alla porta e allo stato condiviso.  I passaggi principali di questa procedura sono indicati di seguito.  
  
1.  Creare un oggetto <xref:System.Printing.PrintQueue> per la stampante esistente che sarà duplicata.  
  
2.  Creare un oggetto <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> dall'oggetto <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A> di <xref:System.Printing.PrintQueue>.  La proprietà <xref:System.Collections.DictionaryEntry.Value%2A> di ciascun elemento di questo dizionario è un oggetto di uno dei tipi derivati da <xref:System.Printing.IndexedProperties.PrintProperty>.  È possibile impostare il valore di un elemento di questo dizionario in due modi.  
  
    -   Utilizzare i metodi **Remove** e <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.Add%2A> del dizionario per rimuovere l'elemento e quindi aggiungerlo nuovamente con il valore desiderato.  
  
    -   Utilizzare il metodo <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.SetProperty%2A> del dizionario.  
  
     Entrambi i metodi vengono illustrati nell'esempio riportato di seguito.  
  
3.  Creare un oggetto <xref:System.Printing.IndexedProperties.PrintBooleanProperty> e impostare <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> su "IsShared" e <xref:System.Printing.IndexedProperties.PrintBooleanProperty.Value%2A> su `true`.  
  
4.  Utilizzare l'oggetto <xref:System.Printing.IndexedProperties.PrintBooleanProperty> come valore dell'elemento "IsShared" di <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>.  
  
5.  Creare un oggetto <xref:System.Printing.IndexedProperties.PrintStringProperty> e impostare <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> su "ShareName" e <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> su un valore di <xref:System.String> appropriato.  
  
6.  Utilizzare l'oggetto <xref:System.Printing.IndexedProperties.PrintStringProperty> come valore dell'elemento "ShareName" di <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>.  
  
7.  Creare un oggetto <xref:System.Printing.IndexedProperties.PrintStringProperty> e impostare <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> su "Location" e <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> su un valore di <xref:System.String> appropriato.  
  
8.  Utilizzare il secondo oggetto <xref:System.Printing.IndexedProperties.PrintStringProperty> come valore dell'elemento "Location" di <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>.  
  
9. Creare una matrice di <xref:System.String>.  Ogni elemento è il nome di una porta del server.  
  
10. Utilizzare <xref:System.Printing.PrintServer.InstallPrintQueue%2A> per installare la nuova stampante con i nuovi valori.  
  
 Di seguito viene riportato un esempio.  
  
 [!code-csharp[ClonePrinter#ClonePrinter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClonePrinter/CSharp/Program.cs#cloneprinter)]
 [!code-vb[ClonePrinter#ClonePrinter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClonePrinter/visualbasic/program.vb#cloneprinter)]  
  
## Vedere anche  
 <xref:System.Printing.IndexedProperties>   
 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Collections.DictionaryEntry>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)