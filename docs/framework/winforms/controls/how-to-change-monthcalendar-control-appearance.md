---
title: "Procedura: modificare l&#39;aspetto del controllo MonthCalendar Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], calendario (controlli)"
  - "MonthBackColor (proprietà)"
  - "MonthCalendar (controllo) [Windows Form], formattazione della visualizzazione"
  - "TitleBackColor (proprietà)"
  - "TitleForeColor (proprietà)"
  - "TrailingForeColor (proprietà)"
ms.assetid: d09b95c9-e108-4608-9b31-b9100c0677bf
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: modificare l&#39;aspetto del controllo MonthCalendar Windows Form
Il controllo <xref:System.Windows.Forms.MonthCalendar> Windows Form consente di personalizzare l'aspetto del calendario in numerosi modi.  È ad esempio possibile definire la combinazione di colori e scegliere se visualizzare o nascondere i numeri delle settimane e la data corrente.  
  
### Per modificare la combinazione dei colori del calendario mensile  
  
-   Impostare proprietà quali <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A> e <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A>.  La proprietà <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A> determina anche il colore del carattere utilizzato per i giorni della settimana.  La proprietà <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> determina il colore delle date precedenti e successive rispetto al mese o ai mesi selezionati.  
  
    ```vb  
    MonthCalendar1.TitleBackColor = System.Drawing.Color.Blue  
    MonthCalendar1.TrailingForeColor = System.Drawing.Color.Red  
    MonthCalendar1.TitleForeColor = System.Drawing.Color.Yellow  
    ```  
  
    ```csharp  
    monthCalendar1.TitleBackColor = System.Drawing.Color.Blue;  
    monthCalendar1.TrailingForeColor = System.Drawing.Color.Red;  
    monthCalendar1.TitleForeColor = System.Drawing.Color.Yellow;  
    ```  
  
    ```cpp  
    monthCalendar1->TitleBackColor = System::Drawing::Color::Blue;  
    monthCalendar1->TrailingForeColor = System::Drawing::Color::Red;  
    monthCalendar1->TitleForeColor = System::Drawing::Color::Yellow;  
    ```  
  
    > [!NOTE]
    >  A partire da Windows Vista e a seconda del tema, l'impostazione di alcune proprietà potrebbe non modificare l'aspetto del calendario.  Se ad esempio Windows è impostato per utilizzare il tema Aereo, l'impostazione delle proprietà <xref:System.Windows.Forms.MonthCalendar.BackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A> o <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> non ha alcun effetto.  Ciò è dovuto al fatto che viene eseguito il rendering di una versione aggiornata del calendario con un aspetto derivato in fase di esecuzione dal tema corrente del sistema operativo.  Se si desidera utilizzare queste proprietà e abilitare la versione precedente del calendario, è possibile disabilitare gli stili di visualizzazione per l'applicazione.  La disabilitazione degli stili di visualizzazione potrebbe influire sull'aspetto e sul comportamento degli altri controlli dell'applicazione.  Per disabilitare gli stili di visualizzazione in Visual Basic, aprire Progettazione progetti e deselezionare la casella di controllo **Attiva stili di visualizzazione XP**.  Per disabilitare gli stili di visualizzazione in C\#, aprire Program.cs e impostare come commento `Application.EnableVisualStyles();`.  Per ulteriori informazioni sugli stili di visualizzazione, vedere [How to: Enable Windows XP Visual Styles](http://msdn.microsoft.com/it-it/0a038ade-31cf-4e56-9cfe-7a1e6b83b57f).  
  
### Per visualizzare la data corrente nella parte inferiore del controllo  
  
-   Impostare la proprietà <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> su `true`.  Nell'esempio riportato di seguito, la visualizzazione della data odierna viene attivata o disattivata facendo doppio clic sul form.  
  
    ```vb  
    Private Sub Form1_DoubleClick(ByVal sender As Object, _  
    ByVal e As System.EventArgs) Handles MyBase.DoubleClick  
       ' Toggle between True and False.  
       MonthCalendar1.ShowToday = Not MonthCalendar1.ShowToday  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_DoubleClick(object sender, System.EventArgs e)  
    {  
       // Toggle between True and False.  
       monthCalendar1.ShowToday = !monthCalendar1.ShowToday;  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void Form1_DoubleClick(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // Toggle between True and False.  
          monthCalendar1->ShowToday = !monthCalendar1->ShowToday;  
       }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.DoubleClick += new System.EventHandler(this.Form1_DoubleClick);  
    ```  
  
    ```cpp  
    this->DoubleClick += gcnew System::EventHandler(this,  
       &Form1::Form1_DoubleClick);  
    ```  
  
### Per visualizzare i numeri delle settimane  
  
-   Impostare la proprietà <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> su `true`.  Questa proprietà può essere impostata nel codice o nella finestra Proprietà.  
  
     I numeri delle settimane vengono visualizzati in una colonna separata a sinistra del primo giorno della settimana.  
  
    ```vb  
    MonthCalendar1.ShowWeekNumbers = True  
    ```  
  
    ```csharp  
    monthCalendar1.ShowWeekNumbers = true;  
    ```  
  
    ```cpp  
    monthCalendar1->ShowWeekNumbers = true;  
    ```  
  
## Vedere anche  
 [Controllo MonthCalendar](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [Procedura: selezionare un intervallo di date nel controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)   
 [Procedura: visualizzare giorni specifici in grassetto con il controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/display-specific-days-in-bold-with-wf-monthcalendar-control.md)   
 [Procedura: visualizzare più mesi nel controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/display-more-than-one-month-wf-monthcalendar-control.md)