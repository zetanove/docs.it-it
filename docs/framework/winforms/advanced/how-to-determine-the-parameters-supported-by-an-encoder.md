---
title: "Procedura: determinare i parametri supportati da un codificatore | Microsoft Docs"
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
  - "codificatore (parametri), determinazione del supporto"
ms.assetid: f47ae459-e3ce-4d41-a140-2f6c6aea3f44
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: determinare i parametri supportati da un codificatore
È possibile modificare i parametri delle immagini, come ad esempio la qualità e il livello di compressione, ma è necessario conoscere i parametri supportati da un codificatore di immagini specificato.  La classe <xref:System.Drawing.Image> fornisce il metodo <xref:System.Drawing.Image.GetEncoderParameterList%2A> in modo da determinare quali parametri di immagini sono supportati per un codificatore particolare.  Specificare il codificatore con un GUID.  Il metodo <xref:System.Drawing.Image.GetEncoderParameterList%2A> restituisce una matrice di oggetti <xref:System.Drawing.Imaging.EncoderParameter>.  
  
## Esempio  
 Nel codice di esempio seguente vengono illustrati i parametri supportati per il codificatore JPEG.  Utilizzare l'elenco delle categorie di parametri e i GUIDs associati nei cenni preliminari sulle classi <xref:System.Drawing.Imaging.Encoder> per stabilire la categoria per ogni parametro.  
  
 [!code-csharp[UsingImageEncodersDecoders#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#3)]
 [!code-vb[UsingImageEncodersDecoders#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#3)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un'applicazione Windows Form.  
  
-   <xref:System.Windows.Forms.PaintEventArgs>, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: elencare i codificatori installati](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)   
 [Tipi di bitmap](../../../../docs/framework/winforms/advanced/types-of-bitmaps.md)   
 [Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)