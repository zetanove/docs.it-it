---
title: "Procedura: aggiungere icone alla barra delle applicazioni mediante il componente NotifyIcon Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "TrayIcon"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "icone, aggiunta a barra delle applicazioni"
  - "NotifyIcon (componente)"
  - "icone dell'area di stato"
  - "barra delle applicazioni, aggiunta di icone"
ms.assetid: d28c0fe6-aaf2-4df7-ad74-928d861a8510
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: aggiungere icone alla barra delle applicazioni mediante il componente NotifyIcon Windows Form
Il componente <xref:System.Windows.Forms.NotifyIcon> Windows Form consente di visualizzare una singola icona nell'area di notifica dello stato della barra delle applicazioni.  Per visualizzare più icone nell'area di stato, è necessario che sul form siano presenti più componenti <xref:System.Windows.Forms.NotifyIcon>.  Per impostare l'icona visualizzata per un controllo, utilizzare la proprietà <xref:System.Windows.Forms.NotifyIcon.Icon%2A>.  È inoltre possibile scrivere nel gestore eventi <xref:System.Windows.Forms.NotifyIcon.DoubleClick> il codice necessario per ottenere un determinato risultato quando l'utente fa doppio clic sull'icona.  È possibile fare in modo che venga visualizzata, ad esempio, una finestra di dialogo per la configurazione del processo in background rappresentato dall'icona.  
  
> [!NOTE]
>  Il componente <xref:System.Windows.Forms.NotifyIcon> viene utilizzato solo a scopo di notifica, per avvisare gli utenti che si è verificata uno specifico evento, azione o modifica dello stato.  Per garantire un'interazione standard con le applicazioni, è consigliabile utilizzare menu, barre degli strumenti e altri elementi dell'interfaccia utente.  
  
### Per impostare l'icona  
  
1.  Assegnare un valore alla proprietà <xref:System.Windows.Forms.NotifyIcon.Icon%2A>.  Il valore deve essere di tipo  `System.Drawing.Icon`  e può essere caricato da un file ICO.  Per specificare il file icona nel codice, scegliere il pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.NotifyIcon.Icon%2A> nella finestra **Proprietà**, quindi selezionare il file nella finestra di dialogo **Apri** che verrà visualizzata.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.NotifyIcon.Visible%2A> su `true`.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.NotifyIcon.Text%2A> su una stringa di descrizione appropriata.  
  
     Nell'esempio di codice riportato di seguito il percorso impostato per la posizione dell'icona corrisponde alla cartella **Documenti**.  Si consiglia di utilizzare questa posizione perché tale cartella è presente nella maggior parte dei computer che esegue il sistema operativo Windows.  Questa impostazione consente inoltre agli utenti con livelli minimi di accesso al sistema di eseguire l'applicazione in modo sicuro.  Per l'esempio è necessario un form a cui sia già stato aggiunto il controllo <xref:System.Windows.Forms.NotifyIcon>.  È inoltre necessario un file icona denominato `Icon.ico`.  
  
     \[Visual Basic\]  
  
    ```  
    ' You should replace the bold icon in the sample below  
    ' with an icon of your own choosing.  
    NotifyIcon1.Icon = New _   
       System.Drawing.Icon(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Icon.ico")  
    NotifyIcon1.Visible = True  
    NotifyIcon1.Text = "Antivirus program"  
  
    ```  
  
     \[C\#\]  
  
    ```  
    // You should replace the bold icon in the sample below  
    // with an icon of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    notifyIcon1.Icon =   
       new System.Drawing.Icon (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Icon.ico");  
    notifyIcon1.Visible = true;  
    notifyIcon1.Text = "Antivirus program";  
  
    ```  
  
     \[cpp\]  
  
    ```  
    // You should replace the bold icon in the sample below  
    // with an icon of your own choosing.  
    notifyIcon1->Icon = gcnew   
       System::Drawing::Icon(String::Concat  
       (System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\Icon.ico"));  
    notifyIcon1->Visible = true;  
    notifyIcon1->Text = "Antivirus program";  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.NotifyIcon>   
 <xref:System.Windows.Forms.NotifyIcon.Icon%2A>   
 [Procedura: associare un menu di scelta rapida a un componente NotifyIcon di Windows Form](../../../../docs/framework/winforms/controls/how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component.md)   
 [Componente NotifyIcon](../../../../docs/framework/winforms/controls/notifyicon-component-windows-forms.md)   
 [Cenni preliminari sul componente NotifyIcon](../../../../docs/framework/winforms/controls/notifyicon-component-overview-windows-forms.md)