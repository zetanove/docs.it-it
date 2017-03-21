---
title: Utilizzo di oggetti dinamici (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- dynamic objects [Visual Basic]
ms.assetid: bdee2a00-07ff-46f9-86dd-fdac9b99cc97
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 366b563764baaa39849356a782ecee264b2ae94f
ms.lasthandoff: 03/13/2017

---
# <a name="working-with-dynamic-objects-visual-basic"></a>Utilizzo di oggetti dinamici (Visual Basic)
Oggetti dinamici forniscono diverso da un altro modo, il `Object` tipo, l'associazione tardiva a un oggetto in fase di esecuzione. Un oggetto dinamico espone membri, ad esempio proprietà e metodi in fase di esecuzione utilizzando interfacce dinamiche che vengono definite nel <xref:System.Dynamic>dello spazio dei nomi.</xref:System.Dynamic> È possibile utilizzare le classi di <xref:System.Dynamic>dello spazio dei nomi per creare gli oggetti che funzionano con strutture di dati che non corrispondono a un formato o il tipo statico.</xref:System.Dynamic> È inoltre possibile utilizzare gli oggetti dinamici definiti in linguaggi dinamici quali IronPython e IronRuby. Per esempi che illustrano come creare oggetti dinamici o utilizzare un oggetto dinamico definito in un linguaggio dinamico, vedere [procedura dettagliata: creazione e l'uso oggetti dinamici](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md), <xref:System.Dynamic.DynamicObject>, o <xref:System.Dynamic.ExpandoObject>.</xref:System.Dynamic.ExpandoObject> </xref:System.Dynamic.DynamicObject>  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]associazione a oggetti dal runtime di linguaggio dinamico e linguaggi dinamici quali IronPython e IronRuby tramite il <xref:System.Dynamic.IDynamicMetaObjectProvider>interfaccia.</xref:System.Dynamic.IDynamicMetaObjectProvider> Esempi di classi che implementano il `IDynamicMetaObjectProvider` interfaccia sono il <xref:System.Dynamic.DynamicObject>e <xref:System.Dynamic.ExpandoObject>classi.</xref:System.Dynamic.ExpandoObject> </xref:System.Dynamic.DynamicObject>  
  
 Se viene effettuata una chiamata ad associazione tardiva a un oggetto che implementa il `IDynamicMetaObjectProvider` interfaccia [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] associata all'oggetto dinamico utilizzando tale interfaccia. Se viene effettuata una chiamata ad associazione tardiva a un oggetto che implementa il `IDynamicMetaObjectProvider` interfaccia, o se la chiamata al `IDynamicMetaObjectProvider` interfaccia ha esito negativo, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] associata all'oggetto utilizzando le funzionalità di associazione tardiva del [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] runtime.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Dynamic.DynamicObject></xref:System.Dynamic.DynamicObject>   
 <xref:System.Dynamic.ExpandoObject></xref:System.Dynamic.ExpandoObject>   
 [Procedura dettagliata: Creazione e utilizzo di oggetti dinamici](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)   
 [Associazione anticipata e tardiva](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
