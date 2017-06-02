---
title: "Procedura: definire un ambito del nome | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "animazione, Storyboard, nel codice procedurale:"
  - "ambito del nome, definizione"
  - "Storyboard, animazione nel codice procedurale:"
ms.assetid: 4f361925-6a08-40dc-8231-a61111c6b28b
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: definire un ambito del nome
Per eseguire un’animazione con <xref:System.Windows.Media.Animation.Storyboard> nel codice, è necessario creare <xref:System.Windows.NameScope> e registrare i nomi degli oggetti di destinazione con l’elemento che possiede quell’ambito del nome.  Nell'esempio riportato di seguito viene creato <xref:System.Windows.NameScope> per `myMainPanel`.  Due pulsanti, `button1` e `button2` vengono aggiunti al pannello e i loro nomi vengono registrati.  Vengono create numerose animazioni e <xref:System.Windows.Media.Animation.Storyboard>.  Il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> dello storyboard viene utilizzato per avviare le animazioni.  
  
 Poiché `button1`, `button2` e `myMainPanel` condividono tutti lo stesso ambito del nome, ognuno di questi elementi può essere utilizzato con il metodo <xref:System.Windows.Media.Animation.Storyboard> <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> per avviare le animazioni.  
  
## Esempio  
 [!code-csharp[StoryboardBeginAnimation_procedural_snip#NameScopeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/CSharp/ScopeExample.cs#namescopeexample)]
 [!code-vb[StoryboardBeginAnimation_procedural_snip#NameScopeExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/visualbasic/scopeexample.vb#namescopeexample)]  
  
## Vedere anche  
 [Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)