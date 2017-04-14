---
title: "Esecuzione delle app .NET Framework 1.1 in Windows 8, Windows 8.1 o Windows 10 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework 1.1, esecuzione su Windows 8"
  - "Windows 8, esecuzione di applicazioni .NET Framework 1.1"
ms.assetid: fb14e195-fea5-4561-b9a8-60a67283edb9
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Esecuzione delle app .NET Framework 1.1 in Windows 8, Windows 8.1 o Windows 10
.NET Framework 1.1 non è supportato nei sistemi operativi [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)], [!INCLUDE[winserver8](../../../includes/winserver8-md.md)], [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] o Windows 10.  In alcuni casi, .NET Framework 1.1 viene identificato specificamente come obbligatorio per l'esecuzione di un'applicazione.  In questi casi, è necessario contattare il fornitore di software indipendente \(ISV\) per disporre dell'applicazione aggiornata da eseguire in [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] o versioni successive.  Per altre informazioni, vedere [Migrazione da .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md).  
  
## Installazione di .NET Framework 1.1 da un CD o dall'Area download  
 Non è possibile installare manualmente .NET Framework 1.1 in [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)], [!INCLUDE[winserver8](../../../includes/winserver8-md.md)], [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] o Windows 10.  e non è più supportato.  Se si tenta di installare il pacchetto, viene visualizzato il seguente messaggio di errore: "Impossibile continuare. La versione corrente di .NET Framework è incompatibile con una versione precedentemente installata". Per risolvere il problema, installare [.NET Framework 3.5 SP1](http://www.microsoft.com/it-it/download/details.aspx?id=22).  Questa versione include .NET Framework 2.0 \(la versione successiva a .NET Framework 1.1\), che è supportata da [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)] e Windows 10.  È consigliabile provare a installare sempre prima l'applicazione per determinare se verrà eseguito un aggiornamento automatico a una versione successiva di .NET Framework.  In caso contrario, contattare il fornitore di software indipendente \(ISV\) per un aggiornamento dell'applicazione.  
  
## Vedere anche  
 [Migrazione da .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)   
 [Installazione di .NET Framework 3.5 in Windows 8 e versioni successive](../../../docs/framework/install/net-framework-3-5-on-windows-8-plus.md)