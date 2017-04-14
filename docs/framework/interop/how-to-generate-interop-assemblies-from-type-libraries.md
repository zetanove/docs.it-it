---
title: "How to: Generate Interop Assemblies from Type Libraries | Microsoft Docs"
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
  - "interop assemblies, generating"
  - "Type Library Importer"
  - "type libraries"
  - "COM interop, importing type library"
ms.assetid: 4afd40c3-68f2-41c5-8ec1-4951bc148b9c
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# How to: Generate Interop Assemblies from Type Libraries
L'[utilità di importazione della libreria dei tipi \(Tlbimp.exe\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) è uno strumento della riga di comando che converte in metadati le coclassi e le interfacce contenute in una libreria dei tipi COM.  Tale strumento crea automaticamente un assembly di interoperabilità e uno spazio dei nomi per le informazioni sui tipi.  Una volta resi disponibili i metadati di una classe, i client gestiti potranno creare istanze dei tipi COM e chiamare i relativi metodi, esattamente come se si trattasse di un'istanza .NET.  Tlbimp.exe converte in blocco un'intera libreria dei tipi e non può generare metadati per un sottoinsieme dei tipi definiti in una libreria.  
  
### Per generare un assembly di interoperabilità da una libreria dei tipi  
  
1.  Utilizzare il comando riportato di seguito:  
  
     **tlbimp** *file della libreria dei tipi*\>  
  
     L'aggiunta dell'opzione **\/out:** consente di produrre un assembly di interoperabilità dal nome modificato, come LOANLib.dll.  La modifica del nome consente di distinguere l'assembly di interoperabilità dalla DLL COM originale ed evita i problemi che possono derivare dalla presenza di nomi duplicati.  
  
## Esempio  
 Il comando che segue produce l'assembly Loanlib.dll nello spazio dei nomi `Loanlib`.  
  
```  
tlbimp Loanlib.dll  
```  
  
 Il comando che segue produce un assembly di interoperabilità dal nome modificato \(LOANLib.dll\).  
  
```  
tlbimp LoanLib.dll /out: LOANLib.dll  
```  
  
## Vedere anche  
 [Importing a Type Library as an Assembly](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)   
 [Exposing COM Components to the .NET Framework](../../../docs/framework/interop/exposing-com-components.md)