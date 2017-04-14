---
title: "Procedura: specificare una bitmap nella casella degli strumenti per un controllo | Microsoft Docs"
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
  - "bitmap [Windows Form], controlli personalizzati"
  - "controlli personalizzati [Windows Form], bitmap della casella degli strumenti"
  - "casella degli strumenti [Windows Form], aggiunta di bitmap per i controlli personalizzati"
ms.assetid: 0ed0840a-616d-41ba-a27d-3573241932ad
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura: specificare una bitmap nella casella degli strumenti per un controllo
Per visualizzare un'icona speciale per il controllo nella **Casella degli strumenti**, è possibile specificare una particolare immagine utilizzando <xref:System.Drawing.ToolboxBitmapAttribute>.  Questa classe è un *attributo*, ovvero un particolare tipo di classe che è possibile collegare ad altre classi.  Per ulteriori informazioni sugli attributi, vedere [NOT IN BUILD: Attributes Overview in Visual Basic](http://msdn.microsoft.com/it-it/0d0cff64-892d-4f57-83bd-bef388553d4f) per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] e [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md) per [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)].  
  
 La classe <xref:System.Drawing.ToolboxBitmapAttribute> consente di specificare una stringa che indica il nome file e il percorso di una bitmap di 16 x 16 pixel.  La bitmap verrà quindi visualizzata accanto al controllo quando quest'ultimo viene aggiunto alla **Casella degli strumenti**.  È inoltre possibile specificare un parametro <xref:System.Type> in modo da caricare la bitmap associata al tipo specificato.  Se si specifica sia un parametro <xref:System.Type> che una stringa, il controllo ricercherà una risorsa immagine il cui nome è specificato dal parametro stringa nell'assembly contenente il tipo specificato dal parametro <xref:System.Type>.  
  
### Per specificare una bitmap nella Casella degli strumenti per il controllo  
  
1.  Aggiungere <xref:System.Drawing.ToolboxBitmapAttribute> alla dichiarazione di classi del controllo prima della parola chiave `Class` per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] e sopra la dichiarazione di classi per [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)].  
  
    ```vb  
    ' Specifies the bitmap associated with the Button type.  
    <ToolboxBitmap(GetType(Button))> Class MyControl1  
    ' Specifies a bitmap file.  
    End Class  
    <ToolboxBitmap("C:\Documents and Settings\Joe\MyPics\myImage.bmp")> _  
       Class MyControl2  
    End Class  
    ' Specifies a type that indicates the assembly to search, and the name   
    ' of an image resource to look for.  
    <ToolboxBitmap(GetType(MyControl), "MyControlBitmap")> Class MyControl  
    End Class  
    ```  
  
    ```csharp  
    // Specifies the bitmap associated with the Button type.  
    [ToolboxBitmap(typeof(Button))]  
    class MyControl1 : UserControl  
    {  
    }  
    // Specifies a bitmap file.  
    [ToolboxBitmap(@"C:\Documents and Settings\Joe\MyPics\myImage.bmp")]  
    class MyControl2 : UserControl  
    {  
    }  
    // Specifies a type that indicates the assembly to search, and the name   
    // of an image resource to look for.  
    [ToolboxBitmap(typeof(MyControl), "MyControlBitmap")]  
    class MyControl : UserControl  
    {  
    }  
    ```  
  
2.  Ricompilare il progetto.  
  
    > [!NOTE]
    >  La bitmap non è visualizzata nella casella degli strumenti per controlli e componenti generati automaticamente.  Per vedere la bitmap, ricaricare il controllo utilizzando la finestra di dialogo **Scegli elementi della Casella degli strumenti**.  Per ulteriori informazioni, vedere [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md).  
  
## Vedere anche  
 <xref:System.Drawing.ToolboxBitmapAttribute>   
 [Procedura dettagliata: compilare automaticamente la casella degli strumenti con componenti personalizzati](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)   
 [Sviluppo di controlli Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [Attributes](../Topic/Attributes%20\(Visual%20Basic\)1.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)