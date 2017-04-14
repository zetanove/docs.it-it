---
title: "Procedura: implementare un oggetto ToolStripRenderer personalizzato | Microsoft Docs"
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
  - "barre degli strumenti [Windows Form]"
  - "ToolStrip (controllo) [Windows Form]"
  - "ToolStripRenderer (classe)"
ms.assetid: c66fd3f7-2377-4553-8f1b-006527f08f32
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: implementare un oggetto ToolStripRenderer personalizzato
È possibile personalizzare l'aspetto di un controllo <xref:System.Windows.Forms.ToolStrip> implementando una classe che deriva da <xref:System.Windows.Forms.ToolStripRenderer>.  In questo modo è possibile creare un aspetto differente da quello fornito dalle classi <xref:System.Windows.Forms.ToolStripProfessionalRenderer> e <xref:System.Windows.Forms.ToolStripSystemRenderer>.  
  
## Esempio  
 L'esempio di codice seguente illustra come implementare una classe <xref:System.Windows.Forms.ToolStripRenderer> personalizzata.  In questo esempio, il controllo `GridStrip` implementa un puzzle con elementi scorrevoli, che consente all'utente di spostare gli elementi in un layout di tabella allo scopo di formare un'immagine.  Un controllo <xref:System.Windows.Forms.ToolStrip> personalizzato dispone i relativi controlli <xref:System.Windows.Forms.ToolStripButton> in un layout di griglia  contenente un'unica cella vuota, nella quale l'utente può spostare un elemento adiacente mediante una semplice operazione di trascinamento.  Gli elementi che possono essere spostati vengono evidenziati.  
  
 La classe `GridStripRenderer` consente di definire tre componenti relativi all'aspetto del controllo `GridStrip`:  
  
-   Bordo di `GridStrip`  
  
-   Bordo di <xref:System.Windows.Forms.ToolStripButton>  
  
-   immagine di <xref:System.Windows.Forms.ToolStripButton>  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.GridStrip#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.GridStrip/CS/GridStrip.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.GridStrip#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.GridStrip/VB/GridStrip.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripRenderer>   
 <xref:System.Windows.Forms.ToolStripProfessionalRenderer>   
 <xref:System.Windows.Forms.ToolStripSystemRenderer>   
 <xref:System.Windows.Forms.StatusStrip>   
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)