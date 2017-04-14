---
title: "Procedura: impostare e restituire date con il controllo DateTimePicker Windows Form | Microsoft Docs"
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
  - "date, impostazione in DateTimePicker"
  - "DateTimePicker (controllo) [Windows Form], impostazione e restituzione di date"
  - "esempi [Windows Form], DateTimePicker (controllo)"
ms.assetid: a8a48d68-e4b5-426e-9764-51230fc9acd2
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: impostare e restituire date con il controllo DateTimePicker Windows Form
La data o l'ora selezionata nel controllo <xref:System.Windows.Forms.DateTimePicker> Windows Form è determinata dalla proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A>,  che può essere impostata sulla proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> prima della visualizzazione del controllo, ad esempio in fase di progettazione o nell'evento <xref:System.Windows.Forms.Form.Load>, per determinare la data che verrà inizialmente selezionata nel controllo.  Per impostazione predefinita, la proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> del controllo è impostata sulla data corrente.  Se la proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> del controllo viene modificata nel codice, il controllo viene automaticamente aggiornato nel form in base alla nuova impostazione.  
  
 La proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> restituisce come valore una struttura <xref:System.DateTime>.  Numerose proprietà della struttura <xref:System.DateTime> restituiscono informazioni specifiche sulla data visualizzata.  Tali proprietà, tuttavia, possono essere usate solo per la restituzione di un valore, non per l'impostazione.  
  
-   Per i valori relativi alla data, le proprietà <xref:System.DateTime.Month%2A>, <xref:System.DateTime.Day%2A> e <xref:System.DateTime.Year%2A> restituiscono valori Integer per le unità di tempo corrispondenti della data selezionata.  La proprietà <xref:System.DateTime.DayOfWeek%2A> restituisce un valore che indica il giorno della settimana selezionato. Per un elenco dei valori disponibili, vedere l'enumerazione <xref:System.DayOfWeek>.  
  
-   Per i valori relativi all'ora, le proprietà <xref:System.DateTime.Hour%2A>, <xref:System.DateTime.Minute%2A>, <xref:System.DateTime.Second%2A> e <xref:System.DateTime.Millisecond%2A> restituiscono valori Integer per le unità di tempo corrispondenti.  Per configurare il controllo in modo da visualizzare l'ora, vedere [Procedura: visualizzare l'ora con il controllo DateTimePicker](../../../../docs/framework/winforms/controls/how-to-display-time-with-the-datetimepicker-control.md).  
  
### Per impostare i valori di data e di ora del controllo  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> su un valore di data o di ora.  
  
    ```vb  
    DateTimePicker1.Value = New DateTime(2001, 10, 20)  
  
    ```  
  
    ```csharp  
    dateTimePicker1.Value = new DateTime(2001, 10, 20);  
  
    ```  
  
    ```cpp  
    dateTimePicker1->Value = DateTime(2001, 10, 20);  
    ```  
  
### Per restituire il valore di data e di ora  
  
-   Chiamare la proprietà <xref:System.Windows.Forms.DateTimePicker.Text%2A> per restituire il valore completo nel formato impostato per il controllo, oppure chiamare il metodo appropriato della proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> per restituire una parte del valore.  Usare <xref:System.Windows.Forms.DateTimePicker.ToString%2A> per convertire le informazioni in una stringa visualizzabile all'utente.  
  
    ```vb  
    MessageBox.Show("The selected value is ", DateTimePicker1.Text)  
    MessageBox.Show("The day of the week is ",   
       DateTimePicker1.Value.DayOfWeek.ToString)  
    MessageBox.Show("Millisecond is: ",   
       DateTimePicker1.Value.Millisecond.ToString)  
  
    ```  
  
    ```csharp  
    MessageBox.Show ("The selected value is " +   
       dateTimePicker1.Text);  
    MessageBox.Show ("The day of the week is " +   
       dateTimePicker1.Value.DayOfWeek.ToString());  
    MessageBox.Show("Millisecond is: " +   
       dateTimePicker1.Value.Millisecond.ToString());  
  
    ```  
  
    ```cpp  
    MessageBox::Show (String::Concat("The selected value is ",  
       dateTimePicker1->Text));  
    MessageBox::Show (String::Concat("The day of the week is ",  
       dateTimePicker1->Value.DayOfWeek.ToString()));  
    MessageBox::Show(String::Concat("Millisecond is: ",  
       dateTimePicker1->Value.Millisecond.ToString()));  
    ```  
  
## Vedere anche  
 [Controllo DateTimePicker](../../../../docs/framework/winforms/controls/datetimepicker-control-windows-forms.md)   
 [Procedura: visualizzare una data in un formato personalizzato con il controllo DateTimePicker di Windows Form](../../../../docs/framework/winforms/controls/display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)