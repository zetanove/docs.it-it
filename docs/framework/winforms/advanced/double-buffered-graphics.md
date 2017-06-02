---
title: "Grafica a doppio buffer | Microsoft Docs"
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
  - "doppio buffer"
  - "esempi [Windows Form], grafica a doppio buffer"
  - "sfarfallio, riduzione con doppio buffer"
  - "grafica, a doppio buffer"
ms.assetid: 4f6fef99-0972-436e-9d73-0167e4033f71
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Grafica a doppio buffer
Lo sfarfallio è un problema comune nella programmazione di grafica.  Le operazioni di tipo grafico che richiedono più operazioni di disegno complesse possono determinare un apparente sfarfallio delle immagini visualizzate oppure attribuire loro un aspetto non accettabile.  Per risolvere questi problemi, .NET Framework consente di accedere al doppio buffering.  
  
 Il doppio buffering utilizza una buffer di memoria per risolvere i problemi di sfarfallio associati a operazioni di disegno multiple.  Quando il doppio buffering è attivo, di tutte le operazioni di disegno viene eseguito il rendering anzitutto in un buffer di memoria anziché sull'area del disegno sullo schermo.  Una volta completate tutte le operazioni di disegno, il buffer di memoria viene copiato direttamente nell'area di disegno associata.  Dato che sullo schermo viene eseguita una sola operazione di tipo grafico, lo sfarfallio dell'immagine associato alle operazioni di disegno più complesse viene eliminato.  
  
## Doppio buffering predefinito  
 Il modo più rapido per utilizzare il doppio buffering nelle applicazioni è applicare il doppio buffering predefinito per form e controlli fornito da .NET Framework.  È possibile attivare il doppio buffering predefinito per Windows Form e controlli modificati per Windows impostando la proprietà <xref:System.Windows.Forms.Control.DoubleBuffered%2A> su `true` oppure utilizzando il metodo <xref:System.Windows.Forms.Control.SetStyle%2A>.  Per ulteriori informazioni, vedere [Procedura: ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli](../../../../docs/framework/winforms/advanced/how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md).  
  
## Gestione manuale della grafica memorizzata nel buffer  
 Per scenari di doppio buffering più avanzati, ad esempio animazioni o gestione avanzata della memoria, è possibile utilizzare le classi .NET Framework per implementare una logica di buffering doppio personalizzata.  La classe responsabile per l'allocazione e la gestione dei singoli buffer grafici è la classe <xref:System.Drawing.BufferedGraphicsContext>.  Ogni applicazione dispone di una propria istanza di <xref:System.Drawing.BufferedGraphicsContext> che gestisce la totalità del buffering doppio predefinito per l'applicazione.  Nella maggioranza dei casi per ogni applicazione sarà disponibile un unico dominio, quindi generalmente per ogni applicazione sarà presente un oggetto <xref:System.Drawing.BufferedGraphicsContext> predefinito.  Le istanze <xref:System.Drawing.BufferedGraphicsContext> predefinite vengono gestite dalla classe <xref:System.Drawing.BufferedGraphicsManager>.  È possibile recuperare un riferimento all'istanza di <xref:System.Drawing.BufferedGraphicsContext> predefinita chiamando la [proprietà BufferedGraphicsManager.Current](frlrfSystemDrawingBufferedGraphicsManagerClassCurrentTopic).  È inoltre possibile creare un'istanza di <xref:System.Drawing.BufferedGraphicsContext> dedicata, che consente di migliorare le prestazioni in applicazioni a elevato contenuto grafico.  Per informazioni su come creare un'istanza di <xref:System.Drawing.BufferedGraphicsContext>, vedere [Procedura: gestire manualmente le immagini memorizzate nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md).  
  
## Visualizzazione manuale della grafica memorizzata nel buffer  
 È possibile utilizzare un'istanza della classe <xref:System.Drawing.BufferedGraphicsContext> per creare buffer per grafica chiamando il [metodo BufferedGraphicsContext.Allocate](frlrfSystemDrawingBufferedGraphicsContextClassAllocateTopic), che restituisce un'istanza della classe <xref:System.Drawing.BufferedGraphics>.  Un oggetto <xref:System.Drawing.BufferedGraphics> gestisce un buffer di memoria associato a una superficie di rendering, ad esempio un form o un controllo.  
  
 Dopo la creazione dell'istanza, la classe <xref:System.Drawing.BufferedGraphics> gestisce il rendering in un buffer grafico in memoria.  È possibile eseguire il rendering di grafica nel buffer di memoria tramite la [proprietà BufferedGraphics.Graphics](frlrfSystemDrawingBufferedGraphicsClassGraphicsTopic), che espone un oggetto <xref:System.Drawing.Graphics> che rappresenta direttamente il buffer di memoria.  È possibile disegnare in questo oggetto <xref:System.Drawing.Graphics> esattamente come si farebbe con un oggetto <xref:System.Drawing.Graphics> che rappresenta un'area di disegno.  Una volta disegnati gli elementi grafici nel buffer, è possibile utilizzare il [metodo BufferedGraphics.Render](frlrfSystemDrawingBufferedGraphicsClassRenderTopic) per copiare il contenuto del buffer nell'area di disegno sullo schermo.  
  
 Per ulteriori informazioni sull'utilizzo della classe <xref:System.Drawing.BufferedGraphics>, vedere [Rendering manuale di grafica memorizzata nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md).  Per ulteriori informazioni sul rendering di elementi grafici, vedere [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)  
  
## Vedere anche  
 <xref:System.Drawing.BufferedGraphics>   
 <xref:System.Drawing.BufferedGraphicsContext>   
 <xref:System.Drawing.BufferedGraphicsManager>   
 [Procedura: eseguire il rendering manuale di grafica memorizzata nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)   
 [Procedura: ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli](../../../../docs/framework/winforms/advanced/how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md)   
 [Procedura: gestire manualmente le immagini memorizzate nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)