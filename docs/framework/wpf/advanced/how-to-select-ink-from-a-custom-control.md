---
title: "Procedura: selezionare l&#39;input penna da un controllo personalizzato | Microsoft Docs"
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
  - "controlli, selezione di input penna"
  - "controlli personalizzati, selezione di input penna"
  - "input penna, selezione da controllo personalizzato"
ms.assetid: 5f3a45c6-6d40-4017-9b47-933f134ceba3
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: selezionare l&#39;input penna da un controllo personalizzato
Aggiungendo un oggetto <xref:System.Windows.Ink.IncrementalLassoHitTester> al controllo personalizzato, è possibile abilitare quest'ultimo in modo che l'utente possa selezionare l'input penna mediante lo strumento lazo, analogamente al modo in cui l'oggetto <xref:System.Windows.Controls.InkCanvas> seleziona l'input penna con un lazo.  
  
 In questo esempio si presuppone che l'utente sia in grado di creare un controllo personalizzato abilitato per l'input penna.  Per creare un controllo personalizzato che supporti l'input penna, vedere [Creazione di un controllo di input penna](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md).  
  
## Esempio  
 Quando l'utente utilizza lo strumento lazo, l'oggetto <xref:System.Windows.Ink.IncrementalLassoHitTester> è in grado di anticipare quali tratti si troveranno all'interno dei confini del lazo al termine dell'operazione.  I tratti che si troveranno all'interno dei confini del lazo possono essere considerati selezionati e,  come tali, potranno anche essere deselezionati.  Ad esempio, se l'utente cambia direzione mentre utilizza lo strumento lazo, è possibile che l'oggetto <xref:System.Windows.Ink.IncrementalLassoHitTester> causi la deselezione di alcuni tratti.  
  
 L'oggetto <xref:System.Windows.Ink.IncrementalLassoHitTester> genera l'evento <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged>, che abilita la risposta del controllo personalizzato mentre l'utente utilizza lo strumento lazo.  È ad esempio possibile modificare l'aspetto dei tratti mentre vengono selezionati e deselezionati.  
  
