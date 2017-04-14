---
title: "Procedura: ottenere le propriet&#224; di un oggetto di sistema di stampa senza ricorrere alla reflection | Microsoft Docs"
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
  - "PrintSystemObject, recupero delle proprietà"
ms.assetid: 43560f28-183d-41c1-b9d1-de7c2552273e
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: ottenere le propriet&#224; di un oggetto di sistema di stampa senza ricorrere alla reflection
L'utilizzo della reflection per descrivere in dettaglio le proprietà \(e i relativi tipi\) su un oggetto può influire negativamente sulle prestazioni dell'applicazione.  Lo spazio dei nomi <xref:System.Printing.IndexedProperties> consente di ottenere queste informazioni utilizzando la reflection.  
  
## Esempio  
 I passaggi di questa procedura sono indicati di seguito.  
  
1.  Creare un'istanza del tipo.  Nell'esempio riportato di seguito, il tipo è il tipo <xref:System.Printing.PrintQueue> fornito con [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)], ma codice quasi identico dovrebbe funzionare per tipi che è possibile derivare da <xref:System.Printing.PrintSystemObject>.  
  
2.  Creare un oggetto <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> dalla proprietà <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A> del tipo.  La proprietà <xref:System.Collections.DictionaryEntry.Value%2A> di ciascun elemento di questo dizionario è un oggetto di uno dei tipi derivati da <xref:System.Printing.IndexedProperties.PrintProperty>.  
  
3.  Enumerare i membri del dizionario.  Per ognuno di essi, eseguire le operazioni seguenti.  
  
4.  Eseguire l'upcast del valore di ogni voce in <xref:System.Printing.IndexedProperties.PrintProperty> e utilizzarlo per creare un oggetto <xref:System.Printing.IndexedProperties.PrintProperty>.  
  
5.  Ottenere il tipo della proprietà <xref:System.Printing.IndexedProperties.PrintProperty.Value%2A> di ogni oggetto <xref:System.Printing.IndexedProperties.PrintProperty>.  
  
 [!code-csharp[GetPrintObjectPropertyTypesWithoutReflection#ShowPropertyTypesWithoutReflection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GetPrintObjectPropertyTypesWithoutReflection/CSharp/Program.cs#showpropertytypeswithoutreflection)]
 [!code-vb[GetPrintObjectPropertyTypesWithoutReflection#ShowPropertyTypesWithoutReflection](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GetPrintObjectPropertyTypesWithoutReflection/visualbasic/program.vb#showpropertytypeswithoutreflection)]  
  
## Vedere anche  
 <xref:System.Printing.IndexedProperties.PrintProperty>   
 <xref:System.Printing.PrintSystemObject>   
 <xref:System.Printing.IndexedProperties>   
 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Collections.DictionaryEntry>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)