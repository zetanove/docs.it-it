---
title: "Procedura: ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli | Microsoft Docs"
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
  - "DoubleBuffered (proprietà)"
  - "sfarfallio, riduzione in Windows Form"
  - "grafica, riduzione dello sfarfallio a doppio buffer"
ms.assetid: 91083d3a-653f-4f15-a467-0f37b2aa39d6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: ridurre lo sfarfallio nella grafica con il doppio buffering per form e controlli
Il doppio buffering utilizza una buffer di memoria per risolvere i problemi di sfarfallio associati a operazioni di disegno multiple.  Quando il doppio buffering è attivo, di tutte le operazioni di disegno viene eseguito il rendering anzitutto in un buffer di memoria anziché sull'area del disegno sullo schermo.  Una volta completate tutte le operazioni di disegno, il buffer di memoria viene copiato direttamente nell'area di disegno associata.  Dato che sullo schermo viene eseguita una sola operazione di tipo grafico, lo sfarfallio dell'immagine associato alle operazioni di disegno più complesse viene eliminato. Per la maggioranza delle applicazioni, il doppio buffering predefinito fornito da [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] determina i risultati ottimali.  I controlli standard di Windows Form sono a doppio buffering per impostazione predefinita.  È possibile attivare il doppio buffering predefinito nei form e nei controlli modificati in due modi.  È possibile impostare la proprietà <xref:System.Windows.Forms.Control.DoubleBuffered%2A> su `true`, oppure chiamare il metodo <xref:System.Windows.Forms.Control.SetStyle%2A> per impostare il flag <xref:System.Windows.Forms.ControlStyles> su `true`.  Entrambi i metodi attiveranno il doppio buffering predefinito per il form o controllo e forniranno un rendering della grafica privo di sfarfallio.  La chiamata del metodo <xref:System.Windows.Forms.Control.SetStyle%2A> è consigliata solo per i controlli personalizzati per i quali è stato scritto il codice di rendering.  
  
 Per scenari di doppio buffering più avanzati, ad esempio animazioni o gestione avanzata della memoria, è possibile implementare una logica di buffering doppio personalizzata.  Per ulteriori informazioni, vedere [Procedura: gestire manualmente le immagini memorizzate nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md).  
  
### Per ridurre lo sfarfallio  
  
-   Impostare la proprietà <xref:System.Windows.Forms.Control.DoubleBuffered%2A> su `true`.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#31)]  
  
 \- oppure \-  
  
-   Chiamare il metodo <xref:System.Windows.Forms.Control.SetStyle%2A> per impostare il flag <xref:System.Windows.Forms.ControlStyles> su `true`.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#32)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#32)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.DoubleBuffered%2A>   
 <xref:System.Windows.Forms.Control.SetStyle%2A>   
 [Grafica a doppio buffer](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)