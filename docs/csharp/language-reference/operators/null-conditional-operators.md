---
title: "Operatori condizionali Null (C# e Visual Basic) | Microsoft Docs"
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
ms.assetid: 9c7b2c8f-a785-44ca-836c-407bfb6d27f5
caps.latest.revision: 3
caps.handback.revision: 3
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatori condizionali Null (C# e Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Vengono usati per verificare la presenza di valori Null prima di eseguire un'operazione di accesso ai membri \(`?.`\) o di indice \(`?[`\).  Questi operatori consentono di scrivere meno codice per gestire i controlli null, soprattutto per l'ordinamento decrescente delle strutture di dati.  
  
```c#  
int? length = customers?.Length; // null if customers is null   
Customer first = customers?[0];  // null if customers is null  
int? count = customers?[0]?.Orders?.Count();  // null if customers, the first customer, or Orders is null  
  
```  
  
```vb  
Dim length = customers?.Length  ‘’ null if customers is null  
Dim first as Customer = customers?(0);  ‘’ null if customers is null  
Dim count as Integer? = customers?[0]?.Orders?.Count();  // null if customers, the first customer, or Orders is null  
  
```  
  
 Nell'ultimo esempio viene dimostrato che gli operatori con condizione Null causano un corto circuito.  Se un'operazione in una catena di operazioni condizionali di indice e accesso ai membri restituisce Null, l'esecuzione delle altre operazioni della catena viene interrotta.  L'esecuzione di altre operazioni con precedenza inferiore nell'espressione invece può continuare.  Ad esempio, nel codice seguente `E` viene sempre eseguita e le operazioni `??` e `==` vengono eseguite.  
  
```vb-c#  
A?.B?.C?[0] ?? E  
A?.B?.C?[0] == E  
  
```  
  
 L'accesso ai membri con condizione Null viene usato anche per richiamare delegati in modo thread\-safe scrivendo molto meno codice.  In passato era necessario codice simile al seguente:  
  
```c#  
var handler = this.PropertyChanged;  
if (handler != null)  
    handler(…)  
  
```  
  
```vb  
Dim handler = AddressOf(Me.PropertyChanged)  
If handler IsNot Nothing  
    Call handler(…)  
  
```  
  
 Ora tutto è molto più semplice:  
  
```vb-c#  
PropertyChanged?.Invoke(e)  
  
```  
  
 Il codice creato in questo modo è thread\-safe perché il compilatore genera il codice per valutare `PropertyChanged` una sola volta, mantenendo il risultato nella variabile temporanea.  
  
 È necessario chiamare esplicitamente il metodo `Invoke` perché non esiste una sintassi di chiamata dei delegati con condizione Null `PropertyChanged?(e)`.  In precedenza esistevano troppe situazioni di analisi ambigue che lo consentivano.  
  
## Specifiche del linguaggio  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
 Per altre informazioni, vedere [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md)   
 [Visual Basic Programming Guide](../../../visual-basic/programming-guide/index.md)