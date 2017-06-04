---
title: "Reliability | Microsoft Docs"
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
  - "SQL Server [.NET Framework]"
  - "managed code, reliability"
  - "reliability [.NET Framework]"
  - "writing reliable code"
  - "code, reliability"
ms.assetid: 294aa306-0afe-4cbe-b397-86ba9f1860f8
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Reliability
È importante che il codice in esecuzione in ambienti server quale SQL Server garantisca protezione dalle eccezioni asincrone.  L'affidabilità, nei termini descritti in questo argomento, non è riferita specificamente a SQL Server, ma alla scrittura di codice affidabile per qualsiasi host in esecuzione in un ambiente .NET Framework versione 2.0.  Tuttavia, poiché SQL Server è il primo servizio che fa uso estensivo delle nuove funzionalità di ottimizzazione dell'affidabilità della versione 2.0, viene utilizzato come esempio.  
  
 Il codice in esecuzione in SQL Server deve rispettare indicazioni di affidabilità più severe rispetto ad altri ambienti server.  Ciò è dovuto al funzionamento stabile di SQL Server al bordo dell'utilizzo delle risorse.  <xref:System.OutOfMemoryException> ed eccezioni di <xref:System.Threading.ThreadAbortException> non vengono utilizzate nell'ambiente SQL Server.  Le presenti indicazioni sono inerenti, più che all'affidabilità, al modo in cui è possibile consentire l'interruzione regolare del codice gestito completamente attendibile a fronte del riciclo a livello di <xref:System.AppDomain>, che rappresenta il mezzo principale con cui il server mantiene la coerenza e l'affidabilità.  
  
## In questa sezione  
 [SQL Server Programming and Host Protection Attributes](../../../docs/framework/performance/sql-server-programming-and-host-protection-attributes.md)  
 Viene illustrata la modalità con cui SQL Server utilizza l'attributo <xref:System.Security.Permissions.HostProtectionAttribute> per limitare l'esecuzione del codice gestito.  
  
 [Reliability Best Practices](../../../docs/framework/performance/reliability-best-practices.md)  
 Vengono fornite indicazioni per la scrittura di codice che soddisfa i requisiti di affidabilità.  
  
 [Constrained Execution Regions](../../../docs/framework/performance/constrained-execution-regions.md)  
 Viene fornita una descrizione della funzione e del comportamento delle aree a esecuzione vincolata \(CER, Constrained Execution Region\).  
  
## Riferimenti  
 <xref:System.Security.Permissions.HostProtectionAttribute>  
  
 <xref:System.Security.Permissions.HostProtectionResource>