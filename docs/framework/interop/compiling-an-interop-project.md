---
title: "Compiling an Interop Project | Microsoft Docs"
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
  - "interoperation with unmanaged code, compiling"
  - "COM interop, compiling"
  - "exposing COM components to .NET Framework"
  - "compiling interop projects"
  - "interoperation with unmanaged code, exposing COM components"
  - "COM interop, exposing COM components"
ms.assetid: 6fcf6588-5e25-41af-b4ae-780974f2c3df
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Compiling an Interop Project
I progetti di interoperabilità COM che fanno riferimento a uno o più assembly contenenti tipi COM importati vengono compilati come qualunque altro progetto gestito.  È possibile fare riferimento agli assembly di interoperabilità in un ambiente di sviluppo quale Visual Studio, oppure quando si utilizza un compilatore da riga di comando.  In entrambi i casi, affinché la compilazione sia corretta, l'assembly di interoperabilità deve trovarsi nella stessa directory degli altri file di progetto.  
  
 Esistono due modi per fare riferimento agli assembly di interoperabilità:  
  
-   Tipi di interoperabilità incorporati: a partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] e [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)], è possibile indicare al compilatore di incorporare nell'eseguibile informazioni sul tipo ottenute da un assembly di interoperabilità.  Questa è la tecnica consigliata.  
  
-   Distribuzione di assembly di interoperabilità: è possibile creare un riferimento standard a un assembly di interoperabilità.  In questo caso è necessario distribuire l'assembly di interoperabilità con l'applicazione.  
  
 Le differenze tra queste due tecniche sono discusse più dettagliatamente in [Using COM Types in Managed Code](http://msdn.microsoft.com/it-it/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66).  
  
 L'incorporamento dei tipi di interoperabilità con Visual Studio è illustrato in [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office](../Topic/Walkthrough:%20Embedding%20Type%20Information%20from%20Microsoft%20Office%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md) e [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Per fare riferimento a un assembly di interoperabilità con un compilatore da riga di comando e incorporare le informazioni sul tipo negli eseguibili, utilizzare l'opzione del compilatore [\/link \(Link to COM Assembly\)](../Topic/-link%20\(C%23%20Compiler%20Options\).md) o [\/link](../Topic/-link%20\(Visual%20Basic\).md) e specificare il nome dell'assembly.  
  
> [!NOTE]
>  Le applicazioni Visual C\+\+ non possono incorporare informazioni sul tipo, ma possono interagire con applicazioni o componenti aggiuntivi in grado di farlo.  
  
 Per compilare un'applicazione che includa un assembly di interoperabilità primario quando viene distribuita, utilizzare l'opzione del compilatore **\/reference** e specificare il nome dell'assembly.  
  
## Vedere anche  
 [Exposing COM Components to the .NET Framework](../../../docs/framework/interop/exposing-com-components.md)   
 [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../../docs/standard/language-independence-and-language-independent-components.md)   
 [Using COM Types in Managed Code](http://msdn.microsoft.com/it-it/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66)   
 [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office](../Topic/Walkthrough:%20Embedding%20Type%20Information%20from%20Microsoft%20Office%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Importing a Type Library as an Assembly](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)