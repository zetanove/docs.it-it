---
title: "Emitting Dynamic Methods and Assemblies | Microsoft Docs"
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
  - "reflection emit"
  - "dynamic assemblies"
  - "metadata, emit interfaces"
  - "reflection emit, overview"
  - "assemblies [.NET Framework], emitting dynamic assemblies"
ms.assetid: 8e8e2631-62fd-40e7-a8ee-0039b06749bc
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Emitting Dynamic Methods and Assemblies
Questa sezione descrive un insieme di tipi gestiti dello spazio dei nomi <xref:System.Reflection.Emit> che consentono la creazione di metadati e codice MSIL \(Microsoft Intermediate Language\) da parte di compilatori o strumenti in fase di esecuzione ed eventualmente la generazione su disco di un file eseguibile portabile \(PE, Portable Executable\).  Questo spazio dei nomi viene usato principalmente da moduli di gestione di script e compilatori.  In questa sezione si farà riferimento alle funzionalità fornite dallo spazio dei nomi <xref:System.Reflection.Emit> con l'espressione reflection emit \(creazione tramite la reflection\).  
  
 La reflection emit offre le funzionalità seguenti:  
  
-   Definizione di metodi globali di tipo lightweight in fase di esecuzione mediante la classe <xref:System.Reflection.Emit.DynamicMethod> ed esecuzione di tali metodi mediante delegati.  
  
-   Definizione di assembly in fase di esecuzione, quindi esecuzione e\/o salvataggio di tali assembly su disco.  
  
-   Definizione di assembly in fase di esecuzione, quindi esecuzione e scaricamento per consentire al processo di Garbage Collection di recuperare le risorse.  
  
-   Definizione di moduli in nuovi assembly in fase di esecuzione, quindi esecuzione e\/o salvataggio di tali assembly su disco.  
  
-   Definizione di tipi in moduli in fase di esecuzione, creazione di istanze di tali tipi e chiamate ai relativi metodi.  
  
-   Definizione di informazioni relative ai simboli per i moduli definiti, che possono essere usate da strumenti quali debugger e analizzatori di codice.  
  
 Oltre ai tipi gestiti dello spazio dei nomi <xref:System.Reflection.Emit>, sono disponibili interfacce di metadati non gestite, descritte nella documentazione di riferimento [Interfacce di metadati](../../../ocs/framework/unmanaged-api/metadata/metadata-interfaces.md).  La reflection emit gestita garantisce un controllo degli errori semantici più completo e un livello di astrazione dei metadati più alto rispetto alle interfacce di metadati non gestite.  
  
 Un'altra risorsa per l'uso di metadati e codice MSIL è la documentazione CLI \(Common Language Infrastructure\), in particolare la seconda e la terza parte, relative rispettivamente alla semantica e alla definizione dei metadati e all'insieme di istruzioni.  La documentazione è disponibile online sul sito Web [MSDN](http://go.microsoft.com/fwlink/?LinkID=65555) e sul sito Web [Ecma](http://go.microsoft.com/fwlink/?LinkId=116487).  
  
## In questa sezione  
 [Security Issues in Reflection Emit](../../../docs/framework/reflection-and-codedom/security-issues-in-reflection-emit.md)  
 Descrive i problemi di sicurezza relativi alla creazione di assembly dinamici mediante la reflection emit.  
  
## Riferimenti  
 <xref:System.Reflection.Emit.OpCodes>  
 Cataloga i codici di istruzioni MSIL che è possibile usare per compilare i corpi dei metodi.  
  
 <xref:System.Reflection.Emit>  
 Contiene le classi gestite usate per creare metodi, assembly e tipi dinamici.  
  
 <xref:System.Type>  
 Illustra la classe <xref:System.Type>, che rappresenta i tipi nella reflection gestita e nella reflection emit, e descrive i concetti fondamentali relativi all'uso di queste tecnologie.  
  
 <xref:System.Reflection>  
 Contiene le classi gestite usate per esaminare i metadati e il codice gestito.  
  
## Sezioni correlate  
 [Reflection](../../../docs/framework/reflection-and-codedom/reflection.md)  
 Illustra come esaminare i metadati e il codice gestito.  
  
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)  
 Fornisce una panoramica degli assembly in .NET Framework.