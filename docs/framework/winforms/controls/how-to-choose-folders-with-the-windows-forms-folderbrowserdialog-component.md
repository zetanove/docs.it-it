---
title: "Procedura: scegliere cartelle con il componente FolderBrowserDialog di Windows Form | Microsoft Docs"
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
  - "directory [Windows Form], scelta"
  - "directory [Windows Form], selezione"
  - "FolderBrowserDialog (componente) [Windows Form], selezione delle directory"
  - "cartelle [Windows Form], scelta"
  - "cartelle [Windows Form], selezione"
ms.assetid: 4593670e-7c7d-4661-b46b-4ffb63258adb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: scegliere cartelle con il componente FolderBrowserDialog di Windows Form
Spesso nelle applicazioni Windows create è necessario chiedere agli utenti di selezionare una cartella, nella maggior parte dei casi per salvare un insieme di file.  Il componente <xref:System.Windows.Forms.FolderBrowserDialog> di Windows Form consente di eseguire questa attività in modo semplice e rapido.  
  
### Per scegliere cartelle con il componente FolderBrowserDialog  
  
1.  In una procedura controllare la proprietà <xref:System.Windows.Forms.Form.DialogResult%2A> del componente <xref:System.Windows.Forms.FolderBrowserDialog> per sapere se la finestra di dialogo è stata chiusa e ottenere il valore della proprietà <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> del componente <xref:System.Windows.Forms.FolderBrowserDialog>.  
  
2.  Per definire la cartella attiva all'interno della visualizzazione della struttura ad albero della finestra di dialogo, impostare la proprietà <xref:System.Windows.Forms.FolderBrowserDialog.RootFolder%2A>, che accetta un membro dell'enumerazione [SpecialFolder](frlrfSystemEnvironmentSpecialFolderClassTopic).  
  
3.  È inoltre possibile impostare la proprietà <xref:System.Windows.Forms.FolderBrowserDialog.Description%2A>, che consente di specificare la stringa di testo visualizzata nella parte superiore della visualizzazione della struttura ad albero del visualizzatore cartelle.  
  
     Nell'esempio che segue per selezionare una cartella viene utilizzato il componente <xref:System.Windows.Forms.FolderBrowserDialog> in modo simile a quando si crea un progetto in Visual Studio e viene richiesto di selezionare una cartella in cui salvarlo.  In questo esempio il nome della cartella viene quindi visualizzato in un controllo <xref:System.Windows.Forms.TextBox>del form.  È consigliabile specificare la posizione in un'area modificabile, quale un controllo <xref:System.Windows.Forms.TextBox>, in modo che gli utenti possano modificare la selezione in caso di errori o di altri problemi.  Nell'esempio si presuppone l'esistenza di un form contenente un componente <xref:System.Windows.Forms.FolderBrowserDialog> e un controllo <xref:System.Windows.Forms.TextBox>.  
  
    ```vb  
    Public Sub ChooseFolder()  
        If FolderBrowserDialog1.ShowDialog() = DialogResult.OK Then  
            TextBox1.Text = FolderBrowserDialog1.SelectedPath  
        End If  
    End Sub  
  
    ```  
  
    ```csharp  
    public void ChooseFolder()  
    {  
        if (folderBrowserDialog1.ShowDialog() == DialogResult.OK)   
        {  
            textBox1.Text = folderBrowserDialog1.SelectedPath;  
        }  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void ChooseFolder()  
       {  
          if (folderBrowserDialog1->ShowDialog() == DialogResult::OK)  
          {  
             textBox1->Text = folderBrowserDialog1->SelectedPath;  
          }  
       }  
    ```  
  
    > [!IMPORTANT]
    >  Per utilizzare questa classe, è necessario che l'assembly disponga di un livello di privilegio concesso dalla proprietà [FileIOPermissionAttribute.PathDiscoveryProperty](frlrfSystemSecurityPermissionsFileIOPermissionAttributeClassPathDiscoveryTopic), che fa parte dell'enumerazione <xref:System.Security.Permissions.FileIOPermissionAccess>.  Se l'esecuzione avviene in un contesto parzialmente attendibile, è possibile che il processo generi un'eccezione dovuta a privilegi insufficienti.  Per ulteriori informazioni, vedere [Code Access Security Basics](../../../../docs/framework/misc/code-access-security-basics.md).  
  
 Per ulteriori informazioni sul salvataggio dei file, vedere [Procedura: salvare file con il componente SaveFileDialog](../../../../docs/framework/winforms/controls/how-to-save-files-using-the-savefiledialog-component.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.FolderBrowserDialog>   
 [Cenni preliminari sul componente FolderBrowserDialog \(Windows Form\)](../../../../docs/framework/winforms/controls/folderbrowserdialog-component-overview-windows-forms.md)   
 [Componente FolderBrowserDialog](../../../../docs/framework/winforms/controls/folderbrowserdialog-component-windows-forms.md)