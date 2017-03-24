---
title: "Procedura: Inizializzare un dizionario con un inizializzatore di raccolta (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "inizializzatori di raccolta [C#], con oggetto Dictionary"
ms.assetid: 25283922-f8ee-40dc-a639-fac30804ec71
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# Procedura: Inizializzare un dizionario con un inizializzatore di raccolta (Guida per programmatori C#)
Una raccolta <xref:System.Collections.Generic.Dictionary%602> contiene una raccolta di coppie chiave\/valore.  Il metodo <xref:System.Collections.Generic.Dictionary%602.Add%2A> accetta due parametri, uno per la chiave e uno per il valore.  Per inizializzare un <xref:System.Collections.Generic.Dictionary%602> o qualsiasi raccolta il cui metodo `Add` accetta più parametri, racchiudere tra parentesi ogni set di parametri, come illustrato nell'esempio seguente.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito un <xref:System.Collections.Generic.Dictionary%602> viene inizializzato con istanze di tipo `StudentName`.  
  
 [!code-cs[csProgGuideLINQ#34](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-initialize-a-dictionary-with-a-collection-initializer_1.cs)]  
  
 Si notino le due coppie di parentesi graffe in ogni elemento della raccolta.  Le parentesi graffe più interne racchiudono l'inizializzatore di oggetto per `StudentName`e quelle più esterne racchiudono l'inizializzatore per la coppia chiave\/valore che verrà aggiunta all'oggetto <xref:System.Collections.Generic.Dictionary%602> di `students`.  Viene infine racchiuso tra parentesi graffe l'intero inizializzatore di raccolta per il dizionario.  
  
## Compilazione del codice  
 Per eseguire questo codice, copiare e incollare la classe in un progetto di applicazione console di Visual C\# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)].  Per impostazione predefinita, questo progetto è destinato alla versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e contiene un riferimento a System.Core.dll e una direttiva using per System.Linq.  Se uno o più di questi requisiti non sono presenti nel progetto, è possibile aggiungerli manualmente.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)