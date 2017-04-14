---
title: "Cenni preliminari sul controllo DateTimePicker (Windows Form) | Microsoft Docs"
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
  - "DateTimePicker"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli selezione data e ora"
  - "DateTimePicker (controllo) [Windows Form], informazioni"
ms.assetid: 501af106-e9fc-4efc-b9b3-c9d8dcaf8c5c
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Cenni preliminari sul controllo DateTimePicker (Windows Form)
Il controllo <xref:System.Windows.Forms.DateTimePicker> Windows Form consente di selezionare un singolo elemento da un elenco di date o ore.  Quando viene utilizzato per rappresentare una data, viene visualizzato in due parti: un elenco a discesa con data in forma di testo e una griglia visualizzata quando si fa clic sulla freccia di selezione accanto all'elenco.  La griglia è simile a quella del controllo <xref:System.Windows.Forms.MonthCalendar>, che può essere utilizzato per la selezione di più date.  Per ulteriori informazioni sul controllo <xref:System.Windows.Forms.MonthCalendar>, vedere [Cenni preliminari sul controllo MonthCalendar](../../../../docs/framework/winforms/controls/monthcalendar-control-overview-windows-forms.md).  
  
## Proprietà principali  
 Se si desidera che il controllo <xref:System.Windows.Forms.DateTimePicker> venga visualizzato come un controllo per la selezione o la modifica di ore anziché di date, impostare la proprietà <xref:System.Windows.Forms.DateTimePicker.ShowUpDown%2A> su `true` e la proprietà <xref:System.Windows.Forms.DateTimePicker.Format%2A> su <xref:System.Windows.Forms.DateTimePickerFormat>.  Per ulteriori informazioni, vedere [Procedura: visualizzare l'ora con il controllo DateTimePicker](../../../../docs/framework/winforms/controls/how-to-display-time-with-the-datetimepicker-control.md).  
  
 Quando la proprietà <xref:System.Windows.Forms.DateTimePicker.ShowCheckBox%2A> è impostata su `true`, nel controllo viene visualizzata una casella di controllo accanto alla data selezionata.  Quando la casella di controllo viene selezionata, è possibile aggiornare il valore data\-ora selezionato.  Quando la casella di controllo è deselezionata, il valore risulta non disponibile.  
  
 Le proprietà <xref:System.Windows.Forms.DateTimePicker.MaxDate%2A> e <xref:System.Windows.Forms.DateTimePicker.MinDate%2A> del controllo determinano l'intervallo di date e ore.  La proprietà <xref:System.Windows.Forms.DateTimePicker.Value%2A> contiene la data e l'ora correnti di impostazione del controllo.  Per informazioni dettagliate, vedere [Procedura: impostare e restituire date con il controllo DateTimePicker Windows Form](../../../../docs/framework/winforms/controls/how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md).  I valori possono essere visualizzati in quattro formati, impostati dalla proprietà <xref:System.Windows.Forms.DateTimePicker.Format%2A>: <xref:System.Windows.Forms.DateTimePickerFormat>, <xref:System.Windows.Forms.DateTimePickerFormat>, <xref:System.Windows.Forms.DateTimePickerFormat> o <xref:System.Windows.Forms.DateTimePickerFormat>.  Se viene selezionato un formato personalizzato, è necessario impostare la proprietà <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> su una stringa appropriata.  Per informazioni dettagliate, vedere [Procedura: visualizzare una data in un formato personalizzato con il controllo DateTimePicker di Windows Form](../../../../docs/framework/winforms/controls/display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md).  
  
## Vedere anche  
 [Procedura: visualizzare una data in un formato personalizzato con il controllo DateTimePicker di Windows Form](../../../../docs/framework/winforms/controls/display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)   
 [Procedura: impostare e restituire date con il controllo DateTimePicker Windows Form](../../../../docs/framework/winforms/controls/how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)