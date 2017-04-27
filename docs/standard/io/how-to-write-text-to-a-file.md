---
title: "Procedura: Scrivere un testo in un file | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "scrittura di testo nei file"
  - "I/O [.NET Framework], scrittura di testo nei file"
  - "flussi, scrittura di testo nei file"
  - "flussi di dati, scrittura di testo nei file"
ms.assetid: 060cbe06-2adf-4337-9e7b-961a5c840208
caps.latest.revision: 29
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 29
---
# Procedura: Scrivere un testo in un file
Questo argomento illustra diverse modalità con cui è possibile scrivere un testo in un file per le applicazioni .NET Framework o le app di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Per scrivere un testo in un file vengono in genere usati le classi e i metodi seguenti:  
  
-   <xref:System.IO.StreamWriter>: contiene i metodi per scrivere in un file in modo sincrono \(<xref:System.IO.StreamWriter.Write%2A> o <xref:System.IO.TextWriter.WriteLine%2A>\) o in modo asincrono \(<xref:System.IO.StreamWriter.WriteAsync%2A> e <xref:System.IO.StreamWriter.WriteLineAsync%2A>\).  
  
-   <xref:System.IO.File>: da usare con le applicazioni .NET Framework. Fornisce i metodi statici per scrivere un testo in un file, ad esempio <xref:System.IO.File.WriteAllLines%2A> e <xref:System.IO.File.WriteAllText%2A>, o per aggiungere un testo in un file \(<xref:System.IO.File.AppendAllLines%2A>, <xref:System.IO.File.AppendAllText%2A> o <xref:System.IO.File.AppendText%2A>\).  
  
-   [FileIO](https://msdn.microsoft.com/library/windows/apps/windows.storage.fileio.aspx): da usare con le app di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Contiene i metodi asincroni per scrivere un testo in un file \([WriteLinesAsync](https://msdn.microsoft.com/library/windows/apps/windows.storage.fileio.writelinesasync.aspx) o [WriteTextAsync](https://msdn.microsoft.com/library/windows/apps/windows.storage.fileio.writetextasync.aspx)\) o per aggiungere un testo in un file \([AppendLinesAsync](https://msdn.microsoft.com/library/windows/apps/windows.storage.fileio.appendlinesasync.aspx) o [AppendTextAsync](https://msdn.microsoft.com/library/windows/apps/windows.storage.fileio.appendtextasync.aspx)\).  
  
 Gli esempi sono semplici per concentrarsi sull'attività da eseguire. Per questo motivo, gli esempi eseguono eventualmente delle procedure minime di controllo degli errori e di gestione delle eccezioni. Un'applicazione reale fornisce in genere procedure di controllo degli errori e di gestione delle eccezioni più efficaci.  
  
## Esempio  
 L'esempio seguente illustra come scrivere in modo sincrono un testo una riga alla volta in un nuovo file usando la classe <xref:System.IO.StreamWriter>. Il nuovo file di testo viene salvato nella cartella Documenti dell'utente. Poiché l'oggetto <xref:System.IO.StreamWriter> viene dichiarato in un'istruzione `using` in cui viene creata anche un'istanza dell'oggetto stesso, viene richiamato il metodo <xref:System.IO.StreamWriter.Dispose%2A> che scarica e chiude automaticamente il flusso.  
  
 <!-- TODO: review snippet reference [!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source.cs#writeline)]  -->
 <!-- TODO: review snippet reference [!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source.vb#writeline)]  -->  
  
## Esempio  
 L'esempio seguente illustra come aggiungere un testo in un file esistente usando la classe <xref:System.IO.StreamWriter>. Viene usato lo stesso file di testo dell'esempio precedente.  
  
 <!-- TODO: review snippet reference [!code-csharp[Conceptual.BasicIO.TextFiles#AppendText](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source.cs#appendtext)]  -->
 <!-- TODO: review snippet reference [!code-vb[Conceptual.BasicIO.TextFiles#AppendText](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source.vb#appendtext)]  -->  
  
## Esempio  
 L'esempio seguente illustra come scrivere in modo asincrono un testo in un nuovo file usando la classe <xref:System.IO.StreamWriter>. Per richiamare il metodo <xref:System.IO.StreamWriter.WriteAsync%2A>, la chiamata al metodo deve essere eseguita all'interno di un metodo `async`. Il nuovo file di testo viene salvato nella cartella Documenti dell'utente.  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#WriteAsync](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source.cs#writeasync)]
 [!code-vb[Conceptual.BasicIO.TextFiles#WriteAsync](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source.vb#writeasync)]  
  
## Esempio  
 L'esempio seguente illustra come scrivere un testo in un nuovo file e aggiungere nuove righe di testo nello stesso file usando la classe <xref:System.IO.File>. I metodi <xref:System.IO.File.WriteAllText%2A> e <xref:System.IO.File.AppendAllLines%2A> aprono e chiudono automaticamente il file. Se il percorso fornito al metodo <xref:System.IO.File.WriteAllText%2A> esiste già, il file verrà sovrascritto.  
  
 [!code-csharp[Conceptual.BasicIO.TextFiles#WriteFile](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source.cs#writefile)]
 [!code-vb[Conceptual.BasicIO.TextFiles#WriteFile](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source.vb#writefile)]  
  
## Esempio  
 L'esempio seguente mostra come scrivere l'input dell'utente in modo asincrono in un file di testo di un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Per motivi di sicurezza, l'apertura di un file da un'app di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] richiede in genere l'uso di un controllo [FileOpenPicker](http://msdn.microsoft.com/library/windows/apps/windows.storage.pickers.fileopenpicker.aspx). In questo esempio, `FileOpenPicker` è filtrato per mostrare i file di testo.  
  
```xaml  
<Page  
    x:Class="OpenFileWindowsStore.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:local="using:OpenFileWindowsStore"  
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    mc:Ignorable="d">  
  
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">  
        <Button Content="save text to a file" HorizontalAlignment="Left" Margin="103,417,0,0" VerticalAlignment="Top"   
                Width="329" Height="86" FontSize="35" Click="Button_Click"/>  
        <TextBox Name="UserInputTextBox"  FontSize="18" HorizontalAlignment="Left" Margin="106,146,0,0"   
                 TextWrapping="Wrap" Text="Write some text here, and select a file to write it to." VerticalAlignment="Top"   
                 Height="201" Width="558" AcceptsReturn="True"/>  
        <TextBlock Name="StatusTextBox" HorizontalAlignment="Left" Margin="106,570,0,147" TextWrapping="Wrap" Text="Status:"   
                   VerticalAlignment="Center" Height="51" Width="1074" FontSize="18" />  
    </Grid>  
</Page>  
```  
  
 [!code-csharp[OpenFileWindowsStore#Code](../../../samples/snippets/csharp/VS_Snippets_CLR/openfilewindowsstore/cs/mainpage.xaml.cs#code)]
 [!code-vb[OpenFileWindowsStore#Code](../../../samples/snippets/visualbasic/VS_Snippets_CLR/openfilewindowsstore/vb/mainpage.xaml.vb#code)]  
  
## Vedere anche  
 <xref:System.IO.StreamWriter>   
 <xref:System.IO.File.CreateText%2A?displayProperty=fullName>   
 [Procedura: enumerare directory e file](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [Procedura: leggere e scrivere su un file di dati appena creato](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [Procedura: Aprire e accodare un file di log](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [I\/O di file e di flussi](../../../docs/standard/io/index.md)