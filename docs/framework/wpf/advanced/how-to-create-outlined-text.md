---
title: "Procedura: creare testo con contorni | Microsoft Docs"
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
  - "pennello sfumato"
  - "pennello sfumato lineare"
  - "testo delimitato"
  - "tipografia, pennello sfumato lineare"
  - "tipografia, effetti struttura"
ms.assetid: 4aa3cf6e-1953-4f26-8230-7c1409e5f28d
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: creare testo con contorni
Nella maggior parte dei casi, quando si aggiungono ornamenti alle stringhe di testo in un'applicazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], si utilizza il testo come una raccolta di caratteri discreti, o glifi.  Ad esempio, è possibile creare un pennello sfumato lineare e applicarlo alla proprietà <xref:System.Windows.Controls.Control.Foreground%2A> di un oggetto <xref:System.Windows.Controls.TextBox>.  Quando viene visualizzata o modificata la casella di testo, il pennello sfumato lineare viene applicato automaticamente all'insieme corrente di caratteri nella stringa di testo.  
  
 ![Testo visualizzato con pennello sfumato lineare](../../../../docs/framework/wpf/advanced/media/outlinedtext01.png "OutlinedText01")  
Esempio di pennello sfumato lineare applicato a una casella di testo  
  
 Tuttavia, è anche possibile convertire il testo in oggetti <xref:System.Windows.Media.Geometry>, per creare altri tipi di testo visivamente dettagliato.  Ad esempio, è possibile creare un oggetto <xref:System.Windows.Media.Geometry> in base alla struttura di una stringa di testo.  
  
 ![Struttura di testo con pennello sfumato lineare](../../../../docs/framework/wpf/advanced/media/outlinedtext02.png "OutlinedText02")  
Esempio di pennello sfumato lineare applicato alla geometria della struttura del testo  
  
 Se il testo viene convertito in un oggetto <xref:System.Windows.Media.Geometry>, non costituisce più una raccolta di caratteri. Di conseguenza, non è possibile modificare i caratteri della stringa di testo.  È tuttavia possibile intervenire sull'aspetto del testo convertito modificandone le proprietà di tratto e riempimento.  Il tratto fa riferimento alla struttura del testo convertito, mentre il riempimento fa riferimento all'area all'interno della struttura del testo convertito.  
  
 Negli esempi seguenti vengono illustrate diverse modalità di creazione di effetti visivi mediante la modifica del tratto e del riempimento del testo convertito.  
  
 ![Testo con colori diversi per tratto e riempimento](../../../../docs/framework/wpf/advanced/media/outlinedtext03.png "OutlinedText03")  
Esempio di impostazione di tratto e riempimento in colori diversi  
  
 ![Testo con tratto con immagine applicato](../../../../docs/framework/wpf/advanced/media/outlinedtext04.png "OutlinedText04")  
Esempio di tratto con immagine applicato al tratto  
  
 È anche possibile modificare il rettangolo del riquadro delimitatore, o l'evidenziazione, del testo convertito.  Nell'esempio riportato di seguito viene illustrata una modalità di creazione di effetti visivi mediante la modifica del tratto e dell'evidenziazione del testo convertito.  
  
 ![Testo con tratto con immagine applicato](../../../../docs/framework/wpf/advanced/media/outlinedtext05.png "OutlinedText05")  
Esempio di tratto con immagine applicato al tratto e all'evidenziazione  
  
## Esempio  
 La chiave per la conversione del testo in un oggetto <xref:System.Windows.Media.Geometry> consiste nell'utilizzare l'oggetto <xref:System.Windows.Media.FormattedText>.  Una volta creato questo oggetto, è possibile utilizzare i metodi <xref:System.Windows.Media.FormattedText.BuildGeometry%2A> e <xref:System.Windows.Media.FormattedText.BuildHighlightGeometry%2A> per convertire il testo in oggetti <xref:System.Windows.Media.Geometry>.  Il primo metodo restituisce la geometria del testo formattato, mentre il secondo restituisce la geometria del riquadro delimitatore del testo formattato.  Nell'esempio di codice seguente viene illustrato come creare un oggetto <xref:System.Windows.Media.FormattedText> e recuperare le geometrie del testo formattato nonché il relativo riquadro delimitatore.  
  
 [!code-csharp[OutlineTextControlViewer#CreateText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#createtext)]
 [!code-vb[OutlineTextControlViewer#CreateText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#createtext)]  
  
 Per visualizzare gli oggetti <xref:System.Windows.Media.Geometry> recuperati, è necessario accedere all'oggetto <xref:System.Windows.Media.DrawingContext> dell'oggetto in cui viene visualizzato il testo convertito.  In questi esempi di codice, questa operazione viene eseguita creando un oggetto controllo personalizzato derivato da una classe che supporta il rendering definito dall'utente.  
  
 Per visualizzare oggetti <xref:System.Windows.Media.Geometry> nel controllo personalizzato, fornire un override per il metodo <xref:System.Windows.UIElement.OnRender%2A>.  È necessario che il metodo sottoposto a override utilizzi il metodo <xref:System.Windows.Media.DrawingContext.DrawGeometry%2A> per disegnare gli oggetti <xref:System.Windows.Media.Geometry>.  
  
 [!code-csharp[OutlineTextControlViewer#OnRender](../../../../samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#onrender)]
 [!code-vb[OutlineTextControlViewer#OnRender](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#onrender)]  
  
## Vedere anche  
 [Disegno di testo formattato](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)