## Gestione della modalità input penna  
 Per l'utente è utile che il lazo sia diverso rispetto all'input penna sul controllo.  A tale scopo, è necessario utilizzare lo strumento personalizzato per tenere traccia del fatto che l'utente scriva o selezioni l'input penna.  Il modo più semplice per ottenere questo risultato consiste nel dichiarare un'enumerazione con due valori, uno per indicare che l'utente scrive l'input penna e un altro per indicare che l'utente seleziona l'input penna.  
  
 [!code-csharp[HowToSelectInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#2)]
 [!code-vb[HowToSelectInk#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#2)]  
  
 Aggiungere quindi due oggetti <xref:System.Windows.Ink.DrawingAttributes> alla classe, uno da utilizzare quando l'utente scrive l'input penna e l'altro quando l'utente seleziona l'input penna.  Nel costruttore, inizializzare l'oggetto <xref:System.Windows.Ink.DrawingAttributes> e collegare entrambi gli eventi <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> allo stesso gestore eventi,  quindi impostare la proprietà <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> dell'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> sull'input penna <xref:System.Windows.Ink.DrawingAttributes>.  
  
 [!code-csharp[HowToSelectInk#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#3)]
 [!code-vb[HowToSelectInk#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#3)]  
[!code-csharp[HowToSelectInk#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#4)]
[!code-vb[HowToSelectInk#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#4)]  
  
 Aggiungere una proprietà che espone la modalità di selezione.  Quando l'utente cambia la modalità di selezione, impostare la proprietà <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> dell'oggetto <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> sull'oggetto <xref:System.Windows.Ink.DrawingAttributes> appropriato, quindi ricollegare la proprietà <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> all'oggetto <xref:System.Windows.Controls.InkPresenter>.  
  
 [!code-csharp[HowToSelectInk#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#5)]
 [!code-vb[HowToSelectInk#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#5)]  
  
 Esporre l'oggetto <xref:System.Windows.Ink.DrawingAttributes> come proprietà affinché le applicazioni possano determinare l'aspetto dei tratti di input penna e selezione.  
  
 [!code-csharp[HowToSelectInk#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#6)]
 [!code-vb[HowToSelectInk#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#6)]  
  
 Quando una proprietà di un oggetto <xref:System.Windows.Ink.DrawingAttributes> cambia, è necessario ricollegare la proprietà <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> all'oggetto <xref:System.Windows.Controls.InkPresenter>.  Nel gestore dell'evento <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged>, ricollegare la proprietà <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> all'oggetto <xref:System.Windows.Controls.InkPresenter>.  
  
 [!code-csharp[HowToSelectInk#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#7)]
 [!code-vb[HowToSelectInk#7](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#7)]  
  
## Utilizzo di IncrementalLassoHitTester  
 Creare e inizializzare un oggetto <xref:System.Windows.Ink.StrokeCollection> contenente i tratti selezionati.  
  
 [!code-csharp[HowToSelectInk#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#8)]
 [!code-vb[HowToSelectInk#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#8)]  
  
 Quando l'utente inizia a disegnare un tratto, che si tratti di un input penna o di un lazo, deselezionare eventuali tratti selezionati.  Se l'utente disegna un lazo, creare un oggetto <xref:System.Windows.Ink.IncrementalLassoHitTester> chiamando <xref:System.Windows.Ink.StrokeCollection.GetIncrementalLassoHitTester%2A>, sottoscrivere l'evento <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> e chiamare <xref:System.Windows.Ink.IncrementalHitTester.AddPoints%2A>.  Questo codice può essere un metodo separato e può essere chiamato dai metodi <xref:System.Windows.UIElement.OnStylusDown%2A> e <xref:System.Windows.UIElement.OnMouseDown%2A>.  
  
 [!code-csharp[HowToSelectInk#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#9)]
 [!code-vb[HowToSelectInk#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#9)]  
  
 Aggiungere i punti dello stilo all'oggetto <xref:System.Windows.Ink.IncrementalLassoHitTester> mentre l'utente disegna il lazo.  Chiamare il metodo seguente dai metodi <xref:System.Windows.UIElement.OnStylusMove%2A>, <xref:System.Windows.UIElement.OnStylusUp%2A>, <xref:System.Windows.UIElement.OnMouseMove%2A> e <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A>.  
  
 [!code-csharp[HowToSelectInk#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#10)]
 [!code-vb[HowToSelectInk#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#10)]  
  
 Gestire l'evento <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged?displayProperty=fullName> in risposta alla selezione e alla deselezione dei tratti da parte dell'utente.  La classe <xref:System.Windows.Ink.LassoSelectionChangedEventArgs> ha le proprietà <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.SelectedStrokes%2A> e <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.DeselectedStrokes%2A> che consentono di ottenere rispettivamente i tratti selezionati e deselezionati.  
  
 [!code-csharp[HowToSelectInk#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#11)]
 [!code-vb[HowToSelectInk#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#11)]  
  
 Quando l'utente completa il disegno del lazo, annullare la sottoscrizione dell'evento <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> e chiamare il metodo <xref:System.Windows.Ink.IncrementalHitTester.EndHitTesting%2A>.  
  
 [!code-csharp[HowToSelectInk#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#12)]
 [!code-vb[HowToSelectInk#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#12)]  
  
## Riepilogo.  
 Nell'esempio riportato di seguito viene illustrato un controllo personalizzato che consente all'utente di selezionare l'input penna con lo strumento lazo.  
  
 [!code-csharp[HowToSelectInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#1)]
 [!code-vb[HowToSelectInk#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Ink.IncrementalLassoHitTester>   
 <xref:System.Windows.Ink.StrokeCollection>   
 <xref:System.Windows.Input.StylusPointCollection>   
 [Creazione di un controllo di input penna](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md)