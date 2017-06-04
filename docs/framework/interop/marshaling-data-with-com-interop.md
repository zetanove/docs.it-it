---
title: "Marshaling Data with COM Interop | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "COM interop, data marshaling"
  - "marshaling data, COM interop"
ms.assetid: 0bcdd7bf-5026-43eb-b08b-f03f90db9df9
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Marshaling Data with COM Interop
Grazie all'interoperabilità COM, è possibile usare oggetti COM dal codice gestito ed esporre oggetti gestiti a COM.  Il supporto per il marshalling dei dati verso e da COM è estensivo e garantisce sempre il comportamento di marshalling corretto.  
  
 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] include i seguenti strumenti di interoperabilità COM:  
  
-   [Utilità di importazione della libreria dei tipi \(Tlbimp.exe\),](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) che consente di convertire una libreria dei tipi COM in un assembly di interoperabilità,  dal quale, con il servizio di marshalling di interoperabilità, vengono generati wrapper per il marshalling dei dati tra memoria gestita e non gestita.  
  
-   [Utilità di esportazione della libreria dei tipi \(Tlbexp.exe\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md), che consente di generare una libreria dei tipi COM da un assembly e un wrapper per l'esecuzione del marshalling durante le chiamate ai metodi.  
  
 Questa sezione descrive i processi per la personalizzazione dei wrapper di interoperabilità quando è possibile o necessario fornire altre informazioni sui tipi al gestore di marshalling.  
  
## In questa sezione  
 [Tipi di dati COM](http://msdn.microsoft.com/it-it/f93ae35d-a416-4218-8700-c8218cc90061)  
 Fornisce i tipi di dati gestiti e non gestiti corrispondenti.  
  
 [Personalizzazione di wrapper COM richiamabili](http://msdn.microsoft.com/it-it/825177d3-4b2c-4723-82be-ce6ca2c34ace)  
 Descrive come eseguire esplicitamente il marshalling dei tipi di dati tramite l'attributo **MarshalAsAttribute** in fase di progettazione.  
  
 [Personalizzazione dei wrapper di runtime disponibili per la chiamata](http://msdn.microsoft.com/it-it/4652beaf-77d0-4f37-9687-ca193288c0be)  
 Descrive come regolare il comportamento del marshalling dei tipi in un assembly di interoperabilità e come definire manualmente i tipi COM.  
  
 [Procedura: Eseguire la migrazione di codice gestito da DCOM a WCF](../../../docs/framework/interop/how-to-migrate-managed-code-dcom-to-wcf.md)  
 Descrive come eseguire la migrazione di codice gestito DCOM in WCF per la soluzione più sicura.  
  
## Sezioni correlate  
 [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 Contiene collegamenti per accedere ad altre informazioni sull'inclusione di componenti COM nell'applicazione .NET Framework.  
  
 [Assembly to Type Library Conversion Summary](http://msdn.microsoft.com/it-it/3a37eefb-a76c-4000-9080-7dbbf66a4896)  
 Descrive il processo di conversione eseguito in caso di esportazione da assembly a libreria dei tipi.  
  
 [Type Library to Assembly Conversion Summary](http://msdn.microsoft.com/it-it/bf3f90c5-4770-4ab8-895c-3ba1055cc958)  
 Descrive il processo di conversione eseguito in caso di importazione da libreria dei tipi ad assembly.  
  
 [Interoperating Using Generic Types](http://msdn.microsoft.com/it-it/26b88e03-085b-4b53-94ba-a5a9c709ce58)  
 Descrive le azioni supportate quando si usano tipi generici per l'interoperabilità COM.