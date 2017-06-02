---
title: "Procedura: utilizzare una classe Control Rendering | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "aspetto professionale, rendering di controlli Windows Form"
  - "stili visivi, rendering di controlli Windows Form"
  - "temi visivi, applicazione a controlli Windows Form"
ms.assetid: c0125e34-cd74-4c35-818c-3e40f462b0a3
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: utilizzare una classe Control Rendering
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Forms.ComboBoxRenderer> per eseguire il rendering della freccia a discesa di un controllo casella combinata.  L'esempio si basa sul metodo <xref:System.Windows.Forms.Control.OnPaint%2A> di un semplice controllo personalizzato.  La proprietà <xref:System.Windows.Forms.ComboBoxRenderer.IsSupported%2A?displayProperty=fullName> viene utilizzata per determinare se gli stili visivi vengono attivati nell'area client delle finestre dell'applicazione.  Se gli stili visivi sono attivi, il metodo <xref:System.Windows.Forms.ComboBoxRenderer.DrawDropDownButton%2A?displayProperty=fullName> esegue il rendering della freccia a discesa con gli stili visivi. Altrimenti il metodo <xref:System.Windows.Forms.ControlPaint.DrawComboButton%2A?displayProperty=fullName> esegue il rendering della freccia a discesa nello stile Windows classico.  
  
## Esempio  
 [!code-cpp[System.Windows.Forms_ControlRenderer#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/cpp/form1.cpp#10)]
 [!code-csharp[System.Windows.Forms_ControlRenderer#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/CS/form1.cs#10)]
 [!code-vb[System.Windows.Forms_ControlRenderer#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/VB/form1.vb#10)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo personalizzato derivato dalla classe <xref:System.Windows.Forms.Control>.  
  
-   Una classe <xref:System.Windows.Forms.Form> che contiene il controllo personalizzato.  
  
-   Riferimenti agli spazi dei nomi <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName>, <xref:System.Windows.Forms?displayProperty=fullName> e <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName>.  
  
## Vedere anche  
 [Rendering dei controlli con stili visivi](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)