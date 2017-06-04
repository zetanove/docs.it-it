---
title: "Procedura: utilizzare la modalit&#224; di interpolazione per controllare la qualit&#224; dell&#39;immagine durante l&#39;adattamento | Microsoft Docs"
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
  - "immagini [Windows Form], controllo della qualità"
  - "immagini [Windows Form], adattamento"
  - "modalità di interpolazione, controllo della qualità dell'immagine"
ms.assetid: fde9bccf-8aa5-4b0d-ba4b-788740627b02
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: utilizzare la modalit&#224; di interpolazione per controllare la qualit&#224; dell&#39;immagine durante l&#39;adattamento
La modalità di interpolazione di un oggetto <xref:System.Drawing.Graphics> determina il modo in cui gli oggetti vengono adattati, tramite estensione o riduzione, in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  Nell'enumerazione <xref:System.Drawing.Drawing2D.InterpolationMode> sono definite numerose modalità di interpolazione, alcune delle quali sono indicate nell'elenco che segue:  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
-   <xref:System.Drawing.Drawing2D.InterpolationMode>  
  
 Per estendere un'immagine ciascun pixel nell'immagine originale deve essere mappato rispetto a un gruppo di pixel dell'immagine più grande.  Per ridurre un'immagine i gruppi di pixel dell'immagine originale devono essere mappati rispetto a singoli pixel dell'immagine più piccola.  La qualità dell'immagine adattata dipende dall'efficacia degli algoritmi che eseguono le associazioni.  Gli algoritmi che producono immagini adattate di qualità elevata richiedono solitamente maggiori tempi di elaborazione.  Nell'elenco precedente <xref:System.Drawing.Drawing2D.InterpolationMode> rappresenta la modalità con qualità più bassa e <xref:System.Drawing.Drawing2D.InterpolationMode> la modalità con qualità più elevata.  
  
 Per impostare la modalità di interpolazione, assegnare uno dei membri dell'enumerazione <xref:System.Drawing.Drawing2D.InterpolationMode> alla proprietà <xref:System.Drawing.Graphics.InterpolationMode%2A> di un oggetto <xref:System.Drawing.Graphics>.  
  
## Esempio  
 Nell'esempio che segue viene disegnata un'immagine, che successivamente viene ridotta utilizzando tre diverse modalità di interpolazione.  
  
 Nell'illustrazione che segue sono mostrate l'immagine originale e le tre immagini più piccole.  
  
 ![Immagine con varie impostazioni di interpolazione](../../../../docs/framework/winforms/advanced/media/csgrapes1.png "csgrapes1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#81](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#81)]
 [!code-vb[System.Drawing.WorkingWithImages#81](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#81)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)