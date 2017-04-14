---
title: "Procedura: selezionare un intervallo di date nel controllo MonthCalendar Windows Form | Microsoft Docs"
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
  - "calendari, selezione dell'intervallo di date"
  - "date, selezione di intervalli nei controlli di tipo calendario"
  - "esempi [Windows Form], calendario (controlli)"
  - "MonthCalendar (controllo) [Windows Form], selezione dell'intervallo di date"
ms.assetid: 95d9ab95-b0f8-4c19-9f63-b5cd4593a5d0
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: selezionare un intervallo di date nel controllo MonthCalendar Windows Form
Un'importante funzionalità del controllo <xref:System.Windows.Forms.MonthCalendar> Windows Form consiste nella possibilità di selezionare un intervallo di date.  Questo rappresenta un miglioramento rispetto alla funzionalità di selezione della data del controllo <xref:System.Windows.Forms.DateTimePicker>, che consentiva all'utente di selezionare soltanto un singolo valore data\/ora.  È possibile utilizzare le proprietà del controllo <xref:System.Windows.Forms.MonthCalendar> per impostare un intervallo di date o per ottenere un intervallo di selezione impostato dall'utente.  Nell'esempio di codice riportato di seguito viene illustrato come impostare un intervallo di selezione.  
  
### Per selezionare un intervallo di date  
  
1.  Creare gli oggetti <xref:System.DateTime> che rappresentano la prima e l'ultima data dell'intervallo.  
  
    ```vb  
    Dim projectStart As Date = New DateTime(2001, 2, 13)  
    Dim projectEnd As Date = New DateTime(2001, 2, 28)  
    ```  
  
    ```csharp  
    DateTime projectStart = new DateTime(2001, 2, 13);  
    DateTime projectEnd = new DateTime(2001, 2, 28);  
    ```  
  
    ```cpp  
    DateTime projectStart = DateTime(2001, 2, 13);  
    DateTime projectEnd = DateTime(2001, 2, 28);  
    ```  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A>.  
  
    ```vb  
    MonthCalendar1.SelectionRange = New SelectionRange(projectStart, projectEnd)  
    ```  
  
    ```csharp  
    monthCalendar1.SelectionRange = new SelectionRange(projectStart, projectEnd);  
    ```  
  
    ```cpp  
    monthCalendar1->SelectionRange = gcnew  
       SelectionRange(projectStart, projectEnd);  
    ```  
  
     Oppure  
  
     Impostare le proprietà <xref:System.Windows.Forms.MonthCalendar.SelectionStart%2A> e <xref:System.Windows.Forms.MonthCalendar.SelectionEnd%2A>.  
  
    ```vb  
    MonthCalendar1.SelectionStart = projectStart  
    MonthCalendar1.SelectionEnd = projectEnd  
    ```  
  
    ```csharp  
    monthCalendar1.SelectionStart = projectStart;  
    monthCalendar1.SelectionEnd = projectEnd;  
    ```  
  
    ```cpp  
    monthCalendar1->SelectionStart = projectStart;  
    monthCalendar1->SelectionEnd = projectEnd;  
    ```  
  
## Vedere anche  
 [Controllo MonthCalendar](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [Procedura: modificare l'aspetto del controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/how-to-change-monthcalendar-control-appearance.md)   
 [Procedura: visualizzare giorni specifici in grassetto con il controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/display-specific-days-in-bold-with-wf-monthcalendar-control.md)   
 [Procedura: visualizzare più mesi nel controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/display-more-than-one-month-wf-monthcalendar-control.md)