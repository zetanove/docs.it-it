---
title: "Procedura: utilizzare la modalit&#224; di composizione per controllare la fusione alfa | Microsoft Docs"
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
  - "sfumatura alfa, composizione"
  - "colori, sfumatura"
  - "colori, controllo della trasparenza"
ms.assetid: f331df2d-b395-4b0a-95be-24fec8c9bbb5
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: utilizzare la modalit&#224; di composizione per controllare la fusione alfa
Possono verificarsi casi in cui è necessario creare un oggetto Bitmap fuori dallo schermo, con le caratteristiche che seguono:  
  
-   I colori hanno valori alfa inferiori a 255.  
  
-   Ai colori non viene applicata la fusione alfa quando si crea l'oggetto Bitmap.  
  
-   A momento della visualizzazione dell'immagine bitmap completata ai colori dell'immagine viene applicata la fusione alfa rispetto ai colori di sfondo sulla periferica di visualizzazione.  
  
 Per creare un'immagine bitmap con queste caratteristiche, costruire un oggetto <xref:System.Drawing.Bitmap> vuoto, quindi un oggetto <xref:System.Drawing.Graphics> basato sull'immagine.  Impostare la modalità di composizione dell'oggetto <xref:System.Drawing.Graphics> su <xref:System.Drawing.Drawing2D.CompositingMode?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio che segue viene creato un oggetto <xref:System.Drawing.Graphics> basato su un oggetto <xref:System.Drawing.Bitmap>.  L'oggetto <xref:System.Drawing.Graphics> viene utilizzato insieme a due pennelli semitrasparenti, con alfa \= 160, per colorare l'immagine bitmap.  Utilizzando i pennelli semitrasparenti un ellisse viene riempito di colore rosso e uno di colore verde.  L'ellisse di colore verde risulta sovrapposta a quella di colore rosso, ma il verde non viene sfumato con il rosso perché la modalità di composizione dell'oggetto <xref:System.Drawing.Graphics> è impostata su <xref:System.Drawing.Drawing2D.CompositingMode>.  
  
 L'immagine bitmap viene disegnata due volte sullo schermo: una volta su sfondo bianco e una volta su sfondo multicolore.  I pixel dell'immagine bitmap che sono parte dei due ellissi hanno una componente alfa pari a 160, perciò gli ellissi risultano sfumati con i colori di sfondo dello schermo.  
  
 Nell'illustrazione che segue si mostra l'output del codice.  Si noti che le ellissi sono sfumate rispetto allo sfondo, ma non l'una rispetto alle altre.  
  
 ![Copia origine](../../../../docs/framework/winforms/advanced/media/sourcecopy.png "sourcecopy")  
  
 Il codice di esempio contiene l'istruzione seguente:  
  
 [!code-csharp[System.Drawing.AlphaBlending#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.AlphaBlending#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#41)]  
  
 Per fare in modo che le ellissi siano sfumate l'una rispetto alle altre nonché rispetto allo sfondo modificare l'istruzione nel modo seguente:  
  
 [!code-csharp[System.Drawing.AlphaBlending#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#42)]
 [!code-vb[System.Drawing.AlphaBlending#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#42)]  
  
 Nell'illustrazione che segue si mostra l'output del codice modificato.  
  
 ![Over origine](../../../../docs/framework/winforms/advanced/media/sourceover.png "sourceover")  
  
 [!code-csharp[System.Drawing.AlphaBlending#43](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#43)]
 [!code-vb[System.Drawing.AlphaBlending#43](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#43)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e` un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 <xref:System.Drawing.Color.FromArgb%2A>   
 [Linee e riempimenti con fusione alfa](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)