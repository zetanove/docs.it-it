---
title: "Procedura: ridimensionare un&#39;area di disegno utilizzando un cursore | Microsoft Docs"
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
  - "Canvas (controllo)"
  - "controlli, Canvas"
  - "controlli, Thumb"
  - "ridimensionamento dei controlli Canvas"
  - "Thumb (controllo)"
ms.assetid: 7dc9f435-726c-4d4d-be41-eb24cfe17bef
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ridimensionare un&#39;area di disegno utilizzando un cursore
In questo esempio viene illustrato come utilizzare un controllo <xref:System.Windows.Controls.Primitives.Thumb> per ridimensionare un controllo <xref:System.Windows.Controls.Canvas>.  
  
## Esempio  
 Il controllo <xref:System.Windows.Controls.Primitives.Thumb> fornisce funzionalità di trascinamento che è possibile utilizzare per spostare o ridimensionare i controlli monitorando gli eventi <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>, <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> e <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> dell'oggetto <xref:System.Windows.Controls.Primitives.Thumb>.  
  
 L'utente inizia un'operazione di trascinamento premendo il pulsante sinistro del mouse quando il puntatore è fermo sul controllo <xref:System.Windows.Controls.Primitives.Thumb>.  L'operazione di trascinamento continua finché il pulsante sinistro del mouse rimane premuto.  Durante l'operazione di trascinamento, l'evento <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> può verificarsi più di una volta.  Ogni volta che si verifica, la classe <xref:System.Windows.Controls.Primitives.DragDeltaEventArgs> fornisce la modifica di posizione che corrisponde alla modifica della posizione del mouse.  Quando l'utente rilascia il pulsante sinistro del mouse, l'operazione di trascinamento termina.  L'operazione di trascinamento fornisce solo nuove coordinate; non riposiziona automaticamente il controllo <xref:System.Windows.Controls.Primitives.Thumb>.  
  
 Nell'esempio seguente viene illustrato un controllo <xref:System.Windows.Controls.Primitives.Thumb> che corrisponde all'elemento figlio di un controllo <xref:System.Windows.Controls.Canvas>.  Il gestore dell'evento <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> fornisce la logica per spostare il controllo <xref:System.Windows.Controls.Primitives.Thumb> e ridimensionare l'oggetto <xref:System.Windows.Controls.Canvas>.  I gestori degli eventi <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> e <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> modificano il colore del controllo <xref:System.Windows.Controls.Primitives.Thumb> durante un'operazione di trascinamento.  Nell'esempio seguente viene definito l'oggetto <xref:System.Windows.Controls.Primitives.Thumb>.  
  
 [!code-xml[Thumb#thumb](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml#thumb)]  
  
 Nell'esempio seguente viene illustrato il gestore dell'evento <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> che sposta il controllo <xref:System.Windows.Controls.Primitives.Thumb> e ridimensiona l'oggetto <xref:System.Windows.Controls.Canvas> in risposta a un movimento del mouse.  
  
 [!code-csharp[Thumb#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#2)]  
  
 Nell'esempio seguente viene illustrato il gestore dell'evento <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>.  
  
 [!code-csharp[Thumb#DragStartedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragstartedhandler)]
 [!code-vb[Thumb#DragStartedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragstartedhandler)]  
  
 Nell'esempio seguente viene illustrato il gestore dell'evento <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted>.  
  
 [!code-csharp[Thumb#DragCompletedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragcompletedhandler)]
 [!code-vb[Thumb#DragCompletedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragcompletedhandler)]  
  
 Per l'esempio completo, vedere [Esempio di funzionalità di trascinamento di un controllo Thumb](http://go.microsoft.com/fwlink/?LinkID=160042) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Controls.Primitives.Thumb>   
 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>   
 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta>   
 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted>