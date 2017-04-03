---
title: Introduzione ai generics (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- generics [C#], about generics
ms.assetid: a1ad761e-42f7-41dd-a62f-452a2de26b9d
caps.latest.revision: 32
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f3092eb1e5435bbced565b02d989a57abf2d52e0
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-generics-c-programming-guide"></a>Introduzione ai generics (Guida per programmatori C#)
Le classi e i metodi generici sono riutilizzabili, indipendenti dai tipi e molto più efficaci delle rispettive controparti non generiche. I generics sono in genere usati con le raccolte e i metodi che operano su di essi. La versione 2.0 della libreria di classi .NET Framework offre un nuovo spazio dei nomi, <xref:System.Collections.Generic>, che contiene diverse nuove classi di raccolta generiche. È consigliabile che tutte le applicazioni destinate a [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 2.0 e versioni successive usino le nuove classi di raccolte generiche anziché le controparti non generiche meno recenti, ad esempio <xref:System.Collections.ArrayList>. Per altre informazioni, vedere [Generics nella libreria di classi .NET Framework](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md).  
  
 Naturalmente, è anche possibile creare tipi e metodi generici personalizzati per offrire le proprie soluzioni e schemi progettuali generalizzati che sono indipendenti dai tipi ed efficienti. Nell'esempio di codice riportato di seguito viene illustrata una classe di elenco collegato generica semplice a scopo dimostrativo. Nella maggior parte dei casi, è necessario usare la classe <xref:System.Collections.Generic.List%601> specificata dalla libreria di classi .NET Framework anziché crearne una propria. Il parametro di tipo `T` viene usato in diverse posizioni in cui di norma verrebbe usato un tipo concreto per indicare il tipo dell'elemento archiviato nell'elenco. In particolare, viene usato nei seguenti modi:  
  
-   Come tipo di un parametro del metodo nel metodo `AddHead`.  
  
-   Come tipo restituito del metodo pubblico `GetNext` e della proprietà `Data` nella classe `Node` annidata.  
  
-   Come tipo dei dati del membro privato della classe annidata.  
  
 Si noti che T è disponibile per la classe `Node` annidata. Quando si crea un'istanza di `GenericList<T>` con un tipo concreto, ad esempio `GenericList<int>`, ogni occorrenza di `T` verrà sostituita con `int`.  
  
 [!code-cs[csProgGuideGenerics#2](../../../csharp/programming-guide/generics/codesnippet/CSharp/introduction-to-generics_1.cs)]  
  
 Nell'esempio di codice riportato di seguito viene illustrato come il codice client usa la classe generica `GenericList<T>` per creare un elenco di interi. Cambiando semplicemente l'argomento relativo al tipo, è possibile modificare il codice riportato di seguito per creare elenchi di stringhe o di qualsiasi altro tipo personalizzato:  
  
 [!code-cs[csProgGuideGenerics#3](../../../csharp/programming-guide/generics/codesnippet/CSharp/introduction-to-generics_2.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)
