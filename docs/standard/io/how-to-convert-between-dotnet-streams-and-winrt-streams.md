---
title: "Procedura: eseguire la conversione tra flussi di .NET Framework e flussi di Windows Runtime | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 23a763ea-8348-4244-9f8c-a4280b870b47
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: eseguire la conversione tra flussi di .NET Framework e flussi di Windows Runtime
.NET Framework per le applicazioni Windows Store è un subset della versione completa di .NET Framework. Per motivi di sicurezza e di altri requisiti per le applicazioni Windows Store, non è possibile usare l'Integer set di API di .NET Framework per aprire e leggere i file. Per altre informazioni, vedere [Panoramica di .NET per le applicazioni Windows Store](http://msdn.microsoft.com/library/windows/apps/br230302.aspx). Tuttavia, è possibile usare le API di .NET Framework per altre operazioni di manipolazione di un flusso. Per modificare questi flussi, potrebbe essere necessario effettuare la conversione tra un tipo di flusso di .NET Framework come <xref:System.IO.MemoryStream> o <xref:System.IO.FileStream> e un flusso di Windows Runtime come [IInputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.iinputstream.aspx), [IOutputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.ioutputstream.aspx) o [IRandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx).  
  
 La classe <xref:System.IO.WindowsRuntimeStreamExtensions> contiene metodi che semplificano queste conversioni. Tuttavia, esistono differenze sottostanti tra flussi in .NET Framework e Windows Runtime che avranno effetto sui risultati dell'utilizzo di questi metodi. I dettagli sono descritti nelle sezioni seguenti.  
  
<a name="BKMK_ConvertingfromaWindowsRuntimestreamtoaNETFrameworkstream"></a>   
## Conversione da un flusso di Windows Runtime nel flusso di .NET Framework  
 È possibile convertire un flusso di Windows Runtime nel flusso di .NET Framework usando uno dei seguenti metodi <xref:System.IO.WindowsRuntimeStreamExtensions>:  
  
 <xref:System.IO.WindowsRuntimeStreamExtensions.AsStream%2A>  
 Converte un flusso ad accesso casuale in Windows Runtime in un flusso gestito nel subset di .NET per applicazioni Windows Store.  
  
 <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForWrite%2A>  
 Converte un flusso di output in Windows Runtime in un flusso gestito nel subset di .NET per applicazioni Windows Store.  
  
 <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead%2A>  
 Converte un flusso di input in Windows Runtime in un flusso gestito nel subset di .NET per applicazioni Windows Store.  
  
 Windows Runtime offre tipi di flusso che supportano solo lettura, solo scrittura o lettura e scrittura e queste funzionalità vengono mantenute quando si converte un flusso di Windows Runtime in un flusso di .NET Framework. Inoltre, se un flusso di Windows Runtime viene convertito in un flusso di .NET Framework e viceversa, si ottiene l'istanza originale di Windows Runtime. È consigliabile usare il metodo di conversione corrispondente alle funzionalità del flusso di Windows Runtime che si desidera convertire. Tuttavia, poiché [IRandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx) è leggibile e modificabile \(implementa sia [IOutputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.ioutputstream.aspx) sia [IInputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.iinputstream.aspx)\), è possibile usare uno dei metodi di conversione e le funzionalità del flusso originale vengono mantenute. Ad esempio, usando <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead%2A> per convertire [IRandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx) il flusso convertito di .NET Framework non sarà limitato alla sola lettura, ma sarà anche modificabile.  
  
#### Per convertire un flusso ad accesso casuale di Windows Runtime in un flusso di .NET Framework  
  
