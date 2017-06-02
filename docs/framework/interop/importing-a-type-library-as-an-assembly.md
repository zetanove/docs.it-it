---
title: "Importing a Type Library as an Assembly | Microsoft Docs"
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
  - "importing type library"
  - "type metadata"
  - "custom wrappers"
  - "metadata"
  - "exposing COM components to .NET Framework"
  - "Type Library Importer"
  - "interoperation with unmanaged code, importing type library"
  - "interoperation with unmanaged code, exposing COM components"
  - "type libraries"
  - "TypeLibConverter class, importing type library as assembly"
  - "COM interop, importing type library"
  - "COM interop, exposing COM components"
ms.assetid: d1898229-cd40-426e-a275-f3eb65fbc79f
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Importing a Type Library as an Assembly
Solitamente le definizioni dei tipi COM risiedono in una libreria dei tipi.  I compilatori conformi a CLS, al contrario, producono metadati di tipi in un assembly.  Le due fonti di informazioni sui tipi sono piuttosto diverse.  In questo argomento vengono illustrate le tecniche che permettono di generare metadati da una libreria dei tipi.  L'assembly risultante è detto assembly di interoperabilità e le informazioni sul tipo che contiene consentono alle applicazioni .NET Framework di utilizzare tipi COM.  
  
 Queste informazioni sul tipo possono essere rese disponibili all'applicazione in due modi:  
  
-   Utilizzo di assembly di interoperabilità disponibili solo nella fase di progettazione: a partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] è possibile indicare al compilatore di incorporare nel file eseguibile informazioni sul tipo ottenute dall'assembly di interoperabilità.  Il compilatore incorpora solo le informazioni sul tipo utilizzate dall'applicazione.  Non è necessario distribuire l'assembly di interoperabilità con l'applicazione.  Questa è la tecnica consigliata.  
  
