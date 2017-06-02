---
title: "Procedura: convertire un&#39;immagine BMP in un&#39;immagine PNG | Microsoft Docs"
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
  - "BMP (immagini), conversione in PNG"
  - "formati di immagine, conversione"
ms.assetid: 9d4a692d-73ac-4ce3-9e05-9ec321e8fbd6
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: convertire un&#39;immagine BMP in un&#39;immagine PNG
Spesso può essere opportuno convertire un formato di file immagine in un altro.  È possibile eseguire questa conversione chiamando il metodo <xref:System.Drawing.Image.Save%2A> della classe <xref:System.Drawing.Image> e specificando l'oggetto <xref:System.Drawing.Imaging.ImageFormat> per il formato di file immagine desiderato.  
  
## Esempio  
 Nell'esempio seguente viene caricata un'immagine BMP da un tipo e quindi salvata nel formato PNG.  
  
 [!code-csharp[UsingImageEncodersDecoders#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#4)]
 [!code-vb[UsingImageEncodersDecoders#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#4)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Applicazione Windows Form.  
  
-   Un riferimento allo spazio dei nomi `System.Drawing.Imaging`.  
  
## Vedere anche  
 [Procedura: elencare i codificatori installati](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)   
 [Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)   
 [Tipi di bitmap](../../../../docs/framework/winforms/advanced/types-of-bitmaps.md)