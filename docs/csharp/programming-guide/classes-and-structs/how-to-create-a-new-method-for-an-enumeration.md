---
title: "Procedura: creare un nuovo metodo per una enumerazione (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "enum (estensibilità) [C#]"
  - "enumerazioni [C#]"
  - "metodi di estensione [C#], per enum"
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
caps.latest.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 7
---
# Procedura: creare un nuovo metodo per una enumerazione (Guida per programmatori C#)
È possibile utilizzare i metodi di estensione per aggiungere la funzionalità specifica a un particolare tipo enum.  
  
## Esempio  
 Nell'esempio seguente, l'enumerazione `Grades` rappresenta, il possibile voto che un studente potrebbe prendere in una classe.  Un metodo di estensione denominato `Passing` viene aggiunto al tipo `Grades` in modo che ogni istanza di tale tipo ora "sa" se rappresenta un voto sufficiente oppure no.  
  
 [!code-cs[csProgGuideExtensionMethods#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-create-a-new-meth_1.cs)]  
  
 Si noti che la classe `Extensions` contiene anche una variabile statica aggiornata in modo dinamico e che il valore restituito del metodo di estensione riflette il valore corrente di tale variabile.  Ciò dimostra che, in background, i metodi di estensione vengono richiamati direttamente sulla classe statica nella quale sono definiti.  
  
## Compilazione del codice  
 Per eseguire questo codice, copiarlo e incollarlo in un progetto di applicazione console di Visual C\# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)].  Per impostazione predefinita, questo progetto è destinato alla versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e contiene un riferimento a System.Core.dll e una direttiva `using` per System.Linq.  Se uno o più di questi requisiti non sono presenti nel progetto, è possibile aggiungerli manualmente.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Metodi di estensione](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)