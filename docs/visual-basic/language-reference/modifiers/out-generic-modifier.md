---
title: "Out (Generic Modifier) (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.VarianceOut"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Out keyword [Visual Basic]"
  - "covariance, Out keyword [Visual Basic]"
ms.assetid: c4418369-1518-4a46-9a1e-054c61038eca
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Out (Generic Modifier) (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per i parametri di tipo generico, la parola chiave `Out` specifica che il tipo è covariante.  
  
## Note  
 La covarianza consente di utilizzare un tipo più derivato di quello specificato dal parametro generico.  Ciò consente la conversione implicita di classi che implementano interfacce variant e la conversione implicita di tipi delegati.  
  
 Per ulteriori informazioni, vedere [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Regole  
 È possibile utilizzare la parola chiave `Out` in interfacce e delegati generici.  
  
 In un'interfaccia generica, un parametro di tipo può essere dichiarato covariante se soddisfa le condizioni seguenti:  
  
-   Il parametro di tipo viene utilizzato solo come tipo restituito di metodi di interfaccia e non viene utilizzato come tipo di argomenti del metodo.  
  
    > [!NOTE]
    >  Esiste un'eccezione a questa regola.  Se in un'interfaccia covariante si dispone di un delegato generico controvariante come parametro del metodo, è possibile utilizzare il tipo covariante come parametro di tipo generico per questo delegato.  Per ulteriori informazioni sui delegati generici covarianti e controvarianti, vedere [Varianza nei delegati](../Topic/Variance%20in%20Delegates%20\(C%23%20and%20Visual%20Basic\).md) e [Utilizzo della varianza per i delegati generici Func e Action](../Topic/Using%20Variance%20for%20Func%20and%20Action%20Generic%20Delegates%20\(C%23%20and%20Visual%20Basic\).md).  
  
-   Il parametro di tipo non viene utilizzato come vincolo generico per i metodi di interfaccia.  
  
 In un delegato generico, un parametro di tipo può essere dichiarato covariante se viene utilizzato solo come tipo restituito del metodo e non per gli argomenti del metodo.  
  
 La covarianza e la controvarianza sono supportate per i tipi di riferimento, ma non per i tipi di valore.  
  
 In Visual Basic, non è possibile dichiarare eventi nelle interfacce covarianti senza specificare il tipo di delegato.  Inoltre, le interfacce covarianti non possono disporre di strutture, enumerazioni o classi annidate, ma possono disporre di interfacce annidate.  
  
## Comportamento  
 Un'interfaccia che dispone di un parametro di tipo covariante consente ai metodi di restituire tipi più derivati di quelli specificati dal parametro di tipo.  Poiché, ad esempio, in .NET Framework 4, nell'interfaccia <xref:System.Collections.Generic.IEnumerable%601>, il tipo T è covariante, è possibile assegnare un oggetto del tipo `IEnumerabe(Of String)` a un oggetto del tipo `IEnumerable(Of Object)` senza utilizzare alcun metodo di conversione speciale.  
  
 A un delegato covariante può essere assegnato un altro delegato dello stesso tipo, ma con un parametro di tipo generico più derivato.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, estendere e implementare un'interfaccia generica covariante.  Viene inoltre illustrato come utilizzare la conversione implicita per le classi che implementano un'interfaccia covariante.  
  
 [!code-vb[vbVarianceKeywords#3](../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/out-generic-modifier_1.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come dichiarare, creare un'istanza e richiamare un delegato generico covariante.  Viene inoltre illustrato come sia possibile utilizzare la conversione implicita per i tipi delegati.  
  
 [!code-vb[vbVarianceKeywords#4](../../../visual-basic/language-reference/modifiers/codesnippet/visualbasic/out-generic-modifier_2.vb)]  
  
## Vedere anche  
 [Varianza nelle interfacce generiche](../Topic/Variance%20in%20Generic%20Interfaces%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)