---
title: "UI Automation Support for Standard Controls | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controls, UI Automation support for"
  - "UI Automation, support for standard controls"
ms.assetid: 3770ea8a-2655-4add-9c59-fe0610ad5084
caps.latest.revision: 11
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 10
---
# UI Automation Support for Standard Controls
> [!NOTE]
>  Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Questo argomento contiene informazioni sul supporto di [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] per i controlli standard in applicazioni sviluppate per i framework [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Windows_Presentation_Foundation_Controls"></a>   
## Controlli WPF \(Windows Presentation Foundation\)  
 Tutti gli elementi di controllo [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] che forniscono informazioni o supporto per l'interazione dell'utente dispongono di supporto nativo completo per [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Gli altri elementi, ad esempio i pannelli, non sono visibile per [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
<a name="Win32_Controls"></a>   
## Controlli Win32  
 La maggior parte dei controlli [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] è esposta a [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] tramite provider lato client in UIAutomationClientsideProviders.dll. Questo assembly viene automaticamente registrato per l'uso con applicazioni client di automazione interfaccia utente.  
  
 Il supporto completo viene fornito solo per i controlli a partire dalla versione 6 di ComCtrl32.dll \(disponibile con [!INCLUDE[TLA#tla_winxp](../../../includes/tlasharptla-winxp-md.md)] e versioni successive\).  
  
 I controlli seguenti sono supportati.  
  
|Nome di classe|Tipo di controllo|  
|--------------------|-----------------------|  
|Button|Button|  
|Button|RadioButton|  
|Button|Group|  
|Button|CheckBox|  
|Button|Hyperlink|  
|Button|SplitButton|  
|Button|CheckBox|  
|ComboBoxEx32|ComboBox|  
|ComboBox|ComboBox|  
|Edit|Document|  
|Edit|Edit|  
|SysLink|Hyperlink|  
|Static|Text|  
|Static|Image|  
|SysIPAddress32|Custom|  
|SysHeader32|Header\/HeaderItem|  
|SysListView32|DataGrid|  
|SysListView32|List|  
|ListBox|List|  
|ListBox|ListItem|  
|\#32768|Menu|  
|\#32768|MenuItem|  
|msctls\_progress32|ProgressBar|  
|RichEdit|Document Vedere la nota.|  
|RichEdit20A|Document|  
|RichEdit20W|Document|  
|RichEdit50W|Document|  
|ScrollBar|Slider|  
|msctls\_trackbar32|Slider|  
|msctls\_updown32|Spinner|  
|msctls\_statusbar32|StatusBar|  
|SysTabControl32|Tab|  
|SysTabControl32|TabItem|  
|ToolbarWindow32|ToolBar|  
|ToolbarWindow32|MenuItem|  
|ToolbarWindow32|Pulsante|  
|ToolbarWindow32|CheckBox|  
|ToolbarWindow32|RadioButton|  
|ToolbarWindow32|Separator|  
|tooltips\_class32|ToolTip|  
|\#32774|ToolTip|  
|ReBarWindow32|ToolBar|  
|SysTreeView32|Tree|  
|SysTreeView32|TreeItem|  
  
 **Nota** Il controllo RichEdit è supportato solo per le versioni fornite con [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] \(in Riched20.dll versione 3.1 e successive e MsftEdit.dll versione 4.1 e successive\).  
  
 I controlli seguenti non sono supportati.  
  
|Nome di classe|Tipo di controllo|  
|--------------------|-----------------------|  
|SysAnimate32|Image|  
|SysPager|Spinner|  
|SysDateTimePick32|Custom|  
|SysMonthCal32|Calendar|  
|MS\_WINNOTE|Tooltip|  
|VBBubble|Tooltip|  
|ScrollBar \(se usato come controllo autonomo\)|Slider|  
|SuperGrid|Custom|  
  
<a name="Windows_Forms_Controls"></a>   
## Controlli per Windows Form  
 I controlli [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)] sono esposti a [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] tramite provider lato client in UIAutomationClientsideProviders.dll. Questo assembly viene automaticamente registrato per l'uso con applicazioni client di automazione interfaccia utente.  
  
 In genere, i controlli [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)] che sono wrapper gestiti per i controlli comuni [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] sono supportati da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. I controlli seguenti sono supportati.  
  
|Nome classe|  
|-----------------|  
|Button|  
|CheckBox|  
|CheckedListBox|  
|ColorDialog|  
|ComboBox|  
|FolderBrowser|  
|FontDialog|  
|GroupBox|  
|HscrollBar|  
|ImageList|  
|Label|  
|ListBox|  
|ListView|  
|MainMenu\/ContextMenu|  
|MonthCalendar|  
|NotifyIcon|  
|OpenFileDialog|  
|PageSetupDialog|  
|PrintDialog|  
|ProgressBar|  
|RadioButton|  
|RichTextBox|  
|SaveFileDialog|  
|ScrollableControl|  
|SoundPlayer|  
|StatusBar|  
|TabControl\/TabPage|  
|TextBox|  
|Timer|  
|ToolBar|  
|ToolTip|  
|Trackbar|  
|TreeView|  
|VscrollBar|  
|WebBrowser|  
  
 I seguenti controlli sono esposti a [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] solo tramite il relativo supporto per [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)]. Alcune funzionalità potrebbero non essere disponibili.  
  
|Nome controllo|  
|--------------------|  
|BindingSource|  
|DataGrid|  
|DataGridView|  
|DataNavigator|  
|DomainUpDown|  
|ErrorProvider|  
|FlowLayoutPanel|  
|Form|  
|LinkLabel|  
|HelpProvider|  
|MaskedTextBox|  
|MenuStrip\/ContextMenuStrip|  
|NumericUpDown|  
|Panel|  
|PictureBox|  
|PrintDocument|  
|PrintPreviewControl|  
|PrintPreviewDialog|  
|PropertyGrid|  
|UserControl|  
|ToolStrip|  
|TableLayoutPanel|  
|SplitContainer\/SplitterPanel|  
|Splitter|  
|RaftingContainer|  
|StatusStrip|  
  
## Vedere anche  
 [UI Automation Control Types](../../../docs/framework/ui-automation/ui-automation-control-types.md)