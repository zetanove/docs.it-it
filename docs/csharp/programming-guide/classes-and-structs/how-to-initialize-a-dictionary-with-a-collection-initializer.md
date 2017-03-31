---
title: 'Procedura: Inizializzare un dizionario con un inizializzatore di insieme (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- collection initializers [C#], with Dictionary
ms.assetid: 25283922-f8ee-40dc-a639-fac30804ec71
caps.latest.revision: 10
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 60443456be4b4fbb13dad6cb9c372a1af332c2fd
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-initialize-a-dictionary-with-a-collection-initializer-c-programming-guide"></a>Procedura: Inizializzare un dizionario con una inizializzatore di raccolta (Guida per programmatori C#)
Il metodo relativo <xref:System.Collections.Generic.Dictionary`2> contains a collection of key/value pairs. Its <xref:System.Collections.Generic.Dictionary`2.Add*> accetta due parametri, uno per la chiave e uno per il valore. Per inizializzare un <xref:System.Collections.Generic.Dictionary`2>, or any collection whose `Add` o qualsiasi raccolta il cui metodo accetta più parametri, racchiudere tra parentesi ogni set di parametri, come illustrato nell'esempio seguente.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene visualizzato <xref:System.Collections.Generic.Dictionary`2> is initialized with instances of type `StudentName`.  
  
 [!code-cs[csProgGuideLINQ#34](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-initialize-a-dictionary-with-a-collection-initializer_1.cs)]  
  
 Si noti che vi sono due coppie di parentesi graffe in ogni elemento della raccolta. Le parentesi più interne racchiudono l'inizializzatore di oggetto per `StudentName`, quelle più esterne racchiudono l'inizializzatore per la coppia chiave/valore che verrà aggiunta a `students` <xref:System.Collections.Generic.Dictionary`2>. Infine, tutto l'inizializzatore di insieme per il dizionario è racchiuso tra parentesi graffe.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per eseguire questo codice, copiare e incollare la classe in un progetto di applicazione console di Visual C# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)]. Per impostazione predefinita, questo progetto usa la versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], e ha un riferimento a System.Core.dll e una direttiva using per System.Linq. Se uno o più di questi requisiti non è presente nel progetto, è possibile aggiungerlo manualmente.   
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)
