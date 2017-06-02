---
title: "Attributi nei controlli Windows Form | Microsoft Docs"
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
  - "attributi [Windows Form]"
  - "attributi [Windows Form], classi"
  - "attributi [Windows Form], controlli (proprietà)"
  - "attributi [Windows Form], proprietà dell'associazione a dati"
ms.assetid: 2c5640e9-6c6c-49d7-a5e4-a768f6be7853
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Attributi nei controlli Windows Form
In .NET Framework sono disponibili vari attributi che possono essere applicati ai membri dei controlli e dei componenti personalizzati.  Alcuni di questi attributi influiscono sul comportamento di una classe in fase di esecuzione, mentre altri influiscono sul comportamento in fase di progettazione.  
  
## Attributi per le proprietà di controlli e componenti  
 Nella tabella riportata di seguito sono descritti gli attributi applicabili alle proprietà o ad altri membri dei controlli e dei componenti personalizzati.  Per un esempio in cui vengono utilizzati numerosi di questi attributi, vedere [Procedura: applicare attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-apply-attributes-in-windows-forms-controls.md).  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|<xref:System.ComponentModel.AmbientValueAttribute>|Specifica il valore da passare a una proprietà affinché questa ottenga il proprio valore da un'altra origine.  Questo concetto è noto come *ambiente*.|  
|<xref:System.ComponentModel.BrowsableAttribute>|Indica se visualizzare una proprietà o un evento in una finestra **Proprietà**.|  
|<xref:System.ComponentModel.CategoryAttribute>|Specifica il nome della categoria in cui raggruppare la proprietà o l'evento se visualizzato in un controllo <xref:System.Windows.Forms.PropertyGrid> impostato sulla modalità <xref:System.Windows.Forms.PropertySort>.|  
|<xref:System.ComponentModel.DefaultValueAttribute>|Specifica il valore predefinito per una proprietà.|  
|<xref:System.ComponentModel.DescriptionAttribute>|Specifica una descrizione per una proprietà o un evento.|  
|<xref:System.ComponentModel.DisplayNameAttribute>|Specifica il nome visualizzato per una proprietà, un evento o un metodo `public` `void` che non accetta argomenti.|  
|<xref:System.ComponentModel.EditorAttribute>|Specifica l'editor da utilizzare per modificare una proprietà.|  
|<xref:System.ComponentModel.EditorBrowsableAttribute>|Indica se una proprietà o un metodo è visualizzabile in un editor.|  
|<xref:System.ComponentModel.Design.HelpKeywordAttribute>|Specifica la parola chiave relativa al contesto per una classe o un membro.|  
|<xref:System.ComponentModel.LocalizableAttribute>|Indica se una proprietà deve essere localizzata.|  
|<xref:System.ComponentModel.PasswordPropertyTextAttribute>|Indica che la rappresentazione del testo di un oggetto è nascosta mediante caratteri, ad esempio asterischi.|  
|<xref:System.ComponentModel.ReadOnlyAttribute>|Indica se la proprietà a cui l'attributo è associato è di sola lettura o lettura\/scrittura in fase di progettazione.|  
|<xref:System.ComponentModel.RefreshPropertiesAttribute>|Indica se la griglia delle proprietà deve essere aggiornata quando il valore della proprietà associata viene modificato.|  
|<xref:System.ComponentModel.TypeConverterAttribute>|Specifica il tipo da utilizzare come convertitore per l'oggetto a cui l'attributo è associato.|  
  
## Attributi per le proprietà di associazione dati  
 Nella tabella riportata di seguito sono descritti gli attributi applicabili per specificare l'interazione tra i controlli e i componenti personalizzati e l'associazione dati.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|<xref:System.ComponentModel.BindableAttribute>|Indica se una proprietà è normalmente utilizzata per l'associazione.|  
|<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|Specifica le proprietà di origine dati e membro dati per un componente.|  
|<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|Specifica la proprietà di associazione predefinita per un componente.|  
|<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|Specifica le proprietà di origine dati e membro dati per un componente.|  
|<xref:System.ComponentModel.AttributeProviderAttribute>|Attiva il reindirizzamento degli attributi.|  
  
## Attributi per le classi  
 Nella tabella riportata di seguito sono descritti gli attributi applicabili per specificare il comportamento dei controlli e dei componenti personalizzati in fase di progettazione.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|<xref:System.ComponentModel.DefaultEventAttribute>|Specifica l'evento predefinito per un componente.|  
|<xref:System.ComponentModel.DefaultPropertyAttribute>|Specifica la proprietà predefinita per un componente.|  
|<xref:System.ComponentModel.DesignerAttribute>|Specifica la classe utilizzata per implementare i servizi in fase di progettazione per un componente.|  
|<xref:System.ComponentModel.DesignerCategoryAttribute>|Indica che la finestra di progettazione di una classe appartiene a una determinata categoria.|  
|<xref:System.ComponentModel.ToolboxItemAttribute>|Rappresenta un attributo di un elemento della Casella degli strumenti.|  
|<xref:System.ComponentModel.ToolboxItemFilterAttribute>|Specifica la stringa del filtro e il tipo di filtro da utilizzare per un elemento della Casella degli strumenti.|  
  
## Vedere anche  
 <xref:System.Attribute>   
 [Procedura: applicare attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-apply-attributes-in-windows-forms-controls.md)   
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)