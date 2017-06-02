---
title: "Utilizzo della trasformazione di tipo World | Microsoft Docs"
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
  - "grafica, trasformazione complessiva"
  - "trasformazione complessiva, esempi"
ms.assetid: 1e717711-1361-448e-aa49-0f3ec43110c9
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Utilizzo della trasformazione di tipo World
La trasformazione di tipo World è una proprietà della classe <xref:System.Drawing.Graphics>.  I numeri che specificano la trasformazione di tipo World sono memorizzati in un oggetto <xref:System.Drawing.Drawing2D.Matrix> che rappresenta una matrice 3x3.  Le classi <xref:System.Drawing.Drawing2D.Matrix> e <xref:System.Drawing.Graphics> contengono numerosi metodi per l'impostazione dei numeri nella matrice della trasformazione di tipo World.  
  
## Tipi di trasformazione diversi  
 Nel codice di esempio riportato di seguito viene creato un rettangolo 50x50 che viene quindi collocato in corrispondenza del punto di origine \(0, 0\).  Il punto di origine si trova in corrispondenza dell'angolo superiore sinistro dell'area client.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.MiscLegacyTopics#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#11)]  
  
 Nel codice che segue viene applicata una trasformazione di adattamento che estende il rettangolo di un fattore 1,75 sull'asse x e lo riduce di un fattore 0,5 sull'asse y:  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#12)]
 [!code-vb[System.Drawing.MiscLegacyTopics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#12)]  
  
 Il risultato è un rettangolo che, rispetto all'originale, è più lungo sull'asse x e più corto sull'asse y.  
  
 Per ruotare il rettangolo anziché adattarlo utilizzare il seguente codice:  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#13)]
 [!code-vb[System.Drawing.MiscLegacyTopics#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#13)]  
  
 Per effettuare la traslazione del rettangolo utilizzare il seguente codice:  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#14](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#14)]
 [!code-vb[System.Drawing.MiscLegacyTopics#14](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#14)]  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.Matrix>   
 [Sistemi di coordinate e trasformazioni](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [Utilizzo di trasformazioni nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-transformations-in-managed-gdi.md)