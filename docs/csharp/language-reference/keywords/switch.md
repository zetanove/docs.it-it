---
title: "switch (Riferimenti per C#) | Microsoft Docs"
ms.date: "2017-03-07"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "switch_CSharpKeyword"
  - "switch"
  - "case"
  - "case_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "switch (istruzione) [C#]"
  - "switch (parola chiave) [C#]"
  - "case (istruzione) [C#]"
  - "default (parola chiave) [C#]"
ms.assetid: 44bae8b8-8841-4d85-826b-8a94277daecb
caps.latest.revision: 47
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 47
---
# switch (Riferimenti per C#)
L'istruzione `switch` è un'istruzione di controllo che seleziona una *sezione opzioni* da eseguire da un elenco di candidati.  
  
 Un'istruzione `switch` include una o più sezioni opzioni.  Ogni sezione opzioni contiene una o più *etichette case* seguite da una o più istruzioni.  Nell'esempio seguente viene illustrata una semplice istruzione `switch` con tre sezioni opzioni.  Ogni sezione opzione ha un'etichetta case, ad esempio `case 1`, e due istruzioni.  
  
 [!code-cs[csrefKeywordsSelection#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/switch_1.cs)]  
  
## Note  
 Ogni etichetta case specifica un valore costante.  L'istruzione switch trasferisce il controllo alla sezione opzioni la cui etichetta case corrisponde al valore dell'*espressione switch* \(`caseSwitch` nell'esempio\).  Se nessuna etichetta case contiene un valore corrispondente, il controllo viene trasferito alla sezione `default`, se esistente.  Se non è presente alcuna sezione `default`, non viene eseguita alcuna azione e il controllo viene trasferito al di fuori dell'istruzione `switch`.  Nell'esempio precedente le istruzioni nella prima parte della sezione opzioni vengono eseguite perché `case 1` corrisponde al valore di `caseSwitch`.  
  
 Un'istruzione `switch` può contenere qualsiasi numero di sezioni opzioni e ogni sezione può avere una o più etichette case come illustrato nell'esempio di etichette case della stringa di seguito.  Tuttavia, due etichette case non possono contenere lo stesso valore di costante.  
  
 L'esecuzione dell'elenco di istruzioni nella sezione opzioni selezionata inizia con la prima istruzione e continua nell'elenco di istruzioni, in genere fino a raggiungere un istruzione jump, ad esempio `break`, `goto case`, `return` o `throw`.  A quel punto, il controllo viene trasferito al di fuori dell'istruzione `switch` o in un'altra etichetta case.  
  
 A differenza di C\+\+, C\# non consente di continuare l'esecuzione da una sezione opzioni a quella successiva.  Il codice seguente causa un errore.  
  
```c#  
switch (caseSwitch)  
{  
    // The following switch section causes an error.  
    case 1:  
        Console.WriteLine("Case 1...");  
        // Add a break or other jump statement here.  
    case 2:  
        Console.WriteLine("... and/or Case 2");  
        break;  
}  
```  
  
 C\# richiede che la fine delle sezioni opzioni, inclusa quella finale, non sia raggiungibile.  Ciò significa che, a differenza di altri linguaggi, il codice non può passare nella successiva sezione opzioni.  Sebbene questo requisito venga in genere soddisfatto utilizzando un'istruzione `break`, è valido anche il caso seguente poiché garantisce che la fine dell'elenco di istruzioni non venga raggiunta.  
  
```c#  
case 4:  
    while (true)  
        Console.WriteLine("Endless looping. . . .");  
```  
  
## Esempio  
 Nell'esempio seguente vengono illustrati i requisiti e le funzionalità di un'istruzione `switch`.  
  
 [!code-cs[csrefKeywordsSelection#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/switch_2.cs)]  
  
## Esempio  
 Nell'esempio finale la variabile di stringa, `str`, e le etichette case della stringa controllano il flusso di esecuzione.  
  
 [!code-cs[csrefKeywordsSelection#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/switch_3.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione switch \(C\+\+\)](/visual-cpp/cpp/switch-statement-cpp)   
 [if\-else](../../../csharp/language-reference/keywords/if-else.md)