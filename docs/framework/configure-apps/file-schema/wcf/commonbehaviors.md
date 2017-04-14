---
title: "&lt;comportamentiComuni&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5260aeca-388d-4e82-94c0-124fa8054cf5
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;comportamentiComuni&gt;
La sezione `commonBehaviors` può essere definita solo nel file machine.config.  e definisce due raccolte figlio denominate `endpointBehaviors` e `serviceBehaviors`.  Ogni raccolta definisce elementi di comportamento usati rispettivamente da tutti gli endpoint [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] e dai servizi del computer.  I comportamenti definiti in `endpointBehaviors` vengono applicati solo ai client e i comportamenti definiti in `serviceBehaviors` vengono applicati solo ai servizi.  Se un comportamento viene definito in entrambe le sezioni `commonBehaviors` e `behaviors`, la preferenza viene assegnata a quello nella sezione `behaviors`.