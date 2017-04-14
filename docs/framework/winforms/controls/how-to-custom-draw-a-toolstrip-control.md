---
title: "Procedura: eseguire un disegno personalizzato di un controllo ToolStrip | Microsoft Docs"
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
  - "disegno personalizzato"
  - "disegno, personalizzati"
  - "disegno, proprietario"
  - "esempi [Windows Form], barre degli strumenti"
  - "creazione del proprietario"
  - "ProfessionalColorTable (classe), override"
  - "RenderMode (proprietà)"
  - "barre degli strumenti [Windows Form], modifica dei colori"
  - "barre degli strumenti [Windows Form], disegno personalizzato"
  - "ToolStrip (controllo) [Windows Form], modifica dei colori"
  - "ToolStrip (controllo) [Windows Form], disegno"
  - "ToolStripProfessionalRenderer (classe)"
  - "ToolStripRenderer (classe)"
  - "ToolStripRenderMode (classe)"
  - "ToolStripSystemRenderer (classe)"
ms.assetid: 94e7d7bd-a752-441c-b5b3-7acf98881163
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire un disegno personalizzato di un controllo ToolStrip
Ai controlli <xref:System.Windows.Forms.ToolStrip> sono associate le classi di rendering \(disegno\) seguenti:  
  
-   <xref:System.Windows.Forms.ToolStripSystemRenderer> fornisce l'aspetto e lo stile del sistema operativo.  
  
-   <xref:System.Windows.Forms.ToolStripProfessionalRenderer> fornisce l'aspetto e lo stile di Microsoft Office.  
  
-   <xref:System.Windows.Forms.ToolStripRenderer> è la classe di base astratta per le altre due classi di rendering.  
  
 Per disegnare un controllo <xref:System.Windows.Forms.ToolStrip> personalizzato \(modalità nota anche come "Owner Draw"\), è possibile eseguire l'override di una delle classi renderer e modificare un aspetto della logica di rendering.  
  
 Le procedure seguenti descrivono vari aspetti del disegno personalizzato.  
  
### Per passare da un renderer fornito all'altro  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> sul valore <xref:System.Windows.Forms.ToolStripRenderMode> desiderato.  
  
     Con <xref:System.Windows.Forms.ToolStripRenderMode> la proprietà statica <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> determina il renderer per l'applicazione.  Gli altri valori di <xref:System.Windows.Forms.ToolStripRenderMode> sono <xref:System.Windows.Forms.ToolStripRenderMode>, <xref:System.Windows.Forms.ToolStripRenderMode> e <xref:System.Windows.Forms.ToolStripRenderMode>.  
  
### Per usare bordi diritti al posto dello stile Microsoft Office  
  
-   Eseguire l'override di <xref:System.Windows.Forms.ToolStripProfessionalRenderer.OnRenderToolStripBorder%2A?displayProperty=fullName>, ma senza chiamare la classe di base.  
  
> [!NOTE]
>  Esiste una versione di questo metodo per <xref:System.Windows.Forms.ToolStripRenderer>, <xref:System.Windows.Forms.ToolStripSystemRenderer> e <xref:System.Windows.Forms.ToolStripProfessionalRenderer>.  
  
### Per modificare la classe ProfessionalColorTable  
  
-   Eseguire l'override di <xref:System.Windows.Forms.ProfessionalColorTable> e cambiare i colori desiderati.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As _  
    System.EventArgs) Handles Me.Load  
        Dim t As MyColorTable = New MyColorTable  
        ToolStrip1.Renderer = New ToolStripProfessionalRenderer(t)  
    End Sub  
  
    Class MyColorTable   
    Inherits ProfessionalColorTable  
  
    Public Overrides ReadOnly Property ButtonPressedGradientBegin() As Color  
        Get  
            Return Color.Red  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonPressedGradientMiddle() _  
    As System.Drawing.Color  
        Get  
            Return Color.Blue  
        End Get  
            End Property  
  
    Public Overrides ReadOnly Property ButtonPressedGradientEnd() _  
    As System.Drawing.Color  
        Get  
            Return Color.Green  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientBegin() _  
    As Color  
        Get  
            Return Color.Yellow  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientMiddle() As System.Drawing.Color  
        Get  
            Return Color.Orange  
        End Get  
    End Property  
  
    Public Overrides ReadOnly Property ButtonSelectedGradientEnd() _  
    As System.Drawing.Color  
        Get  
            Return Color.Violet  
        End Get  
    End Property  
    End Class  
  
    ```  
  
### Per modificare il rendering di tutti i controlli ToolStrip nell'applicazione  
  
1.  Usare la proprietà <xref:System.Windows.Forms.ToolStripManager.RenderMode%2A?displayProperty=fullName> per scegliere uno dei renderer forniti.  
  
2.  Usare <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=fullName> per assegnare un renderer personalizzato.  
  
3.  Accertarsi che <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=fullName> sia impostata sul valore predefinito di <xref:System.Windows.Forms.ToolStripRenderMode>.  
  
### Per disattivare i colori di Microsoft Office in tutta l'applicazione  
  
-   Impostare <xref:System.Windows.Forms.ToolStripManager.VisualStylesEnabled%2A?displayProperty=fullName> su `false`.  
  
### Per disattivare i colori di Microsoft Office in un controllo ToolStrip  
  
-   Usare codice simile all'esempio seguente.  
  
     \[Visual Basic\]  
  
    ```  
    Dim colorTable As ProfessionalColorTable()  
    colorTable.UseSystemColors = True  
    Dim toolStrip.Renderer As ToolStripProfessionalRenderer(colorTable)  
  
    ```  
  
     \[C\#\]  
  
    ```  
    ProfessionalColorTable colorTable = new ProfessionalColorTable();  
    colorTable.UseSystemColors = true;  
    toolStrip.Renderer = new ToolStripProfessionalRenderer(colorTable);  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripSystemRenderer>   
 <xref:System.Windows.Forms.ToolStripProfessionalRenderer>   
 <xref:System.Windows.Forms.ToolStripRenderer>   
 [Controlli con supporto incorporato per la creazione da parte del proprietario](../../../../docs/framework/winforms/controls/controls-with-built-in-owner-drawing-support.md)   
 [Procedura: creare e impostare un renderer personalizzato per il controllo ToolStrip in Windows Form](../../../../docs/framework/winforms/controls/create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)