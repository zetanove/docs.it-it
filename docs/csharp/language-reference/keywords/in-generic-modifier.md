---
title: "in (Modificatore generico) (Riferimenti per C#) | Microsoft Docs"
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
  - "controvarianza, in (parola chiave) [C#]"
  - "in (parola chiave) [C#]"
ms.assetid: 3a778c36-8aed-4ebe-aa8b-39f4057215b1
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# in (Modificatore generico) (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per i parametri di tipo generico, la parola chiave `in` specifica che il parametro di tipo è controvariante.  È possibile utilizzare la parola chiave `in` in interfacce e delegati generici.  
  
 La controvarianza consente di utilizzare un tipo meno derivato di quello specificato dal parametro generico.  Ciò consente la conversione implicita di classi che implementano interfacce variant e la conversione implicita di tipi delegati.  La covarianza e la controvarianza nei parametri di tipo generico sono supportate per i tipi di riferimento, ma non per i tipi di valore.  
  
 Un tipo può essere dichiarato controvariante in un'interfaccia o delegato generico se viene utilizzato solo come tipo di argomenti del metodo e non come tipo restituito dal metodo.  I parametri `Ref` e `out` non possono essere variant.  
  
 Un'interfaccia che dispone di un parametro di tipo controvariante consente ai metodi di accettare argomenti di tipi meno derivati di quelli specificati dal parametro di tipo di interfaccia.  Poiché, ad esempio, in .NET Framework 4, nell'interfaccia <xref:System.Collections.Generic.IComparer%601>, il tipo T è controvariante, è possibile assegnare un oggetto del tipo `IComparer(Of Person)` a un oggetto del tipo `IComparer(Of Employee)` senza utilizzare alcun metodo di conversione speciale se `Employee` eredita `Person`.  
  
 A un delegato controvariante può essere assegnato un altro delegato dello stesso tipo, ma con un parametro di tipo generico meno derivato.  
  
 Per ulteriori informazioni, vedere [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, estendere e implementare un'interfaccia generica controvariante.  Viene inoltre illustrato come sia possibile utilizzare la conversione implicita per le classi che implementano questa interfaccia.  
  
 [!code-cs[csVarianceKeywords#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/in-generic-modifier_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, creare un'istanza e richiamare un delegato generico controvariante.  Viene inoltre illustrato come sia possibile convertire in modo implicito un tipo delegato.  
  
 [!code-cs[csVarianceKeywords#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/in-generic-modifier_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [out](../../../csharp/language-reference/keywords/out-generic-modifier.md)   
 [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)