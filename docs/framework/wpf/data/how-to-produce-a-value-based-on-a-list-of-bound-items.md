---
title: "Procedura: produrre un valore in base a un elenco di elementi associati | Microsoft Docs"
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
  - "associazione dati, MultiBinding"
  - "MultiBinding"
ms.assetid: b3d06378-b511-4181-95aa-316d60c9229b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: produrre un valore in base a un elenco di elementi associati
La classe <xref:System.Windows.Data.MultiBinding> consente di associare una proprietà [di destinazione dell'associazione](GTMT) a un elenco di proprietà di origine e di applicare quindi una logica per produrre un valore con gli input specificati.  In questo esempio viene mostrato come utilizzare la classe <xref:System.Windows.Data.MultiBinding>.  
  
## Esempio  
 Nell'esempio riportato di seguito, l'elemento `NameListData` fa riferimento a una raccolta di oggetti `PersonName`, che contengono due proprietà, `firstName` e `lastName`.  Nell'esempio seguente viene generato un oggetto <xref:System.Windows.Controls.TextBlock> in cui sono mostrati, nell'ordine, il cognome e il nome di una persona.  
  
 [!code-xml[MultiBinding#Resources1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources1)]  
[!code-xml[MultiBinding#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#resources2)]  
[!code-xml[MultiBinding#MultiBindingTextBox2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#multibindingtextbox2)]  
[!code-xml[MultiBinding#Window](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/Window1.xaml#window)]  
  
 Per comprendere il modo in cui viene generato il formato cognome\-nome, è necessario esaminare l'implementazione di `NameConverter`:  
  
 [!code-csharp[MultiBinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MultiBinding/CSharp/NameConverter.cs#3)]
 [!code-vb[MultiBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MultiBinding/VisualBasic/NameConverter.vb#3)]  
  
 L'oggetto `NameConverter` implementa l'interfaccia <xref:System.Windows.Data.IMultiValueConverter>.  `NameConverter` accetta i valori delle singole associazioni e li archivia nella matrice di oggetti valori.  L'ordine in cui gli elementi <xref:System.Windows.Data.Binding> vengono visualizzati nell'elemento <xref:System.Windows.Data.MultiBinding> corrisponde all'ordine in cui tali valori sono archiviati nella matrice.  Per fare riferimento al valore dell'attributo <xref:System.Windows.Data.MultiBinding.ConverterParameter%2A> si utilizza l'argomento di parametro del metodo <xref:System.Windows.Data.MultiBinding.Converter%2A>, che esegue una modifica del parametro per determinare la modalità di formattazione del nome.  
  
## Vedere anche  
 [Convertire i dati associati](../../../../docs/framework/wpf/data/how-to-convert-bound-data.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)