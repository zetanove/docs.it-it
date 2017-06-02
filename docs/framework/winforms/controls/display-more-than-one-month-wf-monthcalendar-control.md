---
title: "Procedura: visualizzare pi&#249; mesi nel controllo MonthCalendar Windows Form | Microsoft Docs"
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
  - "calendari, formattazione della visualizzazione"
  - "calendari, più mesi"
  - "esempi [Windows Form], calendario (controlli)"
  - "MonthCalendar (controllo) [Windows Form], formattazione della visualizzazione"
ms.assetid: d197caa2-38a5-4cb4-acc3-562130c2ace3
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: visualizzare pi&#249; mesi nel controllo MonthCalendar Windows Form
Il controllo <xref:System.Windows.Forms.MonthCalendar> Windows Form è in grado di visualizzare fino a dodici mesi contemporaneamente.  Per impostazione predefinita, il controllo visualizza un solo mese, ma è possibile specificare il numero di mesi da visualizzare e la relativa disposizione all'interno del controllo.  Quando vengono modificate le dimensioni del calendario, il controllo viene ridimensionato in modo da garantire nel form uno spazio sufficiente per le nuove impostazioni.  
  
### Per visualizzare più mesi  
  
-   Impostare la proprietà <xref:System.Windows.Forms.MonthCalendar.CalendarDimensions%2A> sul numero di mesi da visualizzare orizzontalmente e verticalmente.  
  
    ```vb  
    MonthCalendar1.CalendarDimensions = New System.Drawing.Size (3,2)  
  
    ```  
  
    ```csharp  
    monthCalendar1.CalendarDimensions = new System.Drawing.Size (3,2);  
  
    ```  
  
    ```cpp  
    monthCalendar1->CalendarDimensions = System::Drawing::Size (3,2);  
    ```  
  
## Vedere anche  
 [Controllo MonthCalendar](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [Procedura: selezionare un intervallo di date nel controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)   
 [Procedura: modificare l'aspetto del controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/how-to-change-monthcalendar-control-appearance.md)