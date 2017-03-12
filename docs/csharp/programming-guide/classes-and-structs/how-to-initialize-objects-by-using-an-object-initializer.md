---
title: "Procedura: inizializzare oggetti utilizzando un inizializzatore di oggetto (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "inizializzatori di oggetto [C#], modalità di utilizzo"
  - "oggetti [C#], inizializzazione"
ms.assetid: 4b75ebb2-2e29-43de-929c-d736a8f27ce6
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Procedura: inizializzare oggetti utilizzando un inizializzatore di oggetto (Guida per programmatori C#)
È possibile utilizzare inizializzatori di oggetto per inizializzare oggetti tipo in modo dichiarativo senza richiamare esplicitamente un costruttore per il tipo.  
  
 Negli esempi seguenti viene illustrato come utilizzare gli inizializzatori di oggetto con gli oggetti denominati.  Il compilatore elabora gli inizializzatori di oggetto accedendo innanzitutto al costruttore di istanza predefinito e quindi elaborando le inizializzazioni dei membri.  Se pertanto il costruttore predefinito è dichiarato come `private` nella classe, gli inizializzatori di oggetto che richiedono l'accesso pubblico avranno esito negativo.  
  
 È necessario utilizzare un inizializzatore di oggetto se si definisce un tipo anonimo.  Per ulteriori informazioni, vedere [Procedura: restituire sottoinsiemi di proprietà degli elementi in una query](../../../csharp/programming-guide/classes-and-structs/how-to-return-subsets-of-element-properties-in-a-query.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come inizializzare un nuovo tipo `StudentName` tramite inizializzatori di oggetto.  
  
 [!code-cs[csProgGuideLINQ#35](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#35)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come inizializzare una raccolta di tipi `StudentName` nuova utilizzando un inizializzatore di raccolta.  Si noti che un inizializzatore di raccolta è una serie di inizializzatori di oggetto delimitati da virgole.  
  
 [!code-cs[csProgGuideLINQ#36](../../../csharp/programming-guide/arrays/codesnippet/csharp/csLINQProgRef/csRef30LangFeatures_2.cs#36)]  
  
## Compilazione del codice  
 Per eseguire questo codice, copiare e incollare la classe in un progetto di applicazione console di Visual C\# creato in [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)