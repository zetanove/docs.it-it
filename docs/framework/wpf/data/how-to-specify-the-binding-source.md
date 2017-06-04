---
title: "Procedura: specificare l&#39;origine di associazione | Microsoft Docs"
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
  - "associazione dati, associazione di origini"
  - "associazione di origini"
  - "associazione dati, origine di associazione"
ms.assetid: 55d47757-2648-4a52-987f-b767953f168c
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: specificare l&#39;origine di associazione
Nell'associazione dati, l'oggetto [origine di associazione](GTMT) fa riferimento all'oggetto da cui si ottengono i dati.  In questo argomento vengono descritte le diverse modalità per la specifica dell'[origine di associazione](GTMT).  
  
## Esempio  
 Se si associano più proprietà a un'origine comune, è opportuno utilizzare la proprietà `DataContext`, che consente di stabilire in modo pratico un ambito entro cui tutte le proprietà con associazione a dati ereditano un'origine comune.  
  
 Nell'esempio riportato di seguito, il contesto dati viene stabilito sull'elemento radice dell'applicazione.  In questo modo tutti gli elementi figlio possono ereditare tale contesto dati.  I dati per l'associazione derivano da una classe di dati personalizzata, `NetIncome`, a cui viene fatto riferimento direttamente tramite un mapping e viene assegnata la chiave di risorsa di `incomeDataSource`.  
  
 [!code-xml[DirectionalBinding#DataContext1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext1)]  
[!code-xml[DirectionalBinding#DataContext2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#datacontext2)]  
  
 Nell'esempio riportato di seguito viene illustrata la definizione della classe `NetIncome`.  
  
 [!code-csharp[DirectionalBinding#DataObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/billsdata.cs#dataobject)]
 [!code-vb[DirectionalBinding#DataObject](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DirectionalBinding/VisualBasic/NetIncome.vb#dataobject)]  
  
> [!NOTE]
>  Nell'esempio riportato in precedenza un'istanza dell'oggetto viene creata nel markup e viene utilizzata come risorsa.  Se si desidera eseguire l'associazione a un oggetto di cui è già stata creata un'istanza nel codice, è necessario impostare la proprietà `DataContext` a livello di codice.  Per un esempio, vedere [Rendere i dati disponibili per l'associazione in XAML](../../../../docs/framework/wpf/data/how-to-make-data-available-for-binding-in-xaml.md).  
  
 In alternativa, per specificare in modo esplicito l'origine sulle singole associazioni, sono disponibili le opzioni seguenti,  che hanno la precedenza sul contesto dati ereditato.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Windows.Data.Binding.Source%2A>|Utilizzare questa proprietà per impostare l'origine su un'istanza di un oggetto.  Se non è necessario disporre della funzionalità per stabilire un ambito in cui più proprietà ereditano lo stesso contesto dati, è possibile utilizzare la proprietà <xref:System.Windows.Data.Binding.Source%2A> anziché la proprietà `DataContext`.  Per ulteriori informazioni, vedere <xref:System.Windows.Data.Binding.Source%2A>.|  
|<xref:System.Windows.Data.Binding.RelativeSource%2A>|Questa proprietà è utile quando si desidera specificare l'origine relativa alla posizione in cui si trova la [destinazione dell'associazione](GTMT).  Tra gli scenari comuni che consentono l'utilizzo di questa proprietà vi sono i casi in cui si desidera associare una proprietà dell'elemento a un'altra proprietà dello stesso elemento o in cui si definisce un'associazione in uno stile o in un modello.  Per ulteriori informazioni, vedere <xref:System.Windows.Data.Binding.RelativeSource%2A>.|  
|<xref:System.Windows.Data.Binding.ElementName%2A>|Specificare una stringa che rappresenta l'elemento a cui si desidera eseguire l'associazione.  Questa operazione è utile quando si desidera eseguire l'associazione alla proprietà di un altro elemento dell'applicazione.  Ad esempio, se si desidera utilizzare un oggetto <xref:System.Windows.Controls.Slider> per controllare l'altezza di un altro controllo dell'applicazione oppure associare la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> del controllo alla proprietà <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> del controllo <xref:System.Windows.Controls.ListBox>.  Per ulteriori informazioni, vedere <xref:System.Windows.Data.Binding.ElementName%2A>.|  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.DataContext%2A?displayProperty=fullName>   
 <xref:System.Windows.FrameworkContentElement.DataContext%2A?displayProperty=fullName>   
 [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sulle dichiarazioni di associazione](../../../../docs/framework/wpf/data/binding-declarations-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)