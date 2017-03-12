---
title: "out (Modificatore generico) (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "covarianza, out (parola chiave) [C#]"
  - "out (parola chiave) [C#]"
ms.assetid: f8c20dec-a8bc-426a-9882-4076b1db1e00
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# out (Modificatore generico) (Riferimenti per C#)
Per i parametri di tipo generico, la parola chiave `out` specifica che il parametro di tipo è covariante.  È possibile utilizzare la parola chiave `out` in interfacce e delegati generici.  
  
 La covarianza consente di utilizzare un tipo più derivato di quello specificato dal parametro generico.  Ciò consente la conversione implicita di classi che implementano interfacce variant e la conversione implicita di tipi delegati.  La covarianza e la controvarianza sono supportate per i tipi di riferimento, ma non per i tipi di valore.  
  
 Un'interfaccia che dispone di un parametro di tipo covariante consente ai metodi di restituire tipi più derivati di quelli specificati dal parametro di tipo.  Poiché, ad esempio, in .NET Framework 4, nell'interfaccia <xref:System.Collections.Generic.IEnumerable%601>, il tipo T è covariante, è possibile assegnare un oggetto del tipo `IEnumerabe(Of String)` a un oggetto del tipo `IEnumerable(Of Object)` senza utilizzare alcun metodo di conversione speciale.  
  
 A un delegato covariante può essere assegnato un altro delegato dello stesso tipo, ma con un parametro di tipo generico più derivato.  
  
 Per ulteriori informazioni, vedere [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, estendere e implementare un'interfaccia generica covariante.  Viene inoltre illustrato come utilizzare la conversione implicita per le classi che implementano un'interfaccia covariante.  
  
 [!code-cs[csVarianceKeywords#3](../../../csharp/language-reference/keywords/codesnippet/csharp/out-generic-modifier_1.cs)]  
  
 In un'interfaccia generica, un parametro di tipo può essere dichiarato covariante se soddisfa le condizioni seguenti:  
  
-   Il parametro di tipo viene utilizzato solo come tipo restituito di metodi di interfaccia e non viene utilizzato come tipo di argomenti del metodo.  
  
    > [!NOTE]
    >  Esiste un'eccezione a questa regola.  Se in un'interfaccia covariante si dispone di un delegato generico controvariante come parametro del metodo, è possibile utilizzare il tipo covariante come parametro di tipo generico per questo delegato.  Per ulteriori informazioni sui delegati generici covarianti e controvarianti, vedere [Varianza nei delegati](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md) e [Utilizzo della varianza per i delegati generici Func e Action](../Topic/Using%20Variance%20for%20Func%20and%20Action%20Generic%20Delegates%20\(C%23%20and%20Visual%20Basic\).md).  
  
-   Il parametro di tipo non viene utilizzato come vincolo generico per i metodi di interfaccia.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, creare un'istanza e richiamare un delegato generico covariante.  Viene inoltre illustrato come convertire in modo implicito i tipi delegati.  
  
 [!code-cs[csVarianceKeywords#4](../../../csharp/language-reference/keywords/codesnippet/csharp/out-generic-modifier_2.cs)]  
  
 In un delegato generico, un tipo può essere dichiarato covariante se viene utilizzato solo come tipo restituito del metodo e non per gli argomenti del metodo.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Varianza nelle interfacce generiche](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [in](../../../csharp/language-reference/keywords/in-generic-modifier.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)