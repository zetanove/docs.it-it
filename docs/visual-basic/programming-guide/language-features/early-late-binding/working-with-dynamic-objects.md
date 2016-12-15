---
title: "Working with Dynamic Objects (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "dynamic objects [Visual Basic]"
ms.assetid: bdee2a00-07ff-46f9-86dd-fdac9b99cc97
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Working with Dynamic Objects (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Gli oggetti dinamici forniscono un'altra modalità, diversa dal tipo `Object`, per eseguire un'associazione tardiva a un oggetto in fase di runtime.  Un oggetto dinamico espone membri, quali proprietà e i metodi, in fase di runtime utilizzando interfacce dinamiche che sono definite nello spazio dei nomi <xref:System.Dynamic>.  È possibile utilizzare le classi nello spazio dei nomi <xref:System.Dynamic> per creare oggetti, da utilizzare insieme alle strutture dei dati, che non corrispondono a un formato o un tipo statico.  È inoltre possibile utilizzare gli oggetti dinamici definiti nei linguaggi dinamici quali IronPython e IronRuby.  Per esempi che illustrano come creare oggetti dinamici o utilizzare un oggetto dinamico definito in un linguaggio dinamico, vedere [Procedura dettagliata: creazione e utilizzo di oggetti dinamici](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md), <xref:System.Dynamic.DynamicObject> o <xref:System.Dynamic.ExpandoObject>.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] supporta l'associazione a oggetti dal runtime del linguaggio dinamico e dai linguaggi dinamici quali IronPython and IronRuby tramite l'interfaccia <xref:System.Dynamic.IDynamicMetaObjectProvider>.  Esempi di classi che implementano l'interfaccia `IDynamicMetaObjectProvider` sono le classi <xref:System.Dynamic.DynamicObject> e <xref:System.Dynamic.ExpandoObject>.  
  
 Se viene effettuata una chiamata ad associazione tardiva a un oggetto che implementa l'interfaccia `IDynamicMetaObjectProvider`, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esegue l'associazione all'oggetto dinamico utilizzando tale interfaccia.  Se viene effettuata una chiamata ad associazione tardiva a un oggetto che non implementa l'interfaccia `IDynamicMetaObjectProvider` o se la chiamata all'interfaccia `IDynamicMetaObjectProvider` non riesce, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esegue l'associazione all'oggetto utilizzando le funzionalità dell'associazione tardiva del runtime di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## Vedere anche  
 <xref:System.Dynamic.DynamicObject>   
 <xref:System.Dynamic.ExpandoObject>   
 [Procedura dettagliata: creazione e utilizzo di oggetti dinamici](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)   
 [Early and Late Binding](../../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)