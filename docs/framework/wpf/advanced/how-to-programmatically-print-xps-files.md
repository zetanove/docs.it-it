---
title: "Procedura: stampa di file XPS a livello di codice | Microsoft Docs"
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
  - "stampa di file XPS a livello di codice"
  - "XPS (file), stampa a livello di codice"
ms.assetid: 0b1c0a3f-b19e-43d6-bcc9-eb3ec4e555ad
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: stampa di file XPS a livello di codice
È possibile utilizzare un overload del metodo <xref:System.Printing.PrintQueue.AddJob%2A> per stampare file [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] senza aprire un controllo <xref:System.Windows.Controls.PrintDialog> o, in generale, alcuna [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  
  
 È inoltre possibile stampare file [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] utilizzando i diversi metodi <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> e <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> della classe <xref:System.Windows.Xps.XpsDocumentWriter>.  Per ulteriori informazioni, vedere [Printing an XPS Document](http://msdn.microsoft.com/it-it/849555c8-0c4e-48c0-86bc-a5494c69b36c).  
  
 Un altro modo disponibile per stampare i file [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] consiste nell'utilizzare il metodo <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> o <xref:System.Windows.Controls.PrintDialog.PrintVisual%2A> del controllo <xref:System.Windows.Controls.PrintDialog>.  Vedere [Richiamare una finestra di dialogo di stampa](../../../../docs/framework/wpf/advanced/how-to-invoke-a-print-dialog.md).  
  
## Esempio  
 Di seguito sono elencati i passaggi principali da eseguire per utilizzare il metodo <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> con tre parametri.  Nell'esempio riportato di seguito vengono forniti i dettagli.  
  
1.  Determinare se la stampante è una stampante XPSDrv.  \(Per ulteriori informazioni su XPSDrv, vedere [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md).\)  
  
2.  Se la stampante non è una stampante XPSDrv, impostare l'apartment del thread su un thread singolo.  
  
3.  Creare un'istanza di un server di stampa e di un oggetto coda di stampa.  
  
4.  Chiamare il metodo, specificando un nome di processo, il file da stampare e un flag <xref:System.Boolean> per indicare se la stampante è o meno una stampante XPSDrv.  
  
 Nell'esempio riportato di seguito viene illustrato come stampare in modalità batch tutti i file [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] contenuti in una directory.  Sebbene venga richiesto all'utente di specificare la directory, il metodo <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> con tre parametri non richiede un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  Può essere utilizzato in qualsiasi percorso di codice in cui sia presente il nome e il percorso di un file [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] da passare.  
  
 L'overload del metodo <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> con tre parametri di <xref:System.Printing.PrintQueue.AddJob%2A> deve essere eseguito in un apartment a thread singolo ogni volta che il parametro <xref:System.Boolean> è `false`, ovvero ogni volta che viene utilizzata una stampante non XPSDrv.  Tuttavia, lo stato dell'apartment predefinito per [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] è a più thread.  Questa impostazione predefinita deve essere invertita in quanto nell'esempio si presuppone che venga utilizzata una stampante non XPSDrv.  
  
 Sono disponibili due modi per modificare l'impostazione predefinita.  Un modo consiste semplicemente nell'aggiungere <xref:System.STAThreadAttribute> \(ovvero "`[System.STAThreadAttribute()]`"\) appena sopra la prima riga del metodo `Main` dell'applicazione, in genere "`static void Main(string[] args)`".  Tuttavia, poiché molte applicazioni richiedono che per il metodo `Main` lo stato dell'apartment sia a più thread, è disponibile un secondo modo che consiste nell'inserire la chiamata a <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> in un thread separato il cui stato dell'apartment sia impostato su <xref:System.Threading.ApartmentState> con il metodo <xref:System.Threading.Thread.SetApartmentState%2A>.  Nell'esempio riportato di seguito viene utilizzata la seconda tecnica.  
  
 Di conseguenza, l'esempio prevede innanzitutto la creazione di un'istanza di un oggetto <xref:System.Threading.Thread> e il relativo passaggo al metodo **PrintXPS** come parametro <xref:System.Threading.ThreadStart>.  \(Il metodo **PrintXPS** verrà definito più avanti nell'esempio.\) In secondo luogo, il thread viene impostato su un apartment a thread singolo.  Il nuovo thread verrà avviato tramite il codice rimanente del metodo `Main`.  
  
 La parte fondamentale dell'esempio è rappresentata dal metodo `static` **BatchXPSPrinter.PrintXPS**.  Dopo avere creato un server di stampa e una coda, viene richiesto all'utente di specificare una directory contenente i file [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)].  Dopo che l'esistenza della directory e la presenza di file xps sono state accertate, ognuno di questi file viene aggiunto alla coda di stampa.  Poiché nell'esempio si presuppone che la stampante non sia XPSDrv, `false` viene passato all'ultimo parametro del metodo <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29>.  Per questo motivo, il markup [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] verrà convalidato nel file prima che venga convertito nel linguaggio di descrizione della pagina della stampante.  Se la convalida ha esito negativo, viene generata un'eccezione.  Nel codice di esempio l'eccezione viene rilevata e l'utente viene notificato, dopodiché viene elaborato il file [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] successivo.  
  
 [!code-csharp[BatchPrintXPSFiles#BatchPrintXPSFiles](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BatchPrintXPSFiles/CSharp/Program.cs#batchprintxpsfiles)]
 [!code-vb[BatchPrintXPSFiles#BatchPrintXPSFiles](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BatchPrintXPSFiles/visualbasic/program.vb#batchprintxpsfiles)]  
  
 Se si utilizza una stampante XPSDrv, è possibile impostare il parametro finale su `true`.  In questo caso, poiché [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] è il linguaggio di descrizione della pagina della stampante, il file verrà inviato alla stampante senza essere convalidato né convertito a un altro linguaggio di descrizione della pagina.  Se in fase di progettazione non si è certi se verrà effettivamente utilizzata una stampante XPSDrv, è possibile modificare l'applicazione affinché venga letta la proprietà <xref:System.Printing.PrintQueue.IsXpsDevice%2A> e la diramazione secondo quanto rilevato.  
  
 Poiché saranno poche le stampanti XPSDrv immediatamente disponibili dopo il rilascio di [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] e [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)], potrebbe essere necessario fare passare una stampante non XPSDrv per una stampante XPSDrv.  A tale scopo, aggiungere Pipelineconfig.xml all'elenco di file nella seguente chiave del Registro di sistema del computer che esegue l'applicazione:  
  
 HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Print\\Environments\\Windows NT x86\\Drivers\\Version\-3\\*\<PseudoXPSPrinter\>*\\DependentFiles  
  
 in cui *\<PseudoXPSPrinter\>* è una coda di stampa qualsiasi.  Riavviare il computer.  
  
 In questo modo, sarà possibile passare `true` come parametro finale del metodo <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> senza causare un'eccezione, tuttavia poiché *\<PseudoXPSPrinter\>* non è realmente una stampante XPSDrv, verrà stampato contenuto privo di significato.  
  
 **Nota** Per semplicità, nell'esempio viene utilizzata la presenza di un'estensione xps per stabilire se un file è [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)].  I file [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] non devono necessariamente avere questa estensione.  [isXPS.exe \(strumento di conformità isXPS\)](../Topic/isXPS.exe%20\(isXPS%20Conformance%20Tool\).md) rappresenta un modo per stabilire la validità dei file [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)].  
  
## Vedere anche  
 <xref:System.Printing.PrintQueue>   
 <xref:System.Printing.PrintQueue.AddJob%2A>   
 <xref:System.Threading.ApartmentState>   
 <xref:System.STAThreadAttribute>   
 [XPS](http://www.microsoft.com/xps)   
 [Printing an XPS Document](http://msdn.microsoft.com/it-it/849555c8-0c4e-48c0-86bc-a5494c69b36c)   
 [Managed and Unmanaged Threading](http://msdn.microsoft.com/it-it/db425c20-4b2f-4433-bf96-76071c7881e5)   
 [isXPS.exe \(strumento di conformità isXPS\)](../Topic/isXPS.exe%20\(isXPS%20Conformance%20Tool\).md)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)