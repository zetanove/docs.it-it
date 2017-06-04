---
title: "Procedura: specificare la direzione di associazione | Microsoft Docs"
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
  - "direzione di associazione"
  - "associazione dati, direzione di associazione"
  - "direzione di associazione"
ms.assetid: 37334478-028b-4514-86c9-1420709f4818
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura: specificare la direzione di associazione
In questo esempio viene illustrato come specificare se in seguito all'associazione viene aggiornata solo la proprietà della [destinazione di associazione](GTMT), solo la proprietà dell'[origine di associazione](GTMT) oppure entrambe.  
  
## Esempio  
 Utilizzare la proprietà <xref:System.Windows.Data.Binding.Mode%2A> per specificare la direzione di associazione.  Nell'elenco di enumerazione riportato di seguito sono contenute le opzioni disponibili per gli aggiornamenti dell'associazione:  
  
-   <xref:System.Windows.Data.BindingMode> aggiorna la proprietà di destinazione o la proprietà di origine ogni volta che cambia la proprietà di destinazione o la proprietà di origine.  
  
-   <xref:System.Windows.Data.BindingMode> aggiorna la proprietà di destinazione solo quando cambia la proprietà di origine.  
  
-   <xref:System.Windows.Data.BindingMode> aggiorna la proprietà di destinazione solo quando viene avviata l'applicazione o quando cambia la proprietà <xref:System.Windows.FrameworkElement.DataContext%2A>.  
  
-   <xref:System.Windows.Data.BindingMode>aggiorna la proprietà di origine quando cambia la proprietà di destinazione.  
  
-   <xref:System.Windows.Data.BindingMode> impone l'utilizzo del valore <xref:System.Windows.Data.Binding.Mode%2A> predefinito della proprietà di destinazione.  
  
 Per ulteriori informazioni, vedere l'enumerazione <xref:System.Windows.Data.BindingMode>.  
  
 Nell'esempio riportato di seguito viene illustrato come impostare la proprietà <xref:System.Windows.Data.Binding.Mode%2A>.  
  
 [!code-xml[DirectionalBinding#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#4)]  
  
 Per rilevare le modifiche apportate all'origine \(applicabili ad associazioni <xref:System.Windows.Data.BindingMode> e <xref:System.Windows.Data.BindingMode>\), l'origine deve implementare un meccanismo di notifica delle modifiche alle proprietà appropriato, ad esempio <xref:System.ComponentModel.INotifyPropertyChanged>.  Per un esempio di implementazione di <xref:System.ComponentModel.INotifyPropertyChanged>, vedere [Implementare la notifica di modifiche alle proprietà](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md).  
  
 Per le associazioni <xref:System.Windows.Data.BindingMode> o <xref:System.Windows.Data.BindingMode>, è possibile controllare l'intervallo degli aggiornamenti dell'origine impostando la proprietà <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>.  Per ulteriori informazioni, vedere <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Data.Binding>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)