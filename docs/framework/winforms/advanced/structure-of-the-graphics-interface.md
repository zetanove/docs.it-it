---
title: "Struttura dell&#39;interfaccia grafica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "GDI+, mediante l'interfaccia gestita"
  - "grafica, struttura di classi"
ms.assetid: 010a1e46-656b-40a1-8d5d-87aa05ee1243
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Struttura dell&#39;interfaccia grafica
Nell'interfaccia di classe gestita di [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono contenute circa 60 classi, 50 enumerazioni e 8 strutture.  La classe <xref:System.Drawing.Graphics> è il fulcro delle funzionalità [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] poiché consente di tracciare effettivamente linee, curve, figure, immagini e testo.  
  
## Classi importanti  
 Numerose classi vengono utilizzate insieme alla classe <xref:System.Drawing.Graphics>.  Il metodo <xref:System.Drawing.Graphics.DrawLine%2A>, ad esempio, riceve un oggetto <xref:System.Drawing.Pen>, contenente gli attributi \(colore, spessore, stile del tratteggio e così via\) della linea da tracciare.  Il metodo <xref:System.Drawing.Graphics.FillRectangle%2A> può ricevere un puntatore a un oggetto <xref:System.Drawing.Drawing2D.LinearGradientBrush> che viene utilizzato insieme all'oggetto <xref:System.Drawing.Graphics> per riempire un rettangolo con un colore sfumato gradualmente in un altro colore.  Gli oggetti <xref:System.Drawing.Font> e <xref:System.Drawing.StringFormat> influenzano il modo in cui il testo viene tracciato dall'oggetto <xref:System.Drawing.Graphics>.  L'oggetto <xref:System.Drawing.Drawing2D.Matrix> memorizza e modifica la trasformazione di tipo World di un oggetto <xref:System.Drawing.Graphics>, che consente di ruotare e capovolgere le immagini e modificarne le proporzioni.  
  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili varie strutture \(ad esempio, <xref:System.Drawing.Rectangle>, <xref:System.Drawing.Point> e <xref:System.Drawing.Size>\) per l'organizzazione dei dati grafici.  Determinate classi vengono inoltre utilizzate principalmente come tipi di dati strutturati.  Ad esempio la classe <xref:System.Drawing.Imaging.BitmapData> funge da supporto per la classe <xref:System.Drawing.Bitmap> e la classe <xref:System.Drawing.Drawing2D.PathData> da supporto per la classe <xref:System.Drawing.Drawing2D.GraphicsPath>.  
  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono definite numerose enumerazioni, che sono costituite da raccolte di costanti correlate.  L'enumerazione <xref:System.Drawing.Drawing2D.LineJoin>, ad esempio, contiene gli elementi <xref:System.Drawing.Drawing2D.LineJoin>, <xref:System.Drawing.Drawing2D.LineJoin> e <xref:System.Drawing.Drawing2D.LineJoin>, che consentono di specificare gli stili disponibili per unire due linee.  
  
## Vedere anche  
 [Cenni preliminari sulla grafica](../../../../docs/framework/winforms/advanced/graphics-overview-windows-forms.md)   
 [Informazioni sul codice gestito GDI\+](../../../../docs/framework/winforms/advanced/about-gdi-managed-code.md)   
 [Utilizzo di classi grafiche gestite](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md)