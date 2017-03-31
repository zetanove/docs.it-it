---
title: Creare un gruppo annidato
description: Come creare un gruppo annidato.
keywords: .NET, .NET Core, C#
author: stevehoag
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e9f00708-362e-4d13-98c5-d77549347ba0
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ff2c0c00ab23346cbaa3ba7c36a0cba25e03b89b
ms.lasthandoff: 03/13/2017

---
# <a name="create-a-nested-group"></a>Creare un gruppo annidato

Nell'esempio seguente viene illustrato come creare gruppi annidati in un'espressione di query LINQ. Ogni gruppo creato in base all'anno o al livello degli studenti viene ulteriormente suddiviso in gruppi in base ai nomi delle persone.  
  
## <a name="example"></a>Esempio

 > [!NOTE]
 > Questo esempio contiene riferimenti a oggetti definiti nel codice di esempio in [Eseguire una query su una raccolta di oggetti](query-a-collection-of-objects.md). 

 [!code-cs[csProgGuideLINQ#24](../../../samples/snippets/csharp/concepts/linq/how-to-create-a-nested-group_1.cs)]  
  
 Si noti che sono necessari tre cicli `foreach` annidati per eseguire l'iterazione degli elementi interni di un gruppo annidato.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni di query LINQ](index.md)
