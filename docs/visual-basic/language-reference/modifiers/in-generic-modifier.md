---
title: "In (Generic Modifier) (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.VarianceIn"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "contravariance, In keyword [Visual Basic]"
  - "In keyword [Visual Basic]"
ms.assetid: 59bb13c5-fe96-42b8-8286-86293d1661c5
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# In (Generic Modifier) (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per i parametri di tipo generico, la parola chiave `In` specifica che il parametro di tipo è controvariante.  
  
## Note  
 La controvarianza consente di utilizzare un tipo meno derivato di quello specificato dal parametro generico.  Ciò consente la conversione implicita di classi che implementano interfacce variant e la conversione implicita di tipi delegati.  
  
 Per ulteriori informazioni, vedere [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Regole  
 È possibile utilizzare la parola chiave `In` in interfacce e delegati generici.  
  
 Un parametro di tipo può essere dichiarato controvariante in un'interfaccia o delegato generico se è utilizzato solo come tipo di argomenti di metodo e non come tipo restituito dal metodo.  I parametri `ByRef` non possono essere covarianti o controvarianti.  
  
 La covarianza e la controvarianza sono supportate per i tipi di riferimento e non per i tipi di valore.  
  
 In Visual Basic, non è possibile dichiarare eventi nelle interfacce controvarianti senza specificare il tipo di delegato.  Inoltre, le interfacce controvarianti non possono disporre di strutture, enumerazioni o classi annidate, ma possono disporre di interfacce annidate.  
  
## Comportamento  
 Un'interfaccia che dispone di un parametro di tipo controvariante consente ai metodi di accettare argomenti di tipi meno derivati di quelli specificati dal parametro di tipo di interfaccia.  Poiché, ad esempio, in .NET Framework 4, nell'interfaccia <xref:System.Collections.Generic.IComparer%601>, il tipo T è controvariante, è possibile assegnare un oggetto del tipo `IComparer(Of Person)` a un oggetto del tipo `IComparer(Of Employee)` senza utilizzare alcun metodo di conversione speciale se `Person` eredita `Employee`.  
  
 A un delegato controvariante può essere assegnato un altro delegato dello stesso tipo, ma con un parametro di tipo generico meno derivato.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, estendere e implementare un'interfaccia generica controvariante.  Viene inoltre illustrato come sia possibile utilizzare la conversione implicita per le classi che implementano questa interfaccia.  
  
 [!code-vb[vbVarianceKeywords#1](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/in-generic-modifier_1.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, creare un'istanza e richiamare un delegato generico controvariante.  Viene inoltre illustrato come sia possibile convertire in modo implicito un tipo delegato.  
  
 [!code-vb[vbVarianceKeywords#2](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/in-generic-modifier_2.vb)]  
  
## Vedere anche  
 [Varianza nelle interfacce generiche](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)