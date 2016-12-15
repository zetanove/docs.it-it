---
title: "Port Operations in the .NET Framework with Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ports, Visual Basic"
ms.assetid: 1eba223b-7bd3-401a-b097-982bce96df1b
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Port Operations in the .NET Framework with Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile accedere alle porte seriali del computer attraverso le classi [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] nello spazio nomi <xref:System.IO.Ports?displayProperty=fullName>.  La classe più importante, <xref:System.IO.Ports.SerialPort>, fornisce un framework per l'I\/O sincrono e basato su eventi, l'accesso agli stati di blocco e interruzione, l'accesso alle proprietà del driver seriale.  Può essere inserita in un oggetto <xref:System.IO.Stream>, accessibile attraverso la proprietà <xref:System.IO.Ports.SerialPort.BaseStream%2A>.  Inserendo <xref:System.IO.Ports.SerialPort> in un oggetto <xref:System.IO.Stream>, è possibile accedere alla porta seriale attraverso le classi che utilizzano i flussi.  Lo spazio nomi include le enumerazioni che semplificano il controllo delle porte seriali.  
  
 Il modo più semplice per creare un oggetto <xref:System.IO.Ports.SerialPort> è l'utilizzo del metodo <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>.  
  
> [!NOTE]
>  Non è possibile utilizzare le classi [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] per accedere direttamente ad altri tipi di porte, quali le porte parallele, le porte USB e così via.  
  
## Enumerazioni  
 In questa tabella vengono elencate e descritte le enumerazioni principali utilizzate per l'accesso alla porta seriale:  
  
|||  
|-|-|  
|Enumerazione|Descrizione|  
|<xref:System.IO.Ports.Handshake>|Consente di specificare il protocollo di controllo utilizzato per stabilire la comunicazione della porta seriale per un oggetto <xref:System.IO.Ports.SerialPort>.|  
|<xref:System.IO.Ports.Parity>|Consente di specificare il bit di parità per un oggetto <xref:System.IO.Ports.SerialPort>.|  
|<xref:System.IO.Ports.SerialData>|Consente di specificare il tipo di carattere ricevuto sulla porta seriale dell'oggetto <xref:System.IO.Ports.SerialPort>.|  
|<xref:System.IO.Ports.SerialError>|Consente di specificare l'errore che si è verificato nell'oggetto <xref:System.IO.Ports.SerialPort>|  
|<xref:System.IO.Ports.SerialPinChange>|Consente di specificare il tipo di modifica eseguita nell'oggetto <xref:System.IO.Ports.SerialPort>.|  
|<xref:System.IO.Ports.StopBits>|Consente di specificare il numero di bit di interruzione utilizzato nell'oggetto <xref:System.IO.Ports.SerialPort>.|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Ports>   
 [Accessing the Computer's Ports](../../../../visual-basic/developing-apps/programming/computer-resources/accessing-the-computer-s-ports.md)