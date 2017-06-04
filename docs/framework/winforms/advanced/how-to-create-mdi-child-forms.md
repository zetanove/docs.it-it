---
title: "Procedura: creare form figlio MDI | Microsoft Docs"
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
  - "form figlio"
  - "MDI, creazione di form"
ms.assetid: 164b69bb-2eca-4339-ada3-0679eb2c6dda
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: creare form figlio MDI
I form figlio MDI sono un elemento fondamentale delle [Applicazioni MDI \(Interfaccia a documenti multipli, Multiple\-Document Interface\)](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md), in quanto costituiscono il fulcro dell'interazione dell'utente.  
  
 Nella procedura che segue vengono creati form figlio MDI che visualizzano un controllo <xref:System.Windows.Forms.RichTextBox>, analogo alla maggior parte delle applicazioni per l'elaborazione di testi.  Sostituendo il controllo <xref:System.Windows.Forms> con altri controlli, ad esempio con <xref:System.Windows.Forms.DataGridView> o con più controlli, è possibile creare finestre figlio MDI e applicazioni MDI con differenti possibilità.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare form figlio MDI  
  
1.  Creare un nuovo progetto Windows Form.  Nella finestra **Proprietà** del form impostare la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true` e la proprietà `WindowsState` su `Maximized`.  
  
     Il form viene così designato come contenitore MDI per le finestre figlio.  
  
2.  Dalla `Toolbox` trascinare un controllo <xref:System.Windows.Forms.MenuStrip> nel form.  Impostarne la proprietà `Text` su **File**.  
  
3.  Fare clic sui puntini di sospensione \(…\) accanto alla proprietà **Items** e fare clic su **Aggiungi** per aggiungere due voci di menu ToolStrip figlio.  Impostare la proprietà `Text` di questi elementi su **New** e **Window**.  
  
4.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi**, quindi selezionare **Aggiungi nuovo elemento**.  
  
5.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Windows Form** \(in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o in [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]\) o **Applicazione Windows Form \(.NET\)** \(in [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) dal riquadro **Modelli**.  Nella casella **Nome** assegnare al form il nome Form2.  Fare clic sul pulsante **Apri** per aggiungere il form al progetto.  
  
    > [!NOTE]
    >  Il form figlio MDI creato in questo passaggio è un Windows Form standard.  Dispone pertanto di una proprietà <xref:System.Windows.Forms.Form.Opacity%2A> che consente di controllare la trasparenza del form.  La proprietà <xref:System.Windows.Forms.Form.Opacity%2A>, tuttavia, è stata progettata per le finestre di primo livello.  Per evitare problemi di disegno, non usarla con i form figlio MDI.  
  
     Il form costituirà il modello per i form figlio MDI.  
  
     Verrà aperto **Progettazione Windows Form**, in cui è visualizzato Form2.  
  
6.  Dalla **Casella degli strumenti** trascinare un controllo **RichTextBox** nel form.  
  
7.  Nella finestra **Proprietà** impostare la proprietà `Anchor` su **Top, Left** e la proprietà `Dock` su **Fill**.  
  
     In questo modo il controllo <xref:System.Windows.Forms.RichTextBox> riempirà completamente l'area del form figlio MDI, anche quando viene ridimensionato.  
  
8.  Creare un gestore eventi <xref:System.Windows.Forms.Control.Click> per la voce di menu **Nuovo** facendo doppio clic su di essa.  
  
9. Inserire codice simile al seguente per creare un nuovo form figlio MDI quando l'utente fa clic sulla voce di menu **Nuovo**.  
  
    > [!NOTE]
    >  Nell'esempio che segue il gestore eventi gestisce l'evento <xref:System.Windows.Forms.Control.Click> per `MenuItem2`.  Tenere presente che, in base alle specifiche dell'architettura dell'applicazione, la voce di menu **Nuovo** potrebbe non essere `MenuItem2`.  
  
    ```vb  
    Protected Sub MDIChildNew_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MenuItem2.Click  
       Dim NewMDIChild As New Form2()  
       'Set the Parent Form of the Child window.  
       NewMDIChild.MdiParent = Me  
       'Display the new form.  
       NewMDIChild.Show()  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void MDIChildNew_Click(object sender, System.EventArgs e){  
       Form2 newMDIChild = new Form2();  
       // Set the Parent Form of the Child window.  
       newMDIChild.MdiParent = this;  
       // Display the new form.  
       newMDIChild.Show();  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void menuItem2_Click(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          Form2^ newMDIChild = gcnew Form2();  
          // Set the Parent Form of the Child window.  
          newMDIChild->MdiParent = this;  
          // Display the new form.  
          newMDIChild->Show();  
       }  
    ```  
  
     In [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)] aggiungere la direttiva `#include` seguente all'inizio di Form1.h:  
  
    ```cpp  
    #include "Form2.h"  
    ```  
  
10. Nell'elenco a discesa nella parte superiore della finestra **Proprietà** selezionare il controllo MenuStrip che corrisponde a **File** e impostare la proprietà <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> sulla classe <xref:System.Windows.Forms.ToolStripMenuItem> della finestra.  
  
     In questo modo il menu **Finestra** manterrà un elenco di finestre figlio MDI aperte, con un segno di spunta accanto alla finestra figlio attiva.  
  
11. Premere F5 per eseguire l'applicazione.  Scegliendo **Nuovo** dal menu **File** si possono creare nuovi form figlio MDI di cui viene tenuta traccia nella voce di menu **Finestra**.  
  
    > [!NOTE]
    >  Quando un form figlio MDI con un componente <xref:System.Windows.Forms.MainMenu>, associato in genere a una struttura di voci di menu, viene aperto all'interno di un form padre MDI dotato di un componente <xref:System.Windows.Forms.MainMenu>, solitamente con struttura di voci di menu, le voci di menu vengono unite automaticamente se è stata impostata la proprietà <xref:System.Windows.Forms.MenuItem.MergeType%2A> ed eventualmente la proprietà <xref:System.Windows.Forms.MenuItem.MergeOrder%2A>.  Impostare la proprietà <xref:System.Windows.Forms.MenuItem.MergeType%2A> sia per i componenti <xref:System.Windows.Forms.MainMenu> che per tutte le voci di menu del form figlio su <xref:System.Windows.Forms.MenuMerge>.  Impostare anche la proprietà <xref:System.Windows.Forms.MenuItem.MergeOrder%2A> in modo che le voci di entrambi i menu appaiano nell'ordine desiderato.  Tenere presente inoltre che quando si chiude un form padre MDI, ciascun form figlio MDI genera un evento <xref:System.Windows.Forms.Form.Closing> prima che venga generato l'evento <xref:System.Windows.Forms.Form.Closing> per il padre MDI.  L'annullamento di un evento <xref:System.Windows.Forms.Form.Closing> di un figlio MDI non impedisce la generazione dell'evento <xref:System.Windows.Forms.Form.Closing> del padre MDI, ma l'argomento <xref:System.ComponentModel.CancelEventArgs> per l'evento <xref:System.Windows.Forms.Form.Closing> del padre MDI verrà ora impostato su `true`.  È possibile imporre la chiusura del form padre MDI e di tutti i form figlio MDI impostando l'argomento <xref:System.ComponentModel.CancelEventArgs> su `false`.  
  
## Vedere anche  
 [Applicazioni MDI \(Interfaccia a documenti multipli, Multiple\-Document Interface\)](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)   
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [Procedura: determinare il figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)   
 [Procedura: inviare dati al figlio MDI attivo](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)   
 [Procedura: disporre i form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)