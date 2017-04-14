---
title: "Procedura: rendere invisibile il controllo in fase di esecuzione | Microsoft Docs"
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
  - "controlli [Windows Form], invisibili in fase di esecuzione"
  - "controlli personalizzati [Windows Form], invisibile"
  - "controlli invisibili"
  - "runtime, controlli invisibili"
  - "controlli utente [Windows Form], invisibile"
ms.assetid: 69eb2e72-32f5-4f79-a157-c2c5f60c1628
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: rendere invisibile il controllo in fase di esecuzione
In alcuni casi può essere necessario creare un controllo utente che sia invisibile in fase di esecuzione.  È ad esempio possibile impostare un controllo di una sveglia come invisibile quando non viene emesso il segnale acustico.  Per creare un controllo di questo tipo, è sufficiente impostare la proprietà <xref:System.Windows.Forms.Control.Visible%2A>.  Se la proprietà <xref:System.Windows.Forms.Control.Visible%2A> è impostata su `true`, il controllo verrà visualizzato normalmente.  Se la proprietà è impostata su `false`, il controllo verrà nascosto.  Sebbene il codice nel controllo possa essere ancora in esecuzione quando il controllo è invisibile, non sarà possibile interagire con il controllo attraverso l'interfaccia utente.  Se si desidera creare un controllo invisibile in grado di rispondere all'input dell'utente, ad esempio un click del mouse, è necessario creare un controllo trasparente.  Per ulteriori informazioni, vedere [Assegnazione di uno sfondo trasparente al controllo](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md).  
  
### Per rendere un controllo invisibile in fase di esecuzione  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.Visible%2A> su `false`.  
  
    ```vb  
    ' To set the Visible property from within your object's own code.  
    Me.Visible = False  
    ' To set the Visible property from another object.  
    myControl1.Visible = False  
  
    ```  
  
    ```csharp  
    // To set the Visible property from within your object's own code.  
    this.Visible = false;  
    // To set the Visible property from another object.  
    myControl1.Visible = false;  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.Visible%2A>   
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Procedura: assegnare uno sfondo trasparente al controllo](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)