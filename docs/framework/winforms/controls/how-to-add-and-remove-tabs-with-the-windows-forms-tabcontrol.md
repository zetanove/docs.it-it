---
title: "Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form | Microsoft Docs"
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
  - "schede"
  - "TabControl (controllo) [Windows Form], aggiunta e rimozione schede"
  - "TabPage (controllo)"
  - "schede, aggiunta alle pagine"
  - "schede, rimozione da pagine"
ms.assetid: 66d4dfca-41e8-44e3-9c80-fb7ac4cb1619
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form
Per impostazione predefinita, un controllo <xref:System.Windows.Forms.TabControl> contiene due controlli <xref:System.Windows.Forms.TabPage>.  È possibile accedere a queste schede mediante la proprietà <xref:System.Windows.Forms.TabControl.TabPages%2A>.  
  
### Per aggiungere una scheda a livello di codice  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.TabControl.TabPageCollection.Add%2A> della proprietà <xref:System.Windows.Forms.TabControl.TabPages%2A>.  
  
    ```vb  
    Dim myTabPage As New TabPage()  
    myTabPage.Text = "TabPage" & (TabControl1.TabPages.Count + 1)  
    TabControl1.TabPages.Add(myTabPage)  
  
    ```  
  
    ```csharp  
    string title = "TabPage " + (tabControl1.TabCount + 1).ToString();  
    TabPage myTabPage = new TabPage(title);  
    tabControl1.TabPages.Add(myTabPage);  
  
    ```  
  
    ```cpp  
    String^ title = String::Concat("TabPage ",  
       (tabControl1->TabCount + 1).ToString());  
    TabPage^ myTabPage = gcnew TabPage(title);  
    tabControl1->TabPages->Add(myTabPage);  
    ```  
  
### Per rimuovere una scheda a livello di codice  
  
-   Per rimuovere le schede selezionate, utilizzare il metodo <xref:System.Windows.Forms.TabControl.TabPageCollection.Remove%2A> della proprietà <xref:System.Windows.Forms.TabControl.TabPages%2A>.  
  
     In alternativa  
  
-   Per rimuovere tutte le schede, utilizzare il metodo <xref:System.Windows.Forms.TabControl.TabPageCollection.Clear%2A> della proprietà <xref:System.Windows.Forms.TabControl.TabPages%2A>.  
  
    ```vb  
    ' Removes the selected tab:  
    TabControl1.TabPages.Remove(TabControl1.SelectedTab)  
    ' Removes all the tabs:  
    TabControl1.TabPages.Clear()  
  
    ```  
  
    ```csharp  
    // Removes the selected tab:  
    tabControl1.TabPages.Remove(tabControl1.SelectedTab);  
    // Removes all the tabs:  
    tabControl1.TabPages.Clear();  
  
    ```  
  
    ```cpp  
    // Removes the selected tab:  
    tabControl1->TabPages->Remove(tabControl1->SelectedTab);  
    // Removes all the tabs:  
    tabControl1->TabPages->Clear();  
    ```  
  
## Vedere anche  
 [Cenni preliminari sul controllo TabControl](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [Procedura: aggiungere un controllo a un oggetto TabPage](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [Procedura: disabilitare le schede](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [Procedura: modificare l'aspetto del controllo TabControl Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)