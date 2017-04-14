---
title: "Compilazione di app con .NET Native | Microsoft Docs"
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
  - "Codice nativo e .NET"
  - ".NET Native"
  - "Compilazione nativa e C#"
  - "compilazione con .NET Native"
  - "compilazione nativa"
ms.assetid: 47cd5648-9469-4b1d-804c-43cc04384045
caps.latest.revision: 27
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 27
---
# Compilazione di app con .NET Native
[!INCLUDE[net_native](../../../includes/net-native-md.md)] è una tecnologia di precompilazione per la creazione e la distribuzione di applicazioni Windows, inclusa con [!INCLUDE[vs_dev14](../../../includes/vs-dev14-md.md)], che compila automaticamente la versione finale delle app scritte in codice gestito \(C\# o Visual Basic\) e destina .NET Framework e Windows 10 al codice nativo.  
  
 In genere, le applicazioni che usano .NET Framework vengono compilate in Microsoft Intermediate Language \(IL\). In fase di esecuzione, il compilatore just\-in\-time \(JIT\) traduce IL in codice nativo. Al contrario, [!INCLUDE[net_native](../../../includes/net-native-md.md)] consente di compilare applicazioni Windows direttamente in codice nativo. Per gli sviluppatori, questo significa che:  
  
-   Le applicazioni forniranno le prestazioni superiori del codice nativo.  
  
-   È possibile continuare a programmare in c\# o Visual Basic.  
  
-   È possibile continuare a sfruttare le risorse fornite da .NET Framework, tra cui la libreria di classi, gestione della memoria e Garbage Collection automatiche e la gestione delle eccezioni.  
  
 Per gli utenti delle applicazioni, [!INCLUDE[net_native](../../../includes/net-native-md.md)] offre i seguenti vantaggi:  
  
-   Tempi di esecuzione veloce  
  
-   Tempi di avvio veloce in modo coerente  
  
-   Bassi costi di distribuzione e aggiornamento  
  
-   Uso ottimizzato della memoria app  
  
 Ma [!INCLUDE[net_native](../../../includes/net-native-md.md)] prevede molto più di una semplice compilazione in codice nativo: trasforma il modo in cui le applicazioni di .NET Framework vengono compilate ed eseguite. In particolare:  
  
-   Durante la precompilazione, le parti necessarie di .NET Framework vengono collegate staticamente nell'applicazione. Ciò consente di eseguire l'applicazione con le librerie app\-local di .NET Framework e di effettuare l'analisi globale per offrire prestazioni ottimali del compilatore. Di conseguenza, l'avvio delle applicazioni sarà più rapido e coerente dopo l'aggiornamento di .NET Framework.  
  
-   Il runtime [!INCLUDE[net_native](../../../includes/net-native-md.md)] viene ottimizzato per la precompilazione statica e quindi può offrire prestazioni superiori. Allo stesso tempo, mantiene le funzionalità di reflection di base che gli sviluppatori troveranno estremamente produttive.  
  
-   [!INCLUDE[net_native](../../../includes/net-native-md.md)] usa lo stesso back\-end del compilatore C\+\+, che è ottimizzato per scenari di precompilazione statici.  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] può offrire i vantaggi delle prestazioni di C\+\+ agli sviluppatori di codice gestito perché usa strumenti identici o simili come C\+\+ dietro le quinte, come illustrato in questa tabella.  
  
||[!INCLUDE[net_native](../../../includes/net-native-md.md)]|C\+\+|  
|-|----------------------------------------------------------------|-----------|  
|Librerie|.NET Framework \+ Windows Runtime|Win32 \+ Windows Runtime|  
|Compilatore|Compilatore di ottimizzazione UTC|Compilatore di ottimizzazione UTC|  
|Distribuito|File binari Ready to run|File binari Ready to run \(ASM\)|  
|Runtime|MRT.dll \(Runtime CLR minimo\)|CRT.dll \(C Runtime\)|  
  
 Per le app Windows per Windows 10, caricare i file binari per la compilazione con .NET Native in pacchetti di applicazioni \(file APPX\) in Windows Store.  
  
## In questa sezione  
 Per altre informazioni sullo sviluppo di applicazioni con la compilazione con .NET Native, vedere i seguenti argomenti:  
  
-   [Introduzione alla compilazione con .NET Native: procedura dettagliata dell'esperienza di sviluppatore](../../../docs/framework/net-native/getting-started-with-net-native.md)  
  
-   [Compilazione e .NET Native:](../../../docs/framework/net-native/net-native-and-compilation.md) compilazione di un progetto in codice nativo con .NET Native.  
  
-   [Reflection e .NET Native](../../../docs/framework/net-native/reflection-and-net-native.md)  
  
    -   [API basate sulla reflection](../../../docs/framework/net-native/apis-that-rely-on-reflection.md)  
  
    -   [Riferimento all'API Reflection](../../../docs/framework/net-native/net-native-reflection-api-reference.md)  
  
    -   [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)  
  
-   [Serializzazione e metadati](../../../docs/framework/net-native/serialization-and-metadata.md)  
  
-   [Migrazione dell'app di Windows Store a .NET Native](../../../docs/framework/net-native/migrating-your-windows-store-app-to-net-native.md)  
  
-   [Risoluzione dei problemi generale per .NET Native](../../../docs/framework/net-native/net-native-general-troubleshooting.md)  
  
## Vedere anche  
 [Domande frequenti .NET Native](http://msdn.microsoft.com/vstudio/dn642499.aspx)