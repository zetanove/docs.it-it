---
title: "Procedura: richiamare una finestra di dialogo di stampa | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "chiamata di finestre di dialogo per la stampa"
  - "finestre di dialogo per la stampa, chiamata"
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: richiamare una finestra di dialogo di stampa
Per consentire la stampa dall'applicazione, è possibile semplicemente creare e aprire un oggetto <xref:System.Windows.Controls.PrintDialog>.  
  
## Esempio  
 Il controllo <xref:System.Windows.Controls.PrintDialog> rappresenta un singolo punto di ingresso per l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], la configurazione e l'invio di processi [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)].  Per il controllo, semplice da utilizzare, si possono creare istanze utilizzando markup [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] o codice.  Nell'esempio riportato di seguito viene illustrato come creare istanze, aprire il controllo nel codice e stampare.  Viene inoltre illustrato come verificare che la finestra di dialogo consenta all'utente la possibilità di impostare un intervallo specifico di pagine.  Nell'esempio di codice si presuppone la presenza di un file FixedDocumentSequence.xps nella radice dell'unità C.  
  
 [!code-csharp[printdialog#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 Una volta aperta la finestra di dialogo, gli utenti potranno scegliere tra le stampanti installate sul computer.  Sarà possibile anche selezionare [Microsoft XPS Document Writer](http://go.microsoft.com/fwlink/?LinkId=147319) \(la pagina potrebbe essere in inglese\) per creare un file [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] anziché stampare.  
  
> [!NOTE]
>  Il controllo <xref:System.Windows.Controls.PrintDialog?displayProperty=fullName> di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], illustrato in questo argomento, non deve essere confuso con il componente <xref:System.Windows.Forms.PrintDialog?displayProperty=fullName> di [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)].  
  
 In teoria, è possibile utilizzare il metodo <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> senza mai aprire la finestra di dialogo.  Infatti il controllo può essere utilizzato come un componente di stampa non visibile.  Ma per motivi di prestazioni, sarebbe meglio utilizzare il metodo <xref:System.Printing.PrintQueue.AddJob%2A> o uno dei molti metodi <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> e <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> di <xref:System.Windows.Xps.XpsDocumentWriter>.  Per ulteriori informazioni su questo argomento, vedere [Stampa di file XPS a livello di codice](../../../../docs/framework/wpf/advanced/how-to-programmatically-print-xps-files.md) e .  
  
## Vedere anche  
 <xref:System.Windows.Controls.PrintDialog>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Microsoft XPS Document Writer](http://go.microsoft.com/fwlink/?LinkId=147319)