---
title: "Procedura: associare un menu di scelta rapida a un componente NotifyIcon di Windows Form | Microsoft Docs"
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
  - "menu di scelta rapida, processi in background"
  - "NotifyIcon (componente), associazione di menu di scelta rapida"
  - "menu di scelta rapida, processi in background"
ms.assetid: d68f3926-08d3-4f7d-949f-1981b29cf188
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Procedura: associare un menu di scelta rapida a un componente NotifyIcon di Windows Form
> [!NOTE]
>  Benché <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.ContextMenuStrip> sostituiscano i controlli <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> delle versioni precedenti aggiungendovi funzionalità, <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> vengono mantenuti per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Il componente <xref:System.Windows.Forms.NotifyIcon> consente di visualizzare un'icona nell'area di notifica dello stato della barra delle applicazioni.  Le applicazioni consentono in genere di fare clic con il pulsante destro del mouse su questa icona per inviare comandi all'applicazione da essa rappresentata.  Se si associa un componente <xref:System.Windows.Forms.ContextMenu> al componente <xref:System.Windows.Forms.NotifyIcon>, è possibile aggiungere questa funzionalità alle applicazioni.  
  
> [!NOTE]
>  Se si desidera ridurre l'applicazione a icona all'avvio e visualizzare un'istanza del componente <xref:System.Windows.Forms.NotifyIcon> nella barra delle applicazioni, impostare la proprietà <xref:System.Windows.Forms.Form.WindowState%2A> del form principale su <xref:System.Windows.Forms.FormWindowState> e assicurarsi che la proprietà <xref:System.Windows.Forms.NotifyIcon.Visible%2A> del componente  <xref:System.Windows.Forms.NotifyIcon> sia impostata su `true`.  
  
### Per associare un menu di scelta rapida al componente NotifyIcon in fase di progettazione  
  
1.  Aggiungere un componente <xref:System.Windows.Forms.NotifyIcon> al form e impostare le proprietà importanti, quali <xref:System.Windows.Forms.NotifyIcon.Icon%2A> e <xref:System.Windows.Forms.NotifyIcon.Visible%2A>.  
  
     Per ulteriori informazioni, vedere [Procedura: aggiungere icone alla barra delle applicazioni mediante il componente NotifyIcon Windows Form](../../../../docs/framework/winforms/controls/app-icons-to-the-taskbar-with-wf-notifyicon.md).  
  
2.  Aggiungere un componente <xref:System.Windows.Forms.ContextMenu> al form Windows Form.  
  
     Aggiungere al menu di scelta rapida voci che rappresentano i comandi da rendere disponibili in fase di esecuzione.  In questa fase è consigliabile anche aggiungere elementi per il perfezionamento dei menu, quali i tasti di scelta.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> del componente <xref:System.Windows.Forms.NotifyIcon> sul menu di scelta rapida aggiunto.  
  
     Una volta che si è impostata la proprietà, il menu di scelta rapida viene visualizzato quando si fa clic sull'icona della barra delle applicazioni.  
  
### Per associare un menu di scelta rapida al componente NotifyIcon a livello di codice  
  
