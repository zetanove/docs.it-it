---
title: "Procedura: verificare l&#39;uguaglianza e la disuguaglianza di strutture Point4D | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "uguaglianza, verifica delle strutture Point4D"
  - "disuguaglianza, verifica delle strutture Point4D"
  - "Point 4D (strutture), verifica dell'uguaglianza"
  - "Point 4D (strutture), verifica della disuguaglianza"
  - "test, dell'uguaglianza nelle strutture Point4D"
  - "test, della disuguaglianza nelle strutture Point4D"
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: verificare l&#39;uguaglianza e la disuguaglianza di strutture Point4D
In questo esempio viene mostrato come verificare l'uguaglianza e la disuguaglianza delle strutture <xref:System.Windows.Media.Media3D.Point4D>.  
  
 Nell'esempio di codice seguente viene illustrato come verificare l'uguaglianza e la disuguaglianza delle strutture <xref:System.Windows.Media.Media3D.Point4D> utilizzando i metodi di uguaglianza <xref:System.Windows.Media.Media3D.Point4D>.  Viene eseguita la verifica dell'uguaglianza delle strutture <xref:System.Windows.Media.Media3D.Point4D> mediante l'operatore di overload di uguaglianza \(`==`\), quindi viene effettuata la verifica della disuguaglianza tramite l'operatore di overload di disuguaglianza \(`!=`\); infine viene eseguita la verifica dell'uguaglianza di una struttura <xref:System.Windows.Media.Media3D.Point3D> e di una struttura <xref:System.Windows.Media.Media3D.Point4D> mediante il metodo statico <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>.  
  
## Esempio  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>   
 <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>   
 <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>