---
title: "Indicizzatori (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "cs.indexers"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, indicizzatori"
  - "indicizzatori [C#]"
ms.assetid: 022cd27d-d5e0-4cfe-8b97-dc018cc3355d
caps.latest.revision: 29
caps.handback.revision: 29
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Indicizzatori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli indicizzatori consentono di indicizzare le istanze di una classe o struct esattamente come le matrici.  Gli indicizzatori sono analoghi alle [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md), con la differenza che le funzioni di accesso accettano i parametri.  
  
 Nel seguente esempio, viene definita una classe generica a cui vengono forniti i metodi delle funzioni di accesso [get](../../../csharp/language-reference/keywords/get.md) e [set](../../../csharp/language-reference/keywords/set.md) semplici come mezzo per assegnare e recuperare i valori.  La classe `Program` crea un'istanza di questa classe per archiviare le stringhe.  
  
 [!code-cs[csProgGuideIndexers#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/index_1.cs)]  
  
> [!NOTE]
>  Per altri esempi, vedere [Sezioni correlate](../../../csharp/programming-guide/indexers/index.md#BKMK_RelatedSections).  
  
## Definizioni di espressioni corpo  
 È normale che alcuni indicizzatori si limitino a restituire immediatamente il risultato di un'espressione.  Esiste una sintassi breve per definire questi indicizzatori usando `=>`:  
  
```c#  
public Customer this[long id] => store.LookupCustomer(id);  
  
```  
  
 L'indicizzatore deve essere di sola lettura e non è necessario usare la parola chiave della funzione di accesso `get`.  
  
## Panoramica sugli indicizzatori  
  
-   Gli indicizzatori consentono di indicizzare gli oggetti in modo simile alle matrici.  
  
-   Una funzione di accesso `get` restituisce un valore.  Una funzione di accesso `set` assegna un valore.  
  
-   La parola chiave [this](../../../csharp/language-reference/keywords/this.md) viene usata per definire gli indicizzatori.  
  
-   La parola chiave [value](../../../csharp/language-reference/keywords/value.md) viene usata per definire il valore che deve essere assegnato dall'indicizzatore `set`.  
  
-   Non è necessario che gli indicizzatori vengano indicizzati da un valore Integer, perché la definizione del meccanismo di ricerca specifico dipende dall'utente.  
  
-   Gli indicizzatori possono essere sottoposti a overload.  
  
-   Gli indicizzatori possono avere più di un parametro formale, ad esempio quando si accede a una matrice bidimensionale.  
  
##  <a name="BKMK_RelatedSections"></a> Sezioni correlate  
  
-   [Utilizzo degli indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)  
  
-   [Indicizzatori nelle interfacce](../../../csharp/programming-guide/indexers/indexers-in-interfaces.md)  
  
-   [Confronto tra proprietà e indicizzatori](../../../csharp/programming-guide/indexers/comparison-between-properties-and-indexers.md)  
  
-   [Limitazione dell'accessibilità delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)