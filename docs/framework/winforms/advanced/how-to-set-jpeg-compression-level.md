---
title: "Procedura: impostare il livello di compressione JPEG | Microsoft Docs"
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
  - "immagini [Windows Form], modifica dei parametri del codificatore"
  - "JPEG (immagini), impostazione del livello di qualità"
ms.assetid: 4b9a74e3-9504-43c1-9f28-ace651d0772e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: impostare il livello di compressione JPEG
Può essere opportuno modificare i parametri di un'immagine quando questa viene salvata sul disco per ridurre la dimensione del file o migliorarne la qualità.  È possibile regolare la qualità di un’immagine JEPG modificandone il livello di compressione.  Per specificare il livello di compressione quando si salva un'immagine JEPG, è necessario creare un oggetto <xref:System.Drawing.Imaging.EncoderParameters> e passarlo al metodo <xref:System.Drawing.Image.Save%2A> della classe <xref:System.Drawing.Image> .  Inizializzare l'oggetto <xref:System.Drawing.Imaging.EncoderParameters> in modo che disponga di una matrice costituita da un oggetto <xref:System.Drawing.Imaging.EncoderParameter>.  Quando si crea <xref:System.Drawing.Imaging.EncoderParameter>, specificare il codificatore <xref:System.Drawing.Imaging.Encoder.Quality> e il livello di compressione desiderato.  
  
## Esempio  
 Nel codice di esempio seguente viene creato un oggetto <xref:System.Drawing.Imaging.EncoderParameter> e vengono salvate tre immagini JEPG.  Ogni immagine JEPG viene salvata con un livello di qualità diverso, modificando il valore `long` passato al <xref:System.Drawing.Imaging.EncoderParameter> costruttore.  Un livello di qualità 0 corrisponde alla compressione maggiore mentre un livello di qualità 100 corrisponde alla compressione minore.  
  
 [!code-csharp[UsingImageEncodersDecoders#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#8)]
 [!code-vb[UsingImageEncodersDecoders#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#8)]  
[!code-csharp[UsingImageEncodersDecoders#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#6)]
[!code-vb[UsingImageEncodersDecoders#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#6)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un'applicazione Windows Form.  
  
-   <xref:System.Windows.Forms.PaintEventArgs>, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
-   Un file immagine denominato `TestPhoto.jpg` e archiviato in **c:\\**.  
  
## Vedere anche  
 [Procedura: determinare i parametri supportati da un codificatore](../../../../docs/framework/winforms/advanced/how-to-determine-the-parameters-supported-by-an-encoder.md)   
 [Tipi di bitmap](../../../../docs/framework/winforms/advanced/types-of-bitmaps.md)   
 [Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)