-   Distribuzione di assembly di interoperabilità: è possibile creare un riferimento standard all'assembly di interoperabilità.  In questo caso è necessario distribuire l'assembly di interoperabilità con l'applicazione.  Se si utilizza questa tecnica senza tuttavia utilizzare un componente COM privato, fare sempre riferimento all'assembly di interoperabilità primario \(PIA, Primary Interop Assembly\) pubblicato dall'autore del componente COM che si intende incorporare nel codice gestito.  Per ulteriori informazioni sulla creazione e sull'utilizzo di assembly di interoperabilità primari, vedere [Assembly di interoperabilità primari](http://msdn.microsoft.com/it-it/b977a8be-59a0-40a0-a806-b11ffba5c080).  
  
 Quando si utilizzano assembly di interoperabilità disponibili solo nella fase di progettazione è possibile incorporare informazioni sul tipo dall'assembly di interoperabilità primario pubblicato dall'autore del componente COM.  Tuttavia, non è necessario distribuire l'assembly di interoperabilità primario con l'applicazione.  
  
 L'utilizzo di assembly di interoperabilità disponibili solo nella fase di progettazione riduce la dimensione dell'applicazione, in quanto la maggior parte delle applicazioni non utilizza tutte le funzionalità di un componente COM.  Il compilatore è molto efficiente quando incorpora informazioni sul tipo. Se l'applicazione utilizza solo alcuni dei metodi su un'interfaccia COM, il compilatore non incorpora i metodi inutilizzati.  Quando un'applicazione con informazioni sul tipo incorporate interagisce con un'altra applicazione di tale tipo o con un'applicazione che utilizza un assembly di interoperabilità primario, Common Language Runtime utilizza regole di equivalenza fra tipi per determinare se due tipi con lo stesso nome rappresentano lo stesso tipo COM.  Per utilizzare gli oggetti COM non è necessario conoscere queste regole.  Tuttavia, se si desidera ottenere maggiori informazioni sulle regole, vedere [Type Equivalence and Embedded Interop Types](../../../docs/framework/interop/type-equivalence-and-embedded-interop-types.md).  
  
## Generazione di metadati  
 Le librerie dei tipi COM possono essere file autonomi con estensione .tlb, ad esempio Loanlib.tlb.  Alcune librerie dei tipi sono incorporate nella sezione delle risorse di un file con estensione .dll o .exe.  Altre fonti di informazioni sulle librerie dei tipi sono i file con estensione .olb e .ocx.  
  
 Una volta individuata la libreria dei tipi contenente l'implementazione del tipo COM desiderato, saranno disponibili le opzioni seguenti per generare un assembly di interoperabilità contenente i metadati del tipo:  
  
-   Visual Studio  
  
     Visual Studio converte automaticamente i tipi COM di una libreria dei tipi in metadati di un assembly.  Per istruzioni, vedere [Procedura: aggiungere riferimenti alle librerie dei tipi](../../../docs/framework/interop/how-to-add-references-to-type-libraries.md) e [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office](../Topic/Walkthrough:%20Embedding%20Type%20Information%20from%20Microsoft%20Office%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
-   [Utilità di importazione della libreria dei tipi \(Tlbimp.exe\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)  
  
     L'utilità di importazione della libreria dei tipi utilizza le opzioni della riga di comando per modificare i metadati nel file di interoperabilità, importa tipi da una libreria dei tipi esistente e genera un assembly di interoperabilità e uno spazio dei nomi.  Per istruzioni, vedere [Procedura: generare assembly di interoperabilità da librerie dei tipi](../../../docs/framework/interop/how-to-generate-interop-assemblies-from-type-libraries.md).  
  
-   Classe <xref:System.Runtime.InteropServices.TypeLibConverter?displayProperty=fullName>  
  
     Questa classe fornisce metodi per la conversione delle coclassi e delle interfacce di una libreria dei tipi in metadati di un assembly.  Produce lo stesso output di metadati prodotto da Tlbimp.exe.  Tuttavia, a differenza di Tlbimp.exe, la classe <xref:System.Runtime.InteropServices.TypeLibConverter> può convertire una libreria dei tipi in memoria nei metadati.  
  
-   Wrapper personalizzati  
  
     Quando una libreria dei tipi non è disponibile o non è corretta, è possibile creare un duplicato della definizione della classe o dell'interfaccia nel codice sorgente gestito.  In seguito si compila il codice sorgente con un compilatore che si avvale del runtime per produrre metadati in un assembly.  
  
     Per definire manualmente i tipi COM, è necessario avere accesso agli elementi elencati di seguito:  
  
    -   Esatte descrizioni delle coclassi e delle interfacce che si desidera definire.  
  
    -   Un compilatore, come quello di C\#, che possa generare le definizioni di classe appropriate per .NET Framework.  
  
    -   Conoscenza delle regole per la conversione di una libreria dei tipi in assembly.  
  
     La scrittura di un wrapper personalizzato è una tecnica avanzata.  Per ulteriori informazioni su come generare un wrapper personalizzato, vedere [Personalizzazione di wrapper standard](http://msdn.microsoft.com/it-it/c40d089b-6a3c-41b5-a20d-d760c215e49d).  
  
 Per ulteriori informazioni sul processo di importazione per l'interoperabilità COM, vedere [Riepilogo della conversione da libreria dei tipi ad assembly](http://msdn.microsoft.com/it-it/bf3f90c5-4770-4ab8-895c-3ba1055cc958).  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.TypeLibConverter>   
 [Exposing COM Components to the .NET Framework](../../../docs/framework/interop/exposing-com-components.md)   
 [Type Library to Assembly Conversion Summary](http://msdn.microsoft.com/it-it/bf3f90c5-4770-4ab8-895c-3ba1055cc958)   
 [Tlbimp.exe \(Type Library Importer\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)   
 [Customizing Standard Wrappers](http://msdn.microsoft.com/it-it/c40d089b-6a3c-41b5-a20d-d760c215e49d)   
 [Using COM Types in Managed Code](http://msdn.microsoft.com/it-it/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66)   
 [Compiling an Interop Project](../../../docs/framework/interop/compiling-an-interop-project.md)   
 [Deploying an Interop Application](../../../docs/framework/interop/deploying-an-interop-application.md)   
 [How to: Add References to Type Libraries](../../../docs/framework/interop/how-to-add-references-to-type-libraries.md)   
 [How to: Generate Interop Assemblies from Type Libraries](../../../docs/framework/interop/how-to-generate-interop-assemblies-from-type-libraries.md)   
 [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office](../Topic/Walkthrough:%20Embedding%20Type%20Information%20from%20Microsoft%20Office%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)