-   Usare il metodo <xref:System.IO.WindowsRuntimeStreamExtensions.AsStream%2A>.  
  
     L'esempio di codice seguente mostra come chiedere all'utente di selezionare un file, aprirlo con le API di Windows Runtime e convertirlo in un flusso di .NET Framework, che viene letto e restituito in un blocco di testo. In questo scenario, il flusso viene in genere manipolato tramite le API di .NET Framework prima di restituire i risultati.  
  
     Per eseguire l'esempio, è necessario creare un'applicazione Windows Store in XAML che contiene un blocco di testo denominato `TextBlock1` e un pulsante denominato `Button1`. L'evento click del pulsante deve essere associato al metodo `button1_Click` illustrato nell'esempio.  
  
     [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#imports)]
     [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#imports)]  
    [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#1)]
    [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#1)]  
  
<a name="BKMK_ConvertingfromaNETFrameworkstreamtoaWindowsRuntimestream"></a>   
## Conversione da un flusso di .NET Framework nel flusso di Windows Runtime  
 È possibile convertire un flusso di .NET Framework nel flusso di Windows Runtime usando uno dei seguenti metodi <xref:System.IO.WindowsRuntimeStreamExtensions>:  
  
 <xref:System.IO.WindowsRuntimeStreamExtensions.AsInputStream%2A>  
 Converte un flusso gestito nel subset di .NET per applicazioni Windows Store in un flusso di input in Windows Runtime.  
  
 <xref:System.IO.WindowsRuntimeStreamExtensions.AsOutputStream%2A>  
 Converte un flusso gestito nel subset di .NET per applicazioni Windows Store in un flusso di output in Windows Runtime.  
  
 [AsRandomAccessStream](../../../docs/standard/cross-platform/windowsruntimestreamextensions-asrandomaccessstream-method.md)  
 Converte un flusso gestito nel subset di .NET per applicazioni Windows Store in un flusso ad accesso casuale che può essere usato per la lettura o scrittura in Windows Runtime.  
  
 Quando si converte un flusso di .NET Framework in un flusso di Windows Runtime, le funzionalità del flusso convertito dipenderanno dal flusso originale. Ad esempio, se il flusso originale supporta sia la lettura che la scrittura e si chiama <xref:System.IO.WindowsRuntimeStreamExtensions.AsInputStream%2A> per convertire il flusso, il tipo restituito sarà `IRandomAccessStream`, che implementa `IInputStream` e `IOutputStream` e supporta lettura e scrittura  
  
 I flussi di .NET Framework non supportano la clonazione, anche dopo la conversione. Ciò significa che se si converte un flusso di .NET Framework in un flusso di Windows Runtime e si chiama [GetInputStreamAt](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.inmemoryrandomaccessstream.getinputstreamat.aspx) o [GetOutputStreamAt](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.getoutputstreamat.aspx), che chiama [CloneStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.randomaccessstreamoverstream.clonestream.aspx) o chiama [CloneStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.randomaccessstreamoverstream.clonestream.aspx) direttamente, si verificherà un'eccezione.  
  
#### Per convertire un flusso di .NET Framework in un flusso ad accesso casuale di Windows Runtime  
  
-   Usare il metodo [AsRandomAccessStream](../../../docs/standard/cross-platform/windowsruntimestreamextensions-asrandomaccessstream-method.md), come illustrato nell'esempio seguente.  
  
    > [!IMPORTANT]
    >  Assicurarsi che il flusso di .NET Framework usato supporti la ricerca oppure copiarlo in un flusso che la supporti. A tale scopo, è possibile usare la proprietà <xref:System.IO.Stream.CanSeek%2A?displayProperty=fullName>.  
  
     Per eseguire l'esempio, è necessario creare un'applicazione Windows Store in XAML destinata a .NET Framework 4.5.1 contenente un blocco di testo denominato `TextBlock2` e un pulsante denominato `Button2`. L'evento click del pulsante deve essere associato al metodo `button2_Click` illustrato nell'esempio.  
  
     [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#imports)]
     [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#imports)]  
    [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#2)]
    [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#2)]  
  
## Vedere anche  
 [Guida rapida: Lettura e scrittura di un file \(Windows\)](http://msdn.microsoft.com/library/windows/apps/hh464978.aspx)   
 [Panoramica di .NET per le app di Windows Store](http://msdn.microsoft.com/library/windows/apps/br230302.aspx)   
 [.NET per le app di Windows Store: API supportate](http://msdn.microsoft.com/library/windows/apps/br230232.aspx)