---
title: "Procedura: visualizzare una data in un formato personalizzato con il controllo DateTimePicker di Windows Form | Microsoft Docs"
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
  - "date, visualizzazione nel controllo DateTimePicker"
  - "DateTimePicker (controllo) [Windows Form], stili di visualizzazione"
  - "esempi [Windows Form], DateTimePicker (controllo)"
ms.assetid: 39767691-2d2b-46b6-a663-b7901e581a6e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: visualizzare una data in un formato personalizzato con il controllo DateTimePicker di Windows Form
Il controllo <xref:System.Windows.Forms.DateTimePicker> di Windows Form consente di formattare in modo flessibile le date e le ore visualizzate nel controllo.  La proprietà <xref:System.Windows.Forms.DateTimePicker.Format%2A> consente di selezionare uno dei formati predefiniti elencati nell'enumerazione <xref:System.Windows.Forms.DateTimePickerFormat>.  Se nessuno dei formati soddisfa le proprie esigenze, è possibile creare un formato personalizzato utilizzando i caratteri di formato elencati in <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A>.  
  
### Per visualizzare un formato personalizzato  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.DateTimePicker.Format%2A> su `DateTimePickerFormat.Custom`.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> su una stringa di formato.  
  
    ```vb  
    DateTimePicker1.Format = DateTimePickerFormat.Custom  
    ' Display the date as "Mon 27 Feb 2012".  
    DateTimePicker1.CustomFormat = "ddd dd MMM yyyy"  
  
    ```  
  
    ```csharp  
    dateTimePicker1.Format = DateTimePickerFormat.Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1.CustomFormat = "ddd dd MMM yyyy";  
  
    ```  
  
    ```cpp  
    dateTimePicker1->Format = DateTimePickerFormat::Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1->CustomFormat = "ddd dd MMM yyyy";  
    ```  
  
### Per aggiungere testo al valore formattato  
  
1.  Utilizzare le virgolette singole per racchiudere i caratteri che non rappresentano elementi di formato, ad esempio "M", o di delimitazione, ad esempio ":".  La stringa di formato riportata di seguito, ad esempio, visualizza la data corrente nel formato "Today is: 05:30:31 Friday March 02, 2012" nelle impostazioni cultura lingua inglesi \(Stati Uniti\).  
  
    ```vb  
    DateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy"  
  
    ```  
  
    ```csharp  
    dateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
  
    ```  
  
    ```cpp  
    dateTimePicker1->CustomFormat =  
       "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
    ```  
  
     In base alle impostazioni cultura, qualsiasi carattere non racchiuso tra virgolette singole può essere modificato.  La stringa di formato riportata sopra, ad esempio, visualizza la data corrente nel formato "Today is: 05:30:31 Friday March 02, 2012" nelle impostazioni cultura inglesi \(Stati Uniti\).  Notare che il primo segno di due punti è racchiuso tra virgolette singole, poiché non viene utilizzato come carattere di delimitazione come avviene in "hh:mm:ss".  In altre impostazioni cultura, il formato potrebbe essere visualizzato come "Today is: 05.30.31 Friday March 02, 2012".  
  
## Vedere anche  
 [Controllo DateTimePicker](../../../../docs/framework/winforms/controls/datetimepicker-control-windows-forms.md)   
 [Procedura: impostare e restituire date con il controllo DateTimePicker Windows Form](../../../../docs/framework/winforms/controls/how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)