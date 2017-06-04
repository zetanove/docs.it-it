---
title: "Metodo WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "System.IO.WindowsRuntimeStreamExtensions.AsRandomAccessStream"
apilocation: 
  - "System.Runtime.WindowsRuntime.dll"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: dcc72283-caed-49ee-b45d-ccaf94e97129
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# Metodo WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream)
\[Supportato in .NET Framework 4.5.1 e versioni successive\]  
  
 Converte il flusso specificato in un flusso di accesso casuale.  
  
 **Spazio dei nomi:** <xref:System.IO?displayProperty=fullName>   
 **Assembly:** System.Runtime.WindowsRuntime \(in System.Runtime.WindowsRuntime.dll\)  
  
## Sintassi  
  
```csharp  
[CLSCompliantAttribute(false)] public static  IRandomAccessStream AsRandomAccessStream(Stream stream)   
```  
  
```vb  
'Declaration <ExtensionAttribute> _ <CLSCompliantAttribute(False)> _ Public Shared Function AsRandomAccessStream ( _         stream As Stream) As IRandomAccessStream   
```  
  
#### Parametri  
 `stream`  
  
 Tipo: <xref:System.IO.Stream?displayProperty=fullName>   
 Flusso da convertire.  
  
## Valore restituito  
 Tipo: [Windows.Storage.Streams.RandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.randomaccessstream.aspx)   
 Flusso ad accesso casuale [!INCLUDE[wrt](../../../includes/wrt-md.md)], che rappresenta il flusso convertito.  
  
## Eccezioni  
  
|Eccezione|Condizione|  
|---------------|----------------|  
|<xref:System.NotSupportedException>|Il flusso da convertire non supporta la ricerca.|  
  
## Note  
 Questo metodo di estensione è disponibile solo quando si sviluppano applicazioni Windows Store.  Questo metodo fornisce un modo conveniente per lavorare con i flussi nelle applicazioni Windows Store.  Il flusso .NET Framework da convertire deve supportare la ricerca.  Per altre informazioni, vedere il metodo <xref:System.IO.Stream.Seek%2A?displayProperty=fullName>.  
  
> [!IMPORTANT]
>  Questa API è supportata in .NET Framework 4.5.1 e nelle versioni successive, ma non nella versione 4.5.  
  
## Informazioni sulla versione  
 **.NET per applicazioni Windows Store**  
  
 Supportato in: Windows 8.1  
  
## Vedere anche  
 <xref:System.IO.WindowsRuntimeStreamExtensions>   
 [Procedura: eseguire la conversione tra flussi di .NET Framework e flussi di Windows Runtime](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)