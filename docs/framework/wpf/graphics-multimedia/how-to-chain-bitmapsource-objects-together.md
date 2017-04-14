---
title: "Procedura: concatenare gli oggetti BitmapSource | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "BitmapSource (oggetti), concatenazione"
  - "concatenazione di oggetti BitmapSource"
  - "grafica, concatenazione di oggetti BitmapSource"
ms.assetid: 32d88853-395b-4855-9685-51a482a3b421
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: concatenare gli oggetti BitmapSource
In questo esempio viene illustrato come applicare una varietà di effetti a un'origine di immagine concatenando più oggetti <xref:System.Windows.Media.Imaging.BitmapSource> derivati.  
  
 Nell'esempio riportato di seguito viene utilizzata la concatenazione per capovolgere e modificare il formato di pixel dell'origine di un'immagine.  
  
## Esempio  
 [!code-xml[ImagingSnippetGallery_snip#ChainedBitmapSourcesXamlExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_snip/CS/ChainedBitmapSourcesExample.xaml#chainedbitmapsourcesxamlexamplewholepage)]  
  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#ChainedBitmapSourcesCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/ChainedBitmapSourcesExample.cs#chainedbitmapsourcescodeexamplewholepage)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#ChainedBitmapSourcesCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/ChainedBitmapSourcesExample.vb#chainedbitmapsourcescodeexamplewholepage)]