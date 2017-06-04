---
title: "Procedura: elencare i decodificatori installati | Microsoft Docs"
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
  - "immagini (decoder), elenco"
ms.assetid: 11417191-8c95-40ca-8024-779e61706fb6
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: elencare i decodificatori installati
Può essere opportuno elencare i decodificatori di immagini disponibili sul computer per determinare se l'applicazione può leggere un particolare formato di file immagine.  La classe <xref:System.Drawing.Imaging.ImageCodecInfo> fornisce metodi statici <xref:System.Drawing.Imaging.ImageCodecInfo.GetImageDecoders%2A> in modo da stabilire quali decodificatori di immagini sono disponibili.  <xref:System.Drawing.Imaging.ImageCodecInfo.GetImageDecoders%2A> restituisce una matrice di oggetti <xref:System.Drawing.Imaging.ImageCodecInfo>.  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato l'elenco dei decodificatori installati e i relativi valori della proprietà.  
  
 [!code-csharp[UsingImageEncodersDecoders#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#2)]
 [!code-vb[UsingImageEncodersDecoders#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#2)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un'applicazione Windows Form.  
  
-   <xref:System.Windows.Forms.PaintEventArgs>, ovvero un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Procedura: elencare i codificatori installati](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)   
 [Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-image-encoders-and-decoders-in-managed-gdi.md)