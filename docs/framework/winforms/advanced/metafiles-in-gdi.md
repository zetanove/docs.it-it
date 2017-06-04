---
title: "Metafile in GDI+ | Microsoft Docs"
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
  - "GDI+, metafile"
  - "immagini [Windows Form], metafile"
  - "metafile"
ms.assetid: 51da872c-c783-440f-8bf6-1e580a966c31
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Metafile in GDI+
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è disponibile la classe <xref:System.Drawing.Imaging.Metafile> che consente la registrazione e la visualizzazione di metafile.  Un metafile, definito anche immagine vettoriale, è un'immagine memorizzata sotto forma di comandi e impostazioni di disegno.  È possibile archiviare nella memoria o salvare in un file o un flusso i comandi e le impostazioni registrati in un oggetto <xref:System.Drawing.Imaging.Metafile>.  
  
## Formati di metafile  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è consentita la visualizzazione dei metafile memorizzati nei formati seguenti:  
  
-   WMF\(Windows Metafile\)  
  
-   EMF\(Enhanced Metafile\)  
  
-   EMF\+  
  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile registrare metafile in formato EMF e EMF\+, ma non in formato WMF.  
  
 EMF\+ è un'estensione di EMF che consente la memorizzazione di registrazioni [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  Sono disponibili due variazioni del formato EMF\+: EMF\+ Only ed EMF\+ Dual.  I metafile EMF\+ Only contengono solo registrazioni [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  È possibile visualizzare tali metafile in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] ma non in [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  I metafile EMF\+ contengono solo registrazioni [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] e [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  Ogni registrazione [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] presente in un metafile EMF\+ Dual è associata a una registrazione [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] alternativa.  È possibile visualizzare tali metafile in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] o in [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  
  
 Nell'esempio seguente viene riportato un metafile precedentemente salvato come file.  L'angolo superiore sinistro del metafile viene visualizzato nella posizione \(100, 100\).  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#21)]  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)