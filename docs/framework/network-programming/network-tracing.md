---
title: "Tracciatura di rete in .NET Framework | Microsoft Docs"
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
  - "acquisizione del traffico di rete"
  - "debug [.NET Framework], tracciatura della rete"
  - "distribuzione di applicazioni [.NET Framework], traffico di rete"
  - "Internet, tracciatura della rete"
  - "chiamate ai metodi"
  - "metodi, tracciatura della rete"
  - "Risorse di rete"
  - "tracciatura della rete"
  - "tracciatura della rete, informazioni sulla tracciatura della rete"
  - "rete, tracciatura della rete"
  - "Rete"
  - "output, tracciatura della rete"
  - "debug con traccia attivata"
  - "traccia [.NET Framework], rete"
  - "tracciatura del traffico"
ms.assetid: e993b7c3-087f-45d8-9c02-9dded936d804
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Tracciatura di rete in .NET Framework
La funzionalità di traccia di rete in .NET Framework consente di accedere alle informazioni sulle chiamate ai metodi e sul traffico di rete generato da un'applicazione gestita.  Questa funzionalità è utile per il debug delle applicazioni in fase di sviluppo, nonché per l'analisi delle applicazioni distribuite.  È possibile personalizzare l'output generato dalla tracciatura della rete per supportare differenti scenari di utilizzo in fase di sviluppo e nell'ambiente di produzione.  
  
 Per abilitare la traccia di rete in .NET Framework, è necessario selezionare una destinazione per l'output della traccia e aggiungere impostazioni di configurazione della traccia di rete al file di configurazione dell'applicazione o del computer.  Per informazioni sui file di configurazione e sul relativo utilizzo, vedere [File di configurazione](../../../docs/framework/configure-apps/index.md).  Per informazioni su come abilitare la traccia di rete, vedere [Abilitazione della traccia di rete](../../../docs/framework/network-programming/enabling-network-tracing.md).  Per informazioni sulle impostazioni che è necessario aggiungere al file di configurazione, vedere [Procedura: Configurare la traccia di rete](../../../docs/framework/network-programming/how-to-configure-network-tracing.md).  
  
 Quando la funzionalità di traccia è abilitata, è possibile acquisire le informazioni di traccia che vengono restituite dalle classi di **System.Net**.  I membri delle classi della rete che generano le informazioni sulla traccia includono la nota riportata nella sezione relativa alle osservazioni della relativa documentazione della libreria di classi di .NET Framework:  
  
> [!NOTE]
>  Questo membro genera informazioni di traccia quando viene abilitata la funzionalità di traccia di rete nell'applicazione in uso.  Per ulteriori informazioni, vedere Traccia di rete.  
  
## Vedere anche  
 [Abilitazione della traccia di rete](../../../docs/framework/network-programming/enabling-network-tracing.md)   
 [Procedura: Configurare la tracciatura della rete](../../../docs/framework/network-programming/how-to-configure-network-tracing.md)   
 [Interpretazione della traccia di rete](../../../docs/framework/network-programming/interpreting-network-tracing.md)   
 [Introduction to Instrumentation and Tracing](http://msdn.microsoft.com/it-it/e924e57c-33cf-4b0e-9e7f-a45d13e38f2c)