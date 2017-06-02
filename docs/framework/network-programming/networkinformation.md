---
title: "NetworkInformation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Rete"
ms.assetid: 31b44dd3-b903-4a48-8419-40419a3e4038
caps.latest.revision: 5
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 5
---
# NetworkInformation
Lo spazio dei nomi <xref:System.Net.NetworkInformation> consente di raccogliere informazioni sugli eventi, le modifiche, le statistiche e le proprietà della rete.  È anche possibile determinare se un host remoto è raggiungibile mediante la classe <xref:System.Net.NetworkInformation.Ping?displayProperty=fullName>.  
  
## Disponibilità e gli eventi della rete  
 La classe <xref:System.Net.NetworkInformation.NetworkChange?displayProperty=fullName> consente di determinare se l'indirizzo di rete o la disponibilità è stato modificato.  Per utilizzare questa classe, creare un gestore eventi per elaborare la modifica di un oggetto e associarlo a <xref:System.Net.NetworkInformation.NetworkAddressChangedEventHandler> o <xref:System.Net.NetworkInformation.NetworkAvailabilityChangedEventHandler>.  Per ulteriori informazioni, vedere [Procedura: Rilevare la disponibilità della rete e le modifiche all'indirizzo](../../../docs/framework/network-programming/how-to-detect-network-availability-and-address-changes.md).  
  
## Statistiche e proprietà di rete  
 È possibile raccogliere statistiche e le proprietà di rete su un'interfaccia o una base di protocollo.  <xref:System.Net.NetworkInformation.NetworkInterface>, <xref:System.Net.NetworkInformation.NetworkInterfaceType>e le classi <xref:System.Net.NetworkInformation.PhysicalAddress> forniscono informazioni su un'interfaccia di rete, mentre <xref:System.Net.NetworkInformation.IPInterfaceProperties>, <xref:System.Net.NetworkInformation.IPGlobalProperties>, <xref:System.Net.NetworkInformation.IPGlobalStatistics>, <xref:System.Net.NetworkInformation.TcpStatistics>e le classi <xref:System.Net.NetworkInformation.UdpStatistics> forniscono informazioni sui pacchetti di livello 3 e a 4.  Per ulteriori informazioni, vedere [Procedura: Ottenere informazioni su interfacce e protocolli](../../../docs/framework/network-programming/how-to-get-interface-and-protocol-information.md).  
  
## Determinare se un host remoto è raggiungibile  
 È possibile utilizzare la classe <xref:System.Net.NetworkInformation.Ping> per determinare se un host remoto su, in rete e raggiungibile.  Per ulteriori informazioni, vedere [Procedura: Eseguire il ping di un host](../../../docs/framework/network-programming/how-to-ping-a-host.md).  
  
## Vedere anche  
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [Esempio di Information Technology di rete](http://go.microsoft.com/fwlink/?LinkID=179564)   
 [Esempio di tecnologia dello strumento netstat](http://go.microsoft.com/fwlink/?LinkID=179562)   
 [esempio client di tecnologia di ping](http://go.microsoft.com/fwlink/?LinkID=179565)