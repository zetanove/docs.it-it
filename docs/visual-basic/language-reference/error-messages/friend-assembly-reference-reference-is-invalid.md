---
title: "Friend assembly reference &lt;reference&gt; is invalid | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc31535"
  - "bc31535"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31535"
ms.assetid: 6540c1d0-bb19-4051-a579-2e4f9094585e
caps.latest.revision: 5
caps.handback.revision: 5
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Friend assembly reference &lt;reference&gt; is invalid
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il riferimento \<riferimento\> all'assembly Friend non è valido.Gli assembly firmati con nome sicuro devono specificare una chiave pubblica nelle rispettive dichiarazioni InternalsVisibleTo.  
  
 Il nome dell'assembly passato al costruttore dell'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> identifica un assembly con nome sicuro, ma non include un attributo `PublicKey`.  
  
 **ID errore:** BC31535  
  
### Per correggere l'errore  
  
1.  Determinare la chiave pubblica per l'assembly Friend con nome sicuro.  Includere la chiave pubblica nell'ambito del nome dell'assembly passato al costruttore dell'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> utilizzando l'attributo `PublicKey`.  
  
## Vedere anche  
 <xref:System.Reflection.AssemblyName>   
 [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: creare assembly Friend firmati](../Topic/How%20to:%20Create%20Signed%20Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)