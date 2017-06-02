---
title: "Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI+ | Microsoft Docs"
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
  - "immagini (decoder), utilizzo"
  - "immagini (codificatori), utilizzo"
ms.assetid: 0e838ea1-4e7e-4334-b882-ab25df607b8b
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Utilizzo di codificatori e decodificatori di immagini nel codice gestito GDI+
Lo spazio dei nomi <xref:System.Drawing> fornisce le classi <xref:System.Drawing.Image> e <xref:System.Drawing.Bitmap> per l’archiviazione e la modifica delle immagini.  Utilizzando i codificatori di immagini in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile scrivere le immagini dalla memoria sul disco. Utilizzando i decodificatori di immagini in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], è possibile caricare le immagini dal disco nella memoria.  Un decodificatore converte i dati di un oggetto <xref:System.Drawing.Image>o <xref:System.Drawing.Bitmap> in un determinato formato di file su disco.  Un decodificatore converte i dati di un file su disco nel formato richiesto dagli oggetti <xref:System.Drawing.Image>e <xref:System.Drawing.Bitmap>.  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] dispone di codificatori e decodificatori incorporati che supportano i seguenti tipi di file:  
  
-   BMP  
  
-   GIF  
  
-   JPEG  
  
-   PNG  
  
-   TIFF  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] dispone di decodificatori incorporati che supportano i seguenti tipi di file:  
  
-   WMF  
  
-   EMF  
  
-   Icona  
  
 Negli argomenti seguenti vengono descritti più dettagliatamente i codificatori e i decodificatori:  
  
## In questa sezione  
 [Procedura: elencare i codificatori installati](../../../../docs/framework/winforms/advanced/how-to-list-installed-encoders.md)  
 Viene descritto come elencare i codificatori disponibili in un computer.  
  
 [Procedura: elencare i decodificatori installati](../../../../docs/framework/winforms/advanced/how-to-list-installed-decoders.md)  
 Viene descrive come elencare i decodificatori disponibili in un computer.  
  
 [Procedura: determinare i parametri supportati da un codificatore](../../../../docs/framework/winforms/advanced/how-to-determine-the-parameters-supported-by-an-encoder.md)  
 Viene descritto come elencare l'oggetto <xref:System.Drawing.Imaging.EncoderParameters> supportato da un codificatore.  
  
 [Procedura: convertire un'immagine BMP in un'immagine PNG](../../../../docs/framework/winforms/advanced/how-to-convert-a-bmp-image-to-a-png-image.md)  
 Viene descritto come salvare un'immagine in un formato immagine diverso.  
  
 [Procedura: impostare il livello di compressione JPEG](../../../../docs/framework/winforms/advanced/how-to-set-jpeg-compression-level.md)  
 Viene descritto come modificare il livello di qualità di un'immagine.  
  
## Riferimenti  
 <xref:System.Drawing.Image>  
  
 <xref:System.Drawing.Bitmap>  
  
 <xref:System.Drawing.Imaging.ImageCodecInfo>  
  
 <xref:System.Drawing.Imaging.EncoderParameter>  
  
 <xref:System.Drawing.Imaging.Encoder>  
  
## Sezioni correlate  
 [Informazioni sul codice gestito GDI\+](../../../../docs/framework/winforms/advanced/about-gdi-managed-code.md)  
  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)