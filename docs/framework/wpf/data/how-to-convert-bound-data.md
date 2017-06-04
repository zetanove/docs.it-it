---
title: "Procedura: convertire i dati associati | Microsoft Docs"
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
  - "associazione dati, conversione di dati associati"
  - "conversione, dati associati"
  - "associazione dati, conversione di dati associati"
ms.assetid: b00aaa19-c6df-4c3b-a9fd-88a0b488df2b
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: convertire i dati associati
In questo esempio viene illustrata la procedura per applicare la conversione ai dati utilizzati nelle associazioni.  
  
 Per convertire i dati durante un'associazione, è necessario creare una classe che implementi l'interfaccia <xref:System.Windows.Data.IValueConverter>, che include i metodi <xref:System.Windows.Data.IValueConverter.Convert%2A> e <xref:System.Windows.Data.IValueConverter.ConvertBack%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene mostrata l'implementazione di un convertitore di date, che consente di convertire il valore della data passato in modo da visualizzare solo l'anno, il mese e il giorno.  Quando si implementa l'interfaccia <xref:System.Windows.Data.IValueConverter>, è opportuno inserire nell'implementazione un attributo <xref:System.Windows.Data.ValueConversionAttribute> per indicare agli strumenti di sviluppo i tipi di dati coinvolti nella conversione, come nell'esempio riportato di seguito:  
  
 [!code-csharp[DataBindingLab#18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DateConverter.cs#18)]
 [!code-vb[DataBindingLab#18](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/DateConverter.vb#18)]  
  
 Una volta creato un convertitore, è possibile aggiungerlo come risorsa nel file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Nell'esempio seguente viene eseguito il mapping di*src* allo spazio dei nomi nel quale viene definito *DateConverter*.  
  
 [!code-xml[DataBindingLab#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DataBindingLabApp.xaml#15)]  
  
 Infine, è possibile utilizzare il convertitore nell'associazione mediante la seguente sintassi.  Nell'esempio riportato di seguito, il contenuto di testo di <xref:System.Windows.Controls.TextBlock> è associato a *StartDate*, una proprietà di un'origine dati esterna.  
  
 [!code-xml[DataBindingLab#17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/DataBindingLabApp.xaml#17)]  
  
 Le risorse di stile a cui si fa riferimento nell'esempio precedente vengono definite nella sezione relativa alle risorse, non illustrata in questo argomento.  
  
## Vedere anche  
 [Implementare la convalida dell'associazione](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)