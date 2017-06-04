---
title: "Procedura: visualizzare giorni specifici in grassetto con il controllo MonthCalendar Windows Form | Microsoft Docs"
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
  - "calendari, visualizzazione delle date in grassetto"
  - "esempi [Windows Form], calendario (controlli)"
  - "GetDayBold (evento)"
  - "MonthCalendar (controllo) [Windows Form], date visualizzate in grassetto"
ms.assetid: 8b20db5b-8118-4825-90e8-2c45c186ac7d
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: visualizzare giorni specifici in grassetto con il controllo MonthCalendar Windows Form
Il controllo <xref:System.Windows.Forms.MonthCalendar> Windows Form supporta la visualizzazione in grassetto dei giorni, sia di singole date che di date ripetute.  Ciò consente ad esempio di evidenziare date particolari, come giorni festivi e fine settimana.  
  
 Questa funzionalità è controllata da tre proprietà.  La proprietà <xref:System.Windows.Forms.MonthCalendar.BoldedDates%2A> contiene singole date,  la proprietà <xref:System.Windows.Forms.MonthCalendar.AnnuallyBoldedDates%2A> contiene date che vengono visualizzate in grassetto ogni anno,  la proprietà <xref:System.Windows.Forms.MonthCalendar.MonthlyBoldedDates%2A> contiene date che vengono visualizzate in grassetto ogni mese.  Ciascuna di queste proprietà contiene una matrice di oggetti <xref:System.DateTime>.  Per aggiungere o rimuovere una data da questi elenchi, è quindi necessario aggiungere o rimuovere un oggetto <xref:System.DateTime>.  
  
### Per visualizzare una data in grassetto  
  
1.  Creare due oggetti <xref:System.DateTime>.  
  
    ```vb  
    Dim myVacation1 As Date = New DateTime(2001, 6, 10)  
    Dim myVacation2 As Date = New DateTime(2001, 6, 17)  
  
    ```  
  
    ```csharp  
    DateTime myVacation1 = new DateTime(2001, 6, 10);  
    DateTime myVacation2 = new DateTime(2001, 6, 17);  
  
    ```  
  
    ```cpp  
    DateTime myVacation1 = DateTime(2001, 6, 10);  
    DateTime myVacation2 = DateTime(2001, 6, 17);  
    ```  
  
2.  Per impostare la visualizzazione in grassetto di una singola data, chiamare il metodo <xref:System.Windows.Forms.MonthCalendar.AddBoldedDate%2A>, <xref:System.Windows.Forms.MonthCalendar.AddAnnuallyBoldedDate%2A> o <xref:System.Windows.Forms.MonthCalendar.AddMonthlyBoldedDate%2A> del controllo <xref:System.Windows.Forms.MonthCalendar>.  
  
    ```vb  
    MonthCalendar1.AddBoldedDate(myVacation1)  
    MonthCalendar1.AddBoldedDate(myVacation2)  
  
    ```  
  
    ```csharp  
    monthCalendar1.AddBoldedDate(myVacation1);  
    monthCalendar1.AddBoldedDate(myVacation2);  
  
    ```  
  
    ```cpp  
    monthCalendar1->AddBoldedDate(myVacation1);  
    monthCalendar1->AddBoldedDate(myVacation2);  
    ```  
  
     Oppure  
  
     Per impostare la visualizzazione in grassetto di un insieme di date contemporaneamente, creare una matrice di oggetti <xref:System.DateTime> e assegnare la matrice a una proprietà.  
  
    ```vb  
    Dim VacationDates As DateTime() = {myVacation1, myVacation2}  
    MonthCalendar1.BoldedDates = VacationDates  
  
    ```  
  
    ```csharp  
    DateTime[] VacationDates = {myVacation1, myVacation2};  
    monthCalendar1.BoldedDates = VacationDates;  
  
    ```  
  
    ```cpp  
    Array<DateTime>^ VacationDates = {myVacation1, myVacation2};  
    monthCalendar1->BoldedDates = VacationDates;  
    ```  
  
### Per visualizzare una data in caratteri normali  
  
1.  Per impostare la visualizzazione in caratteri normali di una singola data in grassetto, chiamare il metodo <xref:System.Windows.Forms.MonthCalendar.RemoveBoldedDate%2A>, <xref:System.Windows.Forms.MonthCalendar.RemoveAnnuallyBoldedDate%2A> o <xref:System.Windows.Forms.MonthCalendar.RemoveMonthlyBoldedDate%2A>.  
  
    ```vb  
    MonthCalendar1.RemoveBoldedDate(myVacation1)  
    MonthCalendar1.RemoveBoldedDate(myVacation2)  
  
    ```  
  
    ```csharp  
    monthCalendar1.RemoveBoldedDate(myVacation1);  
    monthCalendar1.RemoveBoldedDate(myVacation2);  
  
    ```  
  
    ```cpp  
    monthCalendar1->RemoveBoldedDate(myVacation1);  
    monthCalendar1->RemoveBoldedDate(myVacation2);  
    ```  
  
     Oppure  
  
     Per rimuovere tutte le date in grassetto da uno dei tre elenchi, chiamare il metodo <xref:System.Windows.Forms.MonthCalendar.RemoveAllBoldedDates%2A>, <xref:System.Windows.Forms.MonthCalendar.RemoveAllAnnuallyBoldedDates%2A> o <xref:System.Windows.Forms.MonthCalendar.RemoveAllMonthlyBoldedDates%2A>.  
  
    ```vb  
    MonthCalendar1.RemoveAllBoldedDates()  
  
    ```  
  
    ```csharp  
    monthCalendar1.RemoveAllBoldedDates();  
  
    ```  
  
    ```cpp  
    monthCalendar1->RemoveAllBoldedDates();  
    ```  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.MonthCalendar.UpdateBoldedDates%2A> per aggiornare l'aspetto dei caratteri.  
  
    ```vb  
    MonthCalendar1.UpdateBoldedDates()  
  
    ```  
  
    ```csharp  
    monthCalendar1.UpdateBoldedDates();  
  
    ```  
  
    ```cpp  
    monthCalendar1->UpdateBoldedDates();  
    ```  
  
## Vedere anche  
 [Controllo MonthCalendar](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [Procedura: selezionare un intervallo di date nel controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)   
 [Procedura: modificare l'aspetto del controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/how-to-change-monthcalendar-control-appearance.md)   
 [Procedura: visualizzare più mesi nel controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/display-more-than-one-month-wf-monthcalendar-control.md)