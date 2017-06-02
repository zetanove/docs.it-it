---
title: "Procedura: eseguire l&#39;hit testing utilizzando una regione | Microsoft Docs"
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
  - "hit test, utilizzo delle aree"
  - "aree, test delle occorrenze"
ms.assetid: 3a4c07cb-a40a-4d14-ad35-008f531910a8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: eseguire l&#39;hit testing utilizzando una regione
Lo scopo della verifica passaggio è determinare se il cursore si trova sopra un determinato oggetto, ad esempio un'icona o un pulsante.  
  
## Esempio  
 Nell'esempio che segue si crea un'area a forma di segno più tramite l'unione di due aree rettangolari.  Si supponga che la variabile  `point`  contenga la posizione del clic più recente.  Verrà verificato se  `point`  si trova nella regione a forma di segno più.  Se il punto si trova all'interno dell'area, il che corrisponde a un passaggio, questa verrà riempita con colore rosso opaco.  In caso contrario l'area verrà riempita con colore rosso semitrasparente.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.MiscLegacyTopics#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#31)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 <xref:System.Drawing.Region>   
 [Regioni in GDI\+](../../../../docs/framework/winforms/advanced/regions-in-gdi.md)   
 [Procedura: definire l'area di visualizzazione utilizzando una regione](../../../../docs/framework/winforms/advanced/how-to-use-clipping-with-a-region.md)