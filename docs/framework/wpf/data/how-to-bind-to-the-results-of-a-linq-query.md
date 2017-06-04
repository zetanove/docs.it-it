---
title: "Procedura: eseguire l&#39;associazione ai risultati di una query LINQ | Microsoft Docs"
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
  - "associazione ai risultati di query LINQ [WPF]"
  - "esecuzione di una query LINQ [WPF], associazione ai risultati"
ms.assetid: ff2844d9-17ed-4ea6-aab1-5111af0bc684
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: eseguire l&#39;associazione ai risultati di una query LINQ
In questo esempio viene illustrato come eseguire una query LINQ e successivamente eseguire l'associazione ai risultati ottenuti.  
  
## Esempio  
 Nell'esempio seguente vengono create due caselle di riepilogo.  La prima casella di riepilogo contiene tre voci di elenco.  
  
 [!code-xml[LinqExample#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml#ui)]  
  
 Selezionando un elemento dalla prima casella di riepilogo viene richiamato il seguente gestore eventi.  In questo esempio, `Tasks` è una raccolta di oggetti `Task`.  La classe `Task` dispone di una proprietà denominata `Priority`.  Questo gestore eventi esegue una query LINQ che restituisce la raccolta di oggetti `Task` con il valore di priorità selezionato, che viene quindi impostato come <xref:System.Windows.FrameworkElement.DataContext%2A>:  
  
 [!code-csharp[LinqExample#Using](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#using)]  
[!code-csharp[LinqExample#Tasks](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#tasks)]  
[!code-csharp[LinqExample#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#handler)]  
  
 La seconda casella di riepilogo esegue l'associazione a tale raccolta perché il valore di <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> è impostato su `{Binding}`.  Di conseguenza visualizza la raccolta restituita, in base a `myTaskTemplate`<xref:System.Windows.DataTemplate>.  
  
## Vedere anche  
 [Rendere i dati disponibili per l'associazione in XAML](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md)   
 [Eseguire l'associazione a una raccolta e visualizzare informazioni in base alla selezione](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)   
 [Novità di WPF versione 4.5](../../../../docs/framework/wpf/getting-started/whats-new.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)