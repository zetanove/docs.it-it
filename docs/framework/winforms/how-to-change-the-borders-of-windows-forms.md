---
title: "How to: Change the Borders of Windows Forms | Microsoft Docs"
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
  - "Windows Forms, changing the borders"
ms.assetid: b3d5fa56-80c6-4b10-b505-f9672307ed55
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Change the Borders of Windows Forms
Quando si stabiliscono l'aspetto e il comportamento di Windows Form, è possibile scegliere tra diversi stili bordo.  Modificando la proprietà <xref:System.Windows.Forms.Form.FormBorderStyle%2A>, è possibile controllare il comportamento di ridimensionamento del form.  Inoltre, l'impostazione di <xref:System.Windows.Forms.Form.FormBorderStyle%2A> influisce sul modo in cui la barra del titolo viene visualizzata e su quali pulsanti possono apparire sulla barra stessa.  Per altre informazioni, vedere <xref:System.Windows.Forms.FormBorderStyle>.  
  
 In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] è disponibile supporto completo per questa attività.  
  
 Vedere anche [Procedura: Modificare i bordi di Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/yettzh3e\(v=vs.110\)).  
  
### Per impostare lo stile bordo di Windows Form a livello di codice  
  
-   Impostare la proprietà <xref:System.Windows.Forms.Form.FormBorderStyle%2A> sullo stile desiderato.  L'esempio di codice seguente imposta lo stile bordo del form `DlgBx1` su <xref:System.Windows.Forms.FormBorderStyle>.  
  
    ```vb  
    DlgBx1.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog  
    ```  
  
    ```csharp  
    DlgBx1.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog;  
    ```  
  
    ```cpp  
    DlgBx1->FormBorderStyle =  
       System::Windows::Forms::FormBorderStyle::FixedDialog;  
    ```  
  
     Vedere anche [Procedura: Creare finestre di dialogo in fase di progettazione](http://msdn.microsoft.com/library/55cz5x2c\(v=vs.110\)).  
  
     Inoltre, se si è scelto per il form uno stile bordo che prevede la visualizzazione dei pulsanti facoltativi **Riduci a icona** e **Ingrandisci**, è possibile specificare se uno solo o entrambi i pulsanti debbano essere funzionali.  Questi pulsanti sono utili quando si desidera controllare da vicino l'esperienza utente.  I pulsanti **Riduci a icona** e **Ingrandisci** sono abilitati per impostazione predefinita ed è possibile modificarne la funzionalità nella finestra **Proprietà**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.FormBorderStyle>   
 <xref:System.Windows.Forms.FormBorderStyle>   
 [Getting Started with Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)