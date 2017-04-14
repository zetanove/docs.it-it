---
title: "Procedura: ottenere o impostare le propriet&#224; di posizionamento delle aree di disegno | Microsoft Docs"
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
  - "Canvas (controllo), impostazione di proprietà di posizionamento"
ms.assetid: 1636b950-2b5a-4507-8a10-c5034cc58b1c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: ottenere o impostare le propriet&#224; di posizionamento delle aree di disegno
In questo esempio viene illustrato come utilizzare i metodi di posizionamento dell'elemento <xref:System.Windows.Controls.Canvas> per posizionare il contenuto figlio.  Viene utilizzato contenuto in una classe <xref:System.Windows.Controls.ListBoxItem> per rappresentare valori di posizionamento e i valori vengono convertiti in istanze di <xref:System.Double>, un argomento obbligatorio per il posizionamento.  I valori vengono quindi riconvertiti in stringhe e visualizzati come testo in un elemento <xref:System.Windows.Controls.TextBlock> utilizzando il metodo <xref:System.Windows.Controls.Canvas.GetLeft%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene creato un elemento <xref:System.Windows.Controls.ListBox> con undici elementi <xref:System.Windows.Controls.ListBoxItem> selezionabili.  L'evento <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> attiva il metodo `ChangeLeft` personalizzato che definisce il blocco di codice successivo.  
  
 Ogni classe <xref:System.Windows.Controls.ListBoxItem> rappresenta un valore <xref:System.Double> che è uno degli argomenti accettati dal metodo <xref:System.Windows.Controls.Canvas.SetLeft%2A> di <xref:System.Windows.Controls.Canvas>.  Per utilizzare un oggetto <xref:System.Windows.Controls.ListBoxItem> per rappresentare un'istanza di <xref:System.Double> è necessario innanzitutto convertire l'oggetto <xref:System.Windows.Controls.ListBoxItem> nel tipo di dati corretto.  
  
 [!code-xml[CanvasPositioningProperties#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml#1)]  
  
 Quando un utente modifica la selezione dell'oggetto <xref:System.Windows.Controls.ListBox>, viene richiamato il metodo `ChangeLeft` personalizzato.  Questo metodo passa la classe <xref:System.Windows.Controls.ListBoxItem> a un oggetto <xref:System.Windows.LengthConverter> che converte la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> di un oggetto <xref:System.Windows.Controls.ListBoxItem> in un'istanza di <xref:System.Double>. Si noti che questo valore è già stato convertito in <xref:System.String> utilizzando il metodo <xref:System.Windows.Controls.Control.ToString%2A>.  Questo valore viene quindi passato nuovamente ai metodi <xref:System.Windows.Controls.Canvas.SetLeft%2A> e <xref:System.Windows.Controls.Canvas.GetLeft%2A> di <xref:System.Windows.Controls.Canvas> per modificare la posizione dell'oggetto `text1`.  
  
 [!code-csharp[CanvasPositioningProperties#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml.cs#2)]
 [!code-vb[CanvasPositioningProperties#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasPositioningProperties/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Canvas>   
 <xref:System.Windows.Controls.ListBoxItem>   
 <xref:System.Windows.LengthConverter>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)