---
title: "Procedura: Creare un dominio dell&#39;applicazione | Microsoft Docs"
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
  - "domini dell'applicazione, creazione"
ms.assetid: ba1fa43e-49f5-47d9-bd7f-3024af16f4ba
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: Creare un dominio dell&#39;applicazione
I domini applicazione vengono automaticamente creati dagli host di Common Language Runtime quando necessario.  È tuttavia possibile creare i propri domini applicazione e caricarvi gli assembly che si desidera gestire personalmente.  È inoltre possibile creare domini applicazione da cui eseguire codice.  
  
 Per creare un nuovo dominio dell'applicazione, utilizzare uno dei metodi di overload **CreateDomain** della classe <xref:System.AppDomain?displayProperty=fullName>.  È possibile assegnare un nome al dominio applicazione e fare riferimento al dominio applicazione utilizzando tale nome.  
  
 L'esempio seguente consente di creare un nuovo dominio applicazione, di assegnare il nome `MyDomain` a tale dominio e infine di stampare il nome del dominio host e del dominio applicazione figlio appena creato sulla console.  
  
## Esempio  
 [!code-cpp[ADCreateDomain#2](../../../samples/snippets/cpp/VS_Snippets_CLR/ADCreateDomain/CPP/source2.cpp#2)]
 [!code-csharp[ADCreateDomain#2](../../../samples/snippets/csharp/VS_Snippets_CLR/ADCreateDomain/CS/source2.cs#2)]
 [!code-vb[ADCreateDomain#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/ADCreateDomain/VB/source2.vb#2)]  
  
## Vedere anche  
 [Hosting Overview](http://msdn.microsoft.com/it-it/ea527626-99e3-4995-81c4-c8f3e60eb6d5)   
 [Programming with Application Domains](http://msdn.microsoft.com/it-it/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)