---
title: "Introduzione ai generics (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "generics [C#], informazioni sui tipi generici"
ms.assetid: a1ad761e-42f7-41dd-a62f-452a2de26b9d
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# Introduzione ai generics (Guida per programmatori C#)
Le classi e i metodi generici sono riutilizzabili, indipendenti dai tipi e molto più efficaci rispetto alle rispettive controparti non generiche.  I generics sono in genere utilizzati con le raccolte e con i metodi che operano su di essi.  La versione 2.0 della libreria di classi di .NET Framework fornisce un nuovo spazio dei nomi, <xref:System.Collections.Generic>, che contiene numerose nuove classi di raccolte generiche.  In tutte le applicazioni destinate a [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 2.0 e versioni successive è consigliabile utilizzare le nuove classi di raccolte generiche anziché le controparti non generiche meno recenti, quale <xref:System.Collections.ArrayList>.  Per ulteriori informazioni, vedere [Generics nella libreria di classi .NET Framework](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md).  
  
 È naturalmente anche possibile creare tipi e metodi generici personalizzati per creare soluzioni e schemi di progettazione generalizzati efficaci e indipendenti dai tipi.  Nell'esempio di codice riportato di seguito viene illustrata una classe di elenco collegato generica semplice a scopo dimostrativo.  Nella maggior parte dei casi, è necessario utilizzare la classe <xref:System.Collections.Generic.List%601> fornita dalla libreria di classi .NET Framework anziché crearne una propria. Il parametro di tipo `T` viene utilizzato in diverse posizioni in cui di norma verrebbe utilizzato un tipo concreto per indicare il tipo dell'elemento archiviato nell'elenco.  In particolare, viene utilizzato nei seguenti modi:  
  
-   Come tipo di un parametro di metodo nel metodo `AddHead`.  
  
-   Come tipo restituito del metodo pubblico `GetNext` e della proprietà `Data` nella classe `Node` annidata.  
  
-   Come tipo dei dati del membro privato nella classe annidata.  
  
 Si noti che T è disponibile per la classe `Node` annidata.  Quando si crea un'istanza di `GenericList<T>` con un tipo concreto, ad esempio `GenericList<int>`, ogni occorrenza di `T` verrà sostituita con `int`.  
  
 [!code-cs[csProgGuideGenerics#2](../../../csharp/programming-guide/generics/codesnippet/csharp/introduction-to-generics_1.cs)]  
  
 Nell'esempio di codice riportato di seguito viene illustrato l'utilizzo della classe generica `GenericList<T>` per creare un elenco di valori interi.  Cambiando semplicemente l'argomento relativo al tipo, è possibile modificare il codice riportato di seguito per creare elenchi di stringhe o di qualsiasi altro tipo personalizzato:  
  
 [!code-cs[csProgGuideGenerics#3](../../../csharp/programming-guide/generics/codesnippet/csharp/introduction-to-generics_2.cs)]  
  
## Vedere anche  
 <xref:System.Collections.Generic>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Generics](../../../csharp/programming-guide/generics/index.md)