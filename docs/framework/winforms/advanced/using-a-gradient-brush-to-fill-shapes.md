---
title: "Utilizzo di un pennello a sfumatura per il riempimento di forme | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "pennelli, pennelli per sfumature"
  - "esempi [Windows Form], pennelli per sfumature"
  - "pennelli per sfumature"
ms.assetid: 2c6037b9-05bd-44c0-a22a-19584b722524
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Utilizzo di un pennello a sfumatura per il riempimento di forme
È possibile utilizzare un pennello a sfumatura per riempire una forma con un colore che si modifica gradualmente.  È possibile ad esempio utilizzare una sfumatura orizzontale per riempire una forma con colori che si modificano gradualmente passando dal margine sinistro della forma al margine destro.  Si pensi a un rettangolo che sia di colore nero al margine sinistro e di colore rosso al margine destro, ovvero avente componenti rosso, verde e blu pari a 0, 0, 0 in corrispondenza del margine sinistro e 255, 0, 0 in corrispondenza di quello destro.  Se il rettangolo è largo 256 il componente rosso di un dato pixel sarà maggiore del componente rosso del pixel a sinistra del primo.  Il pixel più a sinistra in una riga ha componenti cromatiche \(0, 0, 0\), il secondo \(1, 0, 0\), il terzo \(2, 0, 0\) e così via, fino al pixel più a destra, che ha componenti cromatiche \(255, 0, 0\).  Questi valori di colore interpolati formano la sfumatura di colore.  
  
 Il colore di una sfumatura lineare cambia spostandosi in orizzontale, in verticale o in parallelo lungo una linea inclinata specificata.  Il colore di una sfumatura percorso cambia spostandosi verso l'interno e i limiti di un percorso.  È possibile personalizzare le sfumature percorso per ottenere una notevole varietà di effetti.  
  
 Nell'illustrazione che segue si mostra un rettangolo riempito con un pennello a sfumatura lineare e un'ellisse riempita con un pennello a sfumatura a percorso.  
  
 ![Sfumatura](../../../../docs/framework/winforms/advanced/media/gradient2.png "gradient2")  
  
## In questa sezione  
 [Procedura: creare una sfumatura lineare](../../../../docs/framework/winforms/advanced/how-to-create-a-linear-gradient.md)  
 Mostra come creare una sfumatura lineare utilizzando la classe <xref:System.Drawing.Drawing2D.LinearGradientBrush>.  
  
 [Procedura: creare una sfumatura percorso](../../../../docs/framework/winforms/advanced/how-to-create-a-path-gradient.md)  
 Descrive come creare una sfumatura a percorso utilizzando la classe <xref:System.Drawing.Drawing2D.PathGradientBrush>.  
  
 [Procedura: applicare la correzione gamma a una sfumatura](../../../../docs/framework/winforms/advanced/how-to-apply-gamma-correction-to-a-gradient.md)  
 Illustra come utilizzare la correzione di gamma con un pennello a sfumatura.  
  
## Riferimenti  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=fullName>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.  
  
 <xref:System.Drawing.Drawing2D.PathGradientBrush?displayProperty=fullName>  
 Descrive la classe e contiene i collegamenti a tutti i relativi membri.