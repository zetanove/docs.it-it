---
title: "Procedura: dichiarare e usare propriet&#224; Read Write (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "get (funzione di accesso) [C#], dichiarazione di proprietà"
  - "set (funzione di accesso) [C#]"
  - "proprietà [C#], dichiarazione"
  - "proprietà in lettura e scrittura [C#]"
  - "funzioni di accesso [C#], dichiarazione di proprietà con"
ms.assetid: a4962fef-af7e-4c4b-a929-4ae4d646ab8a
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: dichiarare e usare propriet&#224; Read Write (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le proprietà offrono i vantaggi dei membri dati pubblici senza i rischi associati all'accesso non protetto, non controllato e non verificato ai dati di un oggetto.  Ciò si ottiene tramite le *funzioni di accesso*, ossia metodi speciali che assegnano e recuperano valori dal membro dati sottostante.  La funzione di accesso [set](../../../csharp/language-reference/keywords/set.md) consente l'assegnazione di valori ai membri dati, mentre la funzione di accesso [get](../../../csharp/language-reference/keywords/get.md) recupera i valori dei membri dati.  
  
 Questo esempio presenta una classe `Person` con due proprietà: `Name` \(string\) e `Age` \(int\).  Entrambe le proprietà forniscono le funzioni di accesso `get` e `set`, quindi vengono considerate proprietà in lettura\/scrittura.  
  
## Esempio  
 [!code-cs[csProgGuideObjects#33](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_1.cs)]  
  
## Programmazione efficiente  
 Nell'esempio precedente le proprietà `Name` e `Age` sono [pubbliche](../../../csharp/language-reference/keywords/public.md) e comprendono una funzione di accesso `get` e una funzione di accesso `set`.  In questo modo qualsiasi oggetto può leggere e scrivere tali proprietà.  È a volte preferibile, tuttavia, escludere una delle funzioni di accesso.  Se ad esempio la funzione di accesso `set` viene omessa, la proprietà diventa in sola lettura:  
  
 [!code-cs[csProgGuideObjects#87](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_2.cs)]  
  
 In alternativa è possibile esporre una funzione di accesso pubblicamente ma rendere l'altra privata o protetta.  Per ulteriori informazioni, vedere [Accessibilità asimmetrica delle funzioni di accesso](../../../csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility.md).  
  
 Una volta dichiarate le proprietà, è possibile utilizzare questi metodi come se si trattasse di campi della classe.  Questo consente di utilizzare una sintassi molto semplice quando si desidera ottenere o impostare il valore di una proprietà, come nelle seguenti istruzioni:  
  
 [!code-cs[csProgGuideObjects#35](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_3.cs)]  
  
 Tenere presente che in un metodo `set` di una proprietà è disponibile una variabile `value` speciale.  Tale variabile contiene il valore specificato dall'utente, ad esempio:  
  
 [!code-cs[csProgGuideObjects#36](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_4.cs)]  
  
 La sintassi per l'incremento della proprietà `Age` per un oggetto `Person` è molto semplice:  
  
 [!code-cs[csProgGuideObjects#37](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_5.cs)]  
  
 Se si utilizzassero due metodi `set` e `get` distinti per impostare le proprietà, sarebbe necessaria una stringa di codice del seguente tipo:  
  
```  
person.SetAge(person.GetAge() + 1);   
```  
  
 In questo esempio viene eseguito l'override del metodo `ToString`:  
  
 [!code-cs[csProgGuideObjects#38](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-declare-and-use-read-write-properties_6.cs)]  
  
 Il metodo `ToString` non è utilizzato in modo esplicito nel programma,  ma viene richiamato per impostazione predefinita dalle chiamate a `WriteLine`.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)