1.  Creare un'istanza della classe <xref:System.Windows.Forms.NotifyIcon> e una classe <xref:System.Windows.Forms.ContextMenu> con le impostazioni necessarie per l'applicazione \(le proprietà <xref:System.Windows.Forms.NotifyIcon.Icon%2A> e <xref:System.Windows.Forms.NotifyIcon.Visible%2A> per il componente <xref:System.Windows.Forms.NotifyIcon> e le voci di menu per il componente <xref:System.Windows.Forms.ContextMenu>\).  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> del componente <xref:System.Windows.Forms.NotifyIcon> sul menu di scelta rapida aggiunto.  
  
     Una volta che si è impostata la proprietà, il menu di scelta rapida viene visualizzato quando si fa clic sull'icona della barra delle applicazioni.  
  
    > [!NOTE]
    >  L'esempio di codice seguente consente di creare una struttura di menu di base.  Personalizzare le scelte di menu in base a quelle necessarie per l'applicazione sviluppata.  Potrebbe inoltre essere necessario scrivere il codice per gestire gli eventi <xref:System.Windows.Forms.MenuItem.Click> per tali voci di menu.  
  
    ```vb  
    Public ContextMenu1 As New ContextMenu  
    Public NotifyIcon1 As New NotifyIcon  
  
    Public Sub CreateIconMenuStructure()  
       ' Add menu items to shortcut menu.  
       ContextMenu1.MenuItems.Add("&Open Application")  
       ContextMenu1.MenuItems.Add("S&uspend Application")  
       ContextMenu1.MenuItems.Add("E&xit")  
  
       ' Set properties of NotifyIcon component.  
       NotifyIcon1.Icon = New System.Drawing.Icon _   
          (System.Environment.GetFolderPath _   
          (System.Environment.SpecialFolder.Personal)  _   
          & "\Icon.ico")  
       NotifyIcon1.Text = "Right-click me!"  
       NotifyIcon1.Visible = True  
       NotifyIcon1.ContextMenu = ContextMenu1  
    End Sub  
  
    ```  
  
```csharp  
public NotifyIcon notifyIcon1 = new NotifyIcon();  
public ContextMenu contextMenu1 = new ContextMenu();  
  
public void createIconMenuStructure()  
{  
   // Add menu items to shortcut menu.  
   contextMenu1.MenuItems.Add("&Open Application");  
   contextMenu1.MenuItems.Add("S&uspend Application");  
   contextMenu1.MenuItems.Add("E&xit");  
  
   // Set properties of NotifyIcon component.  
   notifyIcon1.Icon = new System.Drawing.Icon  
      (System.Environment.GetFolderPath  
      (System.Environment.SpecialFolder.Personal)  
      + @"\Icon.ico");  
   notifyIcon1.Visible = true;  
   notifyIcon1.Text = "Right-click me!";  
   notifyIcon1.Visible = true;  
   notifyIcon1.ContextMenu = contextMenu1;  
}  
  
```  
  
```cpp  
public:  
   System::Windows::Forms::NotifyIcon ^ notifyIcon1;  
   System::Windows::Forms::ContextMenu ^ contextMenu1;  
  
   void createIconMenuStructure()  
   {  
      // Add menu items to shortcut menu.  
      contextMenu1->MenuItems->Add("&Open Application");  
      contextMenu1->MenuItems->Add("S&uspend Application");  
      contextMenu1->MenuItems->Add("E&xit");  
  
      // Set properties of NotifyIcon component.  
      notifyIcon1->Icon = gcnew System::Drawing::Icon  
          (String::Concat(System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::Personal),  
          "\\Icon.ico"));  
      notifyIcon1->Text = "Right-click me!";  
      notifyIcon1->Visible = true;  
      notifyIcon1->ContextMenu = contextMenu1;  
   }  
```  
  
> [!NOTE]
>  È necessario inizializzare `notifyIcon1` e `contextMenu1,`. Per effettuare questa operazione, includere le seguenti istruzioni nel costruttore del form:  
  
```cpp  
notifyIcon1 = gcnew System::Windows::Forms::NotifyIcon();  
contextMenu1 = gcnew System::Windows::Forms::ContextMenu();  
```  
  
## Vedere anche  
 <xref:System.Windows.Forms.NotifyIcon>   
 <xref:System.Windows.Forms.NotifyIcon.Icon%2A>   
 [Procedura: aggiungere icone alla barra delle applicazioni mediante il componente NotifyIcon Windows Form](../../../../docs/framework/winforms/controls/app-icons-to-the-taskbar-with-wf-notifyicon.md)   
 [Componente NotifyIcon](../../../../docs/framework/winforms/controls/notifyicon-component-windows-forms.md)   
 [Cenni preliminari sul componente NotifyIcon](../../../../docs/framework/winforms/controls/notifyicon-component-overview-windows-forms.md)