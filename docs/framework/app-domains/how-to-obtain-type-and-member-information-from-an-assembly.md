---
title: "Procedura: reperire informazioni su tipo e membro da un assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], recupero di informazioni"
  - "recupero di informazioni sull'assembly"
ms.assetid: 348ae651-ccda-4f13-8eda-19e8337e9438
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: reperire informazioni su tipo e membro da un assembly
Nello spazio dei nomi <xref:System.Reflection> sono disponibili numerosi metodi per il recupero di informazioni da un assembly.  In questa sezione viene illustrato uno di tali metodi.  Per ulteriori informazioni, vedere [Cenni preliminari sulla reflection](../../../docs/framework/reflection-and-codedom/reflection.md).  
  
 L'esempio seguente consente di ottenere informazioni relative al tipo e al membro da un assembly.  
  
## Esempio  
 [!code-cpp[Conceptual.Types.ViewInfo#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.types.viewinfo/cpp/source6.cpp#8)]
 [!code-csharp[Conceptual.Types.ViewInfo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.types.viewinfo/cs/source6.cs#8)]
 [!code-vb[Conceptual.Types.ViewInfo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.types.viewinfo/vb/source6.vb#8)]  
  
## Vedere anche  
 [Hosting Overview](http://msdn.microsoft.com/it-it/ea527626-99e3-4995-81c4-c8f3e60eb6d5)   
 [Programming with Application Domains](http://msdn.microsoft.com/it-it/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Reflection](../../../docs/framework/reflection-and-codedom/reflection.md)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)