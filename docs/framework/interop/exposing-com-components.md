---
title: "Exposing COM Components to the .NET Framework | Microsoft Docs"
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
  - "exposing COM components to .NET Framework"
  - "interoperation with unmanaged code, exposing COM components"
  - "COM interop, exposing COM components"
ms.assetid: e78b14f1-e487-43cd-9c6d-1a07483f1730
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Exposing COM Components to the .NET Framework
In questa sezione viene riepilogata la procedura cui attenersi per esporre un componente COM esistente al codice gestito.  Per informazioni dettagliate sulla creazione di server COM strettamente integrati con .NET Framework, vedere [Considerazioni sulla progettazione per l'interoperabilità](http://msdn.microsoft.com/it-it/b59637f6-fe35-40d6-ae72-901e7a707689).  
  
 I componenti COM esistenti possono essere utilizzati con profitto nel codice gestito come applicazioni aziendali di livello intermedio o come funzionalità isolate.  Un componente ideale dispone di un assembly di interoperabilità primario ed è strettamente conforme agli standard di programmazione imposti da COM.  
  
#### Per esporre componenti COM a .NET Framework  
  
1.  [Importare una libreria dei tipi come assembly](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md).  
  
     Common Language Runtime richiede metadati per tutti i tipi, inclusi i tipi COM.  I modi per ottenere un assembly contenente tipi COM importati come metadati sono diversi.  
  
2.  [Creare tipi COM nel codice gestito](http://msdn.microsoft.com/it-it/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66).  
  
     È possibile esaminare i tipi COM, attivare istanze e chiamare i metodi di un oggetto COM così come avviene per qualsiasi tipo gestito.  
  
3.  [Compilare un progetto di interoperabilità](../../../docs/framework/interop/compiling-an-interop-project.md).  
  
     In The [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] sono disponibili compilatori per numerosi linguaggi conformi a Common Language Specification \(CLS\), tra cui [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C\# e C\+\+.  
  
4.  [Distribuzione di un'applicazione di interoperabilità](../../../docs/framework/interop/deploying-an-interop-application.md).  
  
     La soluzione ottimale consiste nel distribuire le applicazioni di interoperabilità come assembly firmati con [nome sicuro](../../../docs/framework/app-domains/strong-named-assemblies.md) nella Global Assembly Cache.  
  
## Vedere anche  
 [Interoperating with Unmanaged Code](../../../docs/framework/interop/index.md)   
 [Design Considerations for Interoperation](http://msdn.microsoft.com/it-it/b59637f6-fe35-40d6-ae72-901e7a707689)   
 [COM Interop Sample: .NET Client and COM Server](../../../docs/framework/interop/com-interop-sample-net-client-and-com-server.md)   
 [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../../docs/standard/language-independence-and-language-independent-components.md)   
 [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)