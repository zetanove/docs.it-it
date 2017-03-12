---
title: "Procedura: implementare e chiamare un metodo di estensione personalizzato (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "metodi di estensione [C#], implementazione e chiamata"
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: implementare e chiamare un metodo di estensione personalizzato (Guida per programmatori C#)
In questo argomento viene illustrato come implementare per contenere i metodi di estensione per qualsiasi tipo in [libreria di classi .NET Framework.](http://go.microsoft.com/fwlink/?LinkID=217856), o qualsiasi altro tipo. .NET che si desidera estendere.  Il codice client può utilizzare i metodi di estensione aggiungendo un riferimento alla DLL che li contiene e aggiungendo una direttiva [using](../../../csharp/language-reference/keywords/using-directive.md) che specifica lo spazio dei nomi nel quale sono definiti i metodi di estensione.  
  
### Per definire e chiamare il metodo di estensione  
  
1.  Definire una [classe](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md) statica per contenere il metodo di estensione.  
  
     La classe deve essere visibile al codice client.  Per ulteriori informazioni sulle regole di accessibilità, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
2.  Implementare il metodo di estensione come metodo statico con almeno la stessa visibilità della classe che lo contiene.  
  
3.  Il primo parametro del metodo specifica il tipo sul quale opera il metodo. Deve essere preceduto dal modificatore [this](../../../csharp/language-reference/keywords/this.md).  
  
4.  Nel codice che effettua la chiamata, aggiungere una direttiva `using` per specificare lo [spazio dei nomi](../../../csharp/language-reference/keywords/namespace.md) che contiene la classe del metodo di estensione.  
  
5.  Chiamare i metodi come se fossero metodi di istanza sul tipo.  
  
     Si noti che il primo parametro non è specificato dal codice che effettua la chiamata perché rappresenta il tipo sul quale viene applicato l'operatore e il compilatore è già a conoscenza del tipo dell'oggetto.  È necessario fornire solo gli argomenti per i parametri 2 tramite `n`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene implementato un metodo di estensione denominato `WordCount` nella classe `CustomExtensions.StringExtension`.  Il metodo opera sulla classe <xref:System.String>, specificata come primo parametro del metodo.  Lo spazio dei nomi `CustomExtensions` viene importato nello spazio dei nomi dell'applicazione e il metodo viene chiamato all'interno del metodo `Main`.  
  
 [!code-cs[csProgGuideExtensionMethods#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-implement-and-cal_1.cs)]  
  
## Compilazione del codice  
 Per eseguire questo codice, copiarlo e incollarlo in un progetto di applicazione console di Visual C\# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs-current-short-md.md)].  Per impostazione predefinita, questo progetto è destinato alla versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] e contiene un riferimento a System.Core.dll e una direttiva `using` per System.Linq.  Se uno o più di questi requisiti non sono presenti nel progetto, è possibile aggiungerli manualmente.  Per ulteriori informazioni, vedere [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  
  
## Sicurezza di .NET Framework  
 I metodi di estensione non presentano vulnerabilità di sicurezza specifiche.  Non possono mai essere utilizzati per rappresentare metodi esistenti su un tipo, perché tutti i conflitti di nomi vengono risolti a favore del metodo di istanza o statico definito dal tipo stesso.  I metodi di estensione non possono accedere ai dati privati nella classe estesa.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Metodi di estensione](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [this](../../../csharp/language-reference/keywords/this.md)   
 [spazio dei nomi](../../../csharp/language-reference/keywords/namespace.md)