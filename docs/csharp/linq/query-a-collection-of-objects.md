---
title: Eseguire query in una raccolta di oggetti
description: Come eseguire una query nelle raccolte.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 11/30/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 87a76f8a-0b58-4791-90ea-2fe0a30416c9
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6694d28355b638c1fe55df0b44700f2dd8d839de
ms.lasthandoff: 03/13/2017

---
# <a name="query-a-collection-of-objects"></a>Eseguire query in una raccolta di oggetti
In questo esempio viene illustrato come eseguire una query semplice su un elenco di oggetti `Student`. Ogni oggetto `Student` contiene informazioni di base sullo studente e un elenco che rappresenta i voti dello studente in quattro esami.  
  
 Questa applicazione viene usata come framework per molti altri esempi di questa sezione che usano la stessa origine dati `students`.  
  
## <a name="example"></a>Esempio  
 La query seguente restituisce gli studenti che hanno ricevuto un punteggio pari o superiore a 90 nel primo esame.  
  
 [!code-cs[csProgGuideLINQ#15](../../../samples/snippets/csharp/concepts/linq/how-to-query-a-collection-of-objects_1.cs)]  
  
 Questa query è volutamente semplice per consentire la sperimentazione. Ad esempio, è possibile provare altre condizioni nella clausola `where` oppure usare una clausola `orderby` per ordinare i risultati.  
  

## <a name="see-also"></a>Vedere anche  
 [Espressioni di query LINQ](index.md)
