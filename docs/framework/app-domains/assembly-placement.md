---
title: "Ubicazione degli assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "<codeBase> (elemento)"
  - "assembly [.NET Framework], posizione"
  - "assembly [.NET Framework], posizionamento"
  - "individuazione di assembly"
ms.assetid: ff8d48bc-f606-484f-9fe1-d0af264269fb
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Ubicazione degli assembly
Per la maggior parte delle applicazioni .NET Framework, gli assembly che costituiscono un'applicazione si trovano nella directory dell'applicazione stessa, in una sottodirectory della directory dell'applicazione o nella Global Assembly Cache \(nel caso in cui l'assembly sia condiviso\).  È possibile eseguire l'override del percorso utilizzato da Common Language Runtime per cercare un assembly utilizzando l'elemento [Elemento \<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) in un file di configurazione.  Se l'assembly non ha un nome sicuro, il percorso specificato tramite l'elemento [Elemento \<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) sarà limitato alla directory o a una sottodirectory dell'applicazione.  Se l'assembly ha un nome sicuro, [Elemento \<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) può specificare qualsiasi percorso del computer o di rete.  
  
 Regole simili vengono adottate per l'individuazione degli assembly quando si utilizza codice non gestito o applicazioni di interoperabilità COM: se l'assembly verrà condiviso da più applicazioni, è opportuno installarlo nella Global Assembly Cache.  Gli assembly utilizzati con codice non gestito devono essere esportati come librerie di tipi e registrati.  Gli assembly utilizzati dall'interoperabilità COM devono essere registrati nel catalogo. Tale registrazione viene talvolta compiuta automaticamente.  
  
## Vedere anche  
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Configurazione di app](../../../docs/framework/configure-apps/index.md)   
 [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)