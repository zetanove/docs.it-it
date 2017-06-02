---
title: "Importanza dell&#39;ordine delle trasformazioni | Microsoft Docs"
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
  - "trasformazioni, significato dell'ordine"
ms.assetid: 37d5f9dc-a5cf-4475-aa5d-34d714e808a9
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Importanza dell&#39;ordine delle trasformazioni
In un singolo oggetto <xref:System.Drawing.Drawing2D.Matrix> è possibile memorizzare un'unica trasformazione o una sequenza di trasformazioni.  Quest'ultima è chiamata trasformazione composita.  La matrice di una trasformazione composita viene ottenuta moltiplicando le matrici di trasformazioni singole.  
  
## Esempi di trasformazione composita  
 In una trasformazione composita è importante l'ordine delle singole trasformazioni.  Se ad esempio si esegue prima una rotazione, poi un adattamento e quindi una traslazione si ottiene un risultato diverso da quello che si otterrebbe effettuando prima una traslazione, poi una rotazione e infine un adattamento.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] le trasformazioni composite sono compilate da sinistra a destra.  Se S, R e T sono rispettivamente matrici di adattamento, rotazione e traslazione, la sequenza SRT \(in quest'ordine\) è la matrice della trasformazione composita che prima effettua l'adattamento, poi la rotazione, poi la traslazione.  La matrice prodotta dalla sequenza SRT è diversa dalla matrice prodotta dalla sequenza TRS.  
  
 Un motivo di rilevanza dell'ordine è che le trasformazioni, come rotazione e adattamento, vengono effettuate rispetto all'origine del sistema di coordinate.  Il ridimensionamento di un oggetto centrato rispetto all'origine produce un risultato diverso dal ridimensionamento di un oggetto spostato rispetto all'origine.  Analogamente, la rotazione di un oggetto centrato rispetto all'origine produce un risultato diverso dalla rotazione di un oggetto spostato rispetto all'origine.  
  
 Nell'esempio che segue si uniscono, nell'ordine, adattamento, rotazione e traslazione per formare una trasformazione composita.  L'argomento <xref:System.Drawing.Drawing2D.MatrixOrder> passato al metodo <xref:System.Drawing.Graphics.RotateTransform%2A> indica che la rotazione sarà successiva all'adattamento.  Analogamente, l'argomento <xref:System.Drawing.Drawing2D.MatrixOrder> passato al metodo <xref:System.Drawing.Graphics.TranslateTransform%2A> indica che la traslazione sarà successiva alla rotazione.  <xref:System.Drawing.Drawing2D.MatrixOrder> e <xref:System.Drawing.Drawing2D.MatrixOrder> sono membri dell'enumerazione <xref:System.Drawing.Drawing2D.MatrixOrder>.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.MiscLegacyTopics#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#21)]  
  
 Nell'esempio che segue vengono eseguite le stesse chiamate di metodo utilizzate nell'esempio precedente, ma con ordine inverso.  L'ordine delle operazioni è traslazione, rotazione e quindi adattamento, con un risultato molto diverso dalla sequenza adattamento, rotazione, traslazione.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.MiscLegacyTopics#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#22)]  
  
 Un modo per invertire l'ordine delle singole trasformazioni in una trasformazione composita è rappresentato dall'inversione dell'ordine di una sequenza di chiamate di metodo.  Un secondo modo per controllare l'ordine delle operazioni è dato dalla modifica dell'argomento dell'ordine della matrice.  L'esempio riportato di seguito si distingue dal precedente solo per il cambiamento di <xref:System.Drawing.Drawing2D.MatrixOrder> in <xref:System.Drawing.Drawing2D.MatrixOrder>.  La moltiplicazione della matrice viene effettuata nell'ordine SRT, dove S, R e T sono, rispettivamente, le matrici per adattamento, rotazione e traslazione.  L'ordine della trasformazione composita è adattamento, rotazione, traslazione.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.MiscLegacyTopics#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#23)]  
  
 Il risultato dell'esempio precedente è identico a quello del primo esempio della sezione,  poiché è stato invertito sia l'ordine delle chiamate di metodo sia l'ordine di moltiplicazione delle matrici.  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.Matrix>   
 [Sistemi di coordinate e trasformazioni](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [Utilizzo di trasformazioni nel codice gestito GDI\+](../../../../docs/framework/winforms/advanced/using-transformations-in-managed-gdi.md)