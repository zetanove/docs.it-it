---
title: "Procedura: eseguire il rendering di un elemento dello stile visivo | Microsoft Docs"
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
  - "aspetto professionale, applicazione a elementi delle applicazioni Windows Form"
  - "stili visivi, rendering di controlli Windows Form"
  - "temi visivi, applicazione a elementi delle applicazioni Windows Form"
ms.assetid: a207781b-1baa-4ce9-b788-1e951bd4b5df
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: eseguire il rendering di un elemento dello stile visivo
Lo spazio dei nomi <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> espone gli oggetti <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> che rappresentano gli elementi dell'interfaccia utente \(UI, User Interface\) Windows supportati dagli stili visivi.  In questo argomento viene illustrato come utilizzare la classe <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> per eseguire il rendering della classe <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> che rappresenta i pulsanti **Disconnetti** e **Chiudi sessione** del menu Start.  
  
### Per eseguire il rendering di un elemento dello stile visivo  
  
1.  Creare una classe <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> e impostarla sull'elemento che si desidera disegnare.  Si noti l'uso della proprietà <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A?displayProperty=fullName> e del metodo <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.IsElementDefined%2A?displayProperty=fullName>: il costruttore <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.%23ctor%2A> genera un'eccezione se gli stili visivi sono disabilitati o un elemento non è definito.  
  
     [!code-cpp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/cpp/form1.cpp#4)]
     [!code-csharp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/VB/form1.vb#4)]  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.DrawBackground%2A> per eseguire il rendering dell'elemento rappresentato dalla classe <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer>.  
  
     [!code-cpp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/cpp/form1.cpp#6)]
     [!code-csharp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/VB/form1.vb#6)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo personalizzato derivato dalla classe <xref:System.Windows.Forms.Control>.  
  
-   Una classe <xref:System.Windows.Forms.Form> che contiene il controllo personalizzato.  
  
-   Riferimenti agli spazi dei nomi <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName>, <xref:System.Windows.Forms?displayProperty=fullName> e <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName>.  
  
## Vedere anche  
 [Rendering dei controlli con stili visivi](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)