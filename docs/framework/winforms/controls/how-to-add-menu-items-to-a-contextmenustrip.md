---
title: "Procedura: aggiungere voci di menu a un ContextMenuStrip | Microsoft Docs"
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
  - "menu di scelta rapida, aggiunta di voci di menu"
  - "ContextMenuStrips, aggiunta di voci di menu"
  - "menu di scelta rapida, aggiunta di elementi"
ms.assetid: 1ec14776-3ea2-4752-bd22-4fae0fd19e1a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: aggiungere voci di menu a un ContextMenuStrip
È possibile aggiungere una singola voce di menu o più voci contemporaneamente a un <xref:System.Windows.Forms.ContextMenuStrip>.  
  
### Per aggiungere una sola voce di menu a un ContextMenuStrip  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> per aggiungere una voce di menu a un <xref:System.Windows.Forms.ContextMenuStrip>.  
  
     \[Visual Basic\]  
  
    ```  
    Me.contextMenuStrip1.Items.Add(Me.toolStripMenuItem1)  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.Add(toolStripMenuItem1);  
    ```  
  
### Per aggiungere varie voci di menu a un ContextMenuStrip  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> per aggiungere più voci di menu a un <xref:System.Windows.Forms.ContextMenuStrip>.  
  
     \[Visual Basic\]  
  
    ```  
    Me.contextMenuStrip1.Items.AddRange(New _  
       System.Windows.Forms.ToolStripItem() {Me.toolStripMenuItem1, _  
          Me.toolStripMenuItem2})  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.AddRange(new   
       System.Windows.Forms.ToolStripItem[] {  
          this.toolStripMenuItem1, this.toolStripMenuItem2});  
    ```  
  
## Vedere anche  
 [Controllo ContextMenuStrip](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)