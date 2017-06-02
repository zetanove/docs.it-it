---
title: "Procedura: creare e impostare un renderer personalizzato per il controllo ToolStrip in Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], barre degli strumenti"
  - "barre degli strumenti [Windows Form], rendering"
  - "ToolStrip (controllo) [Windows Form], rendering personalizzato"
  - "ToolStrip (controllo) [Windows Form], rendering"
ms.assetid: 88a804ba-679f-4ba3-938a-0dc396199c5b
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: creare e impostare un renderer personalizzato per il controllo ToolStrip in Windows Form
I controlli <xref:System.Windows.Forms.ToolStrip> forniscono un semplice supporto per temi e stili.  Per ottenere un aspetto e un comportamento completamente personalizzati, impostare la proprietà <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=fullName> o la proprietà <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=fullName> su un renderer personalizzato.  
  
 È possibile assegnare renderer a ogni singolo controllo <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip>, <xref:System.Windows.Forms.ContextMenuStrip> o <xref:System.Windows.Forms.StatusStrip> oppure è possibile utilizzare la proprietà <xref:System.Windows.Forms.ToolStripManager.Renderer%2A> per influenzare tutti gli oggetti impostando la proprietà <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=fullName> su <xref:System.Windows.Forms.ToolStripRenderMode?displayProperty=fullName>.  
  
> [!NOTE]
>  La proprietà <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> restituisce <xref:System.Windows.Forms.ToolStripRenderMode> solo se il valore della proprietà <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=fullName> è diverso da `null`.  
  
### Per creare un renderer personalizzato  
  
1.  Estendere la classe <xref:System.Windows.Forms.ToolStripRenderer>.  
  
2.  Implementare il rendering personalizzato desiderato eseguendo l'override di membri *On…* appropriati.  
  
    ```vb  
    Public Class RedTextRenderer  
        Inherits System.Windows.Forms.ToolStripRenderer  
        Protected Overrides Sub OnRenderItemText(ByVal e As _  
            ToolStripItemTextRenderEventArgs)   
            e.TextColor = Color.Red  
            e.TextFont = New Font("Helvetica", 7, FontStyle.Bold)  
            MyBase.OnRenderItemText(e)  
        End Sub  
    End Class  
  
    ```  
  
     \[C\#\]  
  
    ```  
    public class RedTextRenderer : _  
        System.Windows.Forms.ToolStripRenderer  
    {  
        protected override void _  
            OnRenderItemText(ToolStripItemTextRenderEventArgs e)  
        {  
            e.TextColor = Color.Red;  
            e.TextFont = new Font("Helvetica", 7, FontStyle.Bold);  
           base.OnRenderItemText(e);  
        }  
    }  
  
    ```  
  
### Per impostare come corrente il renderer personalizzato  
  
1.  Per impostare il renderer personalizzato per un <xref:System.Windows.Forms.ToolStrip>, impostare la proprietà <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=fullName> sul renderer personalizzato.  
  
    ```vb  
    toolStrip1.Renderer = New RedTextRenderer()  
  
    ```  
  
     \[C\#\]  
  
    ```  
    toolStrip1.Renderer = new RedTextRenderer();  
  
    ```  
  
2.  In alternativa, per impostare il renderer personalizzato per tutte le classi <xref:System.Windows.Forms.ToolStrip> contenute nell'applicazione, impostare la proprietà <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=fullName> sul renderer personalizzato e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> su <xref:System.Windows.Forms.ToolStripRenderMode>.  
  
    ```vb  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode  
    ToolStripManager.Renderer = New RedTextRenderer()  
  
    ```  
  
     \[C\#\]  
  
    ```  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode;  
    ToolStripManager.Renderer = new RedTextRenderer();  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A>   
 <xref:System.Windows.Forms.ToolStripRenderer>   
 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)