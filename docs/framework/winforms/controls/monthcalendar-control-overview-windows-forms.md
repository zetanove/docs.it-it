---
title: "Cenni preliminari sul controllo MonthCalendar (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "MonthCalendar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "calendario (controlli), Windows Form"
  - "calendari, controlli Windows Form"
  - "MonthCalendar (controllo) [Windows Form], impostazione del primo giorno della settimana"
ms.assetid: 788c5325-b721-44ec-95bf-9b680ba0f6a2
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo MonthCalendar (Windows Form)
Il controllo <xref:System.Windows.Forms.MonthCalendar> Windows Form presenta agli utenti un'intuitiva interfaccia grafica per la visualizzazione e l'impostazione delle informazioni sulle date.  Tramite il controllo viene visualizzato un calendario: una griglia contenente i giorni del mese rappresentati da numeri e disposti in colonne in base ai giorni della settimana, in cui l'intervallo di date selezionate è evidenziato.  È possibile selezionare un diverso mese facendo clic sui pulsanti con le frecce su uno dei lati della didascalia del mese.  Diversamente dall'analogo controllo <xref:System.Windows.Forms.DateTimePicker>, consente di selezionare più di una data.  Per ulteriori informazioni sul controllo <xref:System.Windows.Forms.DateTimePicker>, vedere [Controllo DateTimePicker](../../../../docs/framework/winforms/controls/datetimepicker-control-windows-forms.md).  
  
## Configurazione del controllo MonthCalendar  
 L'aspetto del controllo <xref:System.Windows.Forms.MonthCalendar> è configurabile.  Per impostazione predefinita attorno alla data odierna è visualizzato un cerchio e la data è inoltre specificata nella parte inferiore della griglia.  È possibile modificare tale funzionalità impostando le proprietà <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> e <xref:System.Windows.Forms.MonthCalendar.ShowTodayCircle%2A> su `false`.  È inoltre possibile aggiungere i numeri delle settimane al calendario impostando la proprietà <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> su `true`.  Se si imposta la proprietà <xref:System.Windows.Forms.MonthCalendar.CalendarDimensions%2A>, è possibile visualizzare più mesi in orizzontale o in verticale.  Per impostazione predefinita il primo giorno della settimana visualizzato è la domenica ma è possibile designare qualsiasi giorno con la proprietà <xref:System.Windows.Forms.MonthCalendar.FirstDayOfWeek%2A>.  
  
 È inoltre possibile impostare la visualizzazione di determinate date in grassetto una volta sola, su base annua o mensile, aggiungendo oggetti <xref:System.DateTime> alle proprietà <xref:System.Windows.Forms.MonthCalendar.BoldedDates%2A>, <xref:System.Windows.Forms.MonthCalendar.AnnuallyBoldedDates%2A> e <xref:System.Windows.Forms.MonthCalendar.MonthlyBoldedDates%2A>.  Per ulteriori informazioni, vedere [Procedura: visualizzare giorni specifici in grassetto con il controllo MonthCalendar Windows Form](../../../../docs/framework/winforms/controls/display-specific-days-in-bold-with-wf-monthcalendar-control.md).  
  
 La proprietà chiave del controllo <xref:System.Windows.Forms.MonthCalendar> è <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A>, l'intervallo di date selezionate nel controllo.  Il valore di <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A> non deve superare il numero massimo di giorni selezionabili, impostato nella proprietà <xref:System.Windows.Forms.MonthCalendar.MaxSelectionCount%2A>.  La prima e l'ultima data che è possibile selezionare sono determinate dalle proprietà <xref:System.Windows.Forms.MonthCalendar.MaxDate%2A> e <xref:System.Windows.Forms.MonthCalendar.MinDate%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MonthCalendar>   
 [Controllo MonthCalendar](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)