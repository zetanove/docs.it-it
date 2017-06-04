---
title: "Procedura: elencare i codificatori installati | Microsoft Docs"
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
  - "immagini (codec), elenco"
  - "immagini (codificatori), elenco"
ms.assetid: 49e8e4e9-7a67-42d9-86bf-08821cdc282e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: elencare i codificatori installati
Può essere opportuno elencare i decodificatori di immagini disponibili su un computer, per stabilire se l'applicazione li può salvare in un formato di file immagine particolare.  La classe <xref:System.Drawing.Imaging.ImageCodecInfo> fornisce metodi statici <xref:System.Drawing.Imaging.ImageCodecInfo.GetImageEncoders%2A> in modo da stabilire quali codificatori di immagini sono disponibili.  <xref:System.Drawing.Imaging.ImageCodecInfo.GetImageEncoders%2A> restituisce una matrice di oggetti <xref:System.Drawing.Imaging.ImageCodecInfo>.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato l'elenco dei codificatori installati e i relativi valori della proprietà.  
  
 [!code-csharp[UsingImageEncodersDecoders#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#1)]
 [!code-vb[UsingImageEncodersDecoders#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un'applicazione Windows Form.  
  
-   <xref:System.Windows.Forms.PaintEventArgs>, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: elencare i decodificatori installati](../../../../docs/framework/winforms/advanced/how-to-list-installed-decoders.md)   
 [Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)