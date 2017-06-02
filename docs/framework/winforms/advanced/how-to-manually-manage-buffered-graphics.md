---
title: "Procedura: gestire manualmente le immagini memorizzate nel buffer | Microsoft Docs"
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
  - "classe BufferedGraphicsContext"
  - "sfarfallio, riduzione mediante la gestione manuale della grafica"
  - "grafica, gestione della memorizzazione nel buffer"
ms.assetid: 4c2a90ee-bbbe-4ff6-9170-1b06c195c918
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: gestire manualmente le immagini memorizzate nel buffer
Per scenari di buffering doppio più avanzati, è possibile utilizzare le classi di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per implementare una logica di buffering doppio personalizzata.  La classe responsabile per l'allocazione e la gestione dei singoli buffer grafici è la classe <xref:System.Drawing.BufferedGraphicsContext>.  Ogni applicazione dispone di un proprio oggetto <xref:System.Drawing.BufferedGraphicsContext> predefinito che gestisce la totalità del buffering doppio predefinito per l'applicazione.  È possibile recuperare un riferimento all'istanza chiamando la proprietà <xref:System.Drawing.BufferedGraphicsManager.Current%2A>.  
  
### Per ottenere un riferimento a BufferedGraphicsContext predefinito  
  
-   Impostare la proprietà <xref:System.Drawing.BufferedGraphicsManager.Current%2A>, come illustrato nell'esempio di codice seguente.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#11)]  
  
    > [!NOTE]
    >  Non è necessario chiamare il metodo `Dispose` sul riferimento <xref:System.Drawing.BufferedGraphicsContext> ricevuto dalla classe <xref:System.Drawing.BufferedGraphicsManager>.  L'oggetto <xref:System.Drawing.BufferedGraphicsManager> gestisce totalmente l'allocazione e la distribuzione della memoria per le istanze <xref:System.Drawing.BufferedGraphicsContext> predefinite.  
  
     Per applicazioni a elevato contenuto grafico, ad esempio animazioni, è a volte possibile migliorare le prestazioni utilizzando un oggetto <xref:System.Drawing.BufferedGraphicsContext> anziché l'oggetto <xref:System.Drawing.BufferedGraphicsContext> fornito da <xref:System.Drawing.BufferedGraphicsManager>.  Questo consente di creare e gestire singolarmente i buffer grafici, senza ottenere una riduzione delle prestazioni derivante dalla gestione di tutti gli altri buffer grafici associati all'applicazione, sebbene la memoria utilizzata dall'applicazione sia superiore.  
  
### Per creare un BufferedGraphicsContext dedicato  
  
-   Dichiarare e creare una nuova istanza della classe <xref:System.Drawing.BufferedGraphicsContext>, come illustrato nell'esempio di codice seguente.  
  
     [!code-csharp[System.Windows.Forms.LegacyBufferedGraphics#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.LegacyBufferedGraphics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.LegacyBufferedGraphics/VB/Class1.vb#12)]  
  
## Vedere anche  
 <xref:System.Drawing.BufferedGraphicsContext>   
 [Grafica a doppio buffer](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)   
 [Procedura: eseguire il rendering manuale di grafica memorizzata nel buffer](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)