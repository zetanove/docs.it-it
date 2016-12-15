---
title: "string (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "string"
  - "string_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "stringhe [C#], riferimenti"
  - "@ (valore letterale stringa)"
  - "valori letterali stringa [C#]"
  - "string (parola chiave) [C#]"
ms.assetid: 3037e558-fb22-494d-bca1-a15ade11b11a
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# string (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il tipo `string` rappresenta una sequenza di zero o più caratteri Unicode.  Il tipo `string` è un alias dell'elemento <xref:System.String> in .NET Framework.  
  
 Sebbene `string` sia un tipo di riferimento, gli operatori di uguaglianza \(`==` e `!=`\) vengono definiti per confrontare i valori degli oggetti `string`, non i riferimenti.  Questo rende più intuitiva la verifica dell'uguaglianza delle stringhe.  Ad esempio:  
  
```c#  
  
      string a = "hello";  
string b = "h";  
// Append to contents of 'b'  
b += "ello";  
Console.WriteLine(a == b);  
Console.WriteLine((object)a == (object)b);  
```  
  
 Viene visualizzato "True" e quindi "False" perché i contenuti delle stringhe sono equivalenti, ma `a` e `b` non fanno riferimento alla stessa istanza di stringa.  
  
 L'operatore \+ concatena le stringhe:  
  
```c#  
  
string a = "good " + "morning";  
```  
  
 Viene creato un oggetto stringa che contiene "good morning".  
  
 Le stringhe *non sono modificabili*, ovvero il contenuto di un oggetto di tipo stringa non può essere modificato dopo che l'oggetto è stato creato, nonostante la sintassi faccia inferire il contrario.  Ad esempio, scrivendo il codice definito, il compilatore creerà in realtà un nuovo oggetto di tipo stringa nel quale archiviare la nuova sequenza di caratteri, quindi il nuovo oggetto verrà assegnato a b.  La stringa "h" è quindi idonea per Garbage Collection.  
  
```c#  
  
      string b = "h";  
b += "ello";  
```  
  
 È possibile utilizzare l'operatore \[\] per accedere in sola lettura ai singoli caratteri di un oggetto `string`:  
  
```c#  
  
      string str = "test";  
char x = str[2];  // x = 's';  
```  
  
 Le stringhe letterali sono di tipo `string` e possono essere scritte in due formati, tra virgolette oppure tra virgolette e preceduti da @.  Le stringhe letterali racchiuse tra virgolette sono precedute e seguite da virgolette doppie \("\):  
  
```c#  
"good morning"  // a string literal  
```  
  
 I valori letterali stringa possono contenere qualsiasi valore letterale carattere.  Le sequenze di escape sono incluse.  Nell'esempio seguente vengono utilizzate le sequenze di escape `\\` per la barra rovesciata, `\u0066` per la lettera f e `\n` per l'indicatore di nuova riga.  
  
```  
  
      string a = "\\\u0066\n";  
Console.WriteLine(a);  
```  
  
> [!NOTE]
>  Il codice di escape `\`u`dddd`, dove `dddd` è un numero a quattro cifre, rappresenta il carattere Unicode U\+`dddd`.  Sono inoltre riconosciuti i codici di escape Unicode a otto cifre: `\Udddddddd`.  
  
 I valori letterali stringa verbatim iniziano con @ e sono anche racchiusi tra virgolette doppie.  Ad esempio:  
  
```c#  
@"good morning"  // a string literal  
```  
  
 Il vantaggio dell'utilizzo delle stringhe verbatim è che le sequenze di escape *non* vengono elaborate e questo semplifica la scrittura, ad esempio, di un nome di file completo:  
  
```c#  
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"  
```  
  
 Per includere delle virgolette doppie in una stringa tra virgolette preceduta da @, sarà necessario raddoppiare le virgolette:  
  
```c#  
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.  
```  
  
 È inoltre possibile utilizzare il simbolo @ per avvalersi di identificatori a cui si fa riferimento \([\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)\) e che rappresentano parole chiave C\#.  
  
 Per ulteriori informazioni sulle stringhe in C\#, vedere [Stringhe](../../../csharp/programming-guide/strings/index.md).  
  
## Esempio  
 [!code-cs[csrefKeywordsTypes#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/string_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Procedure consigliate per l'utilizzo di stringhe](../Topic/Best%20Practices%20for%20Using%20Strings%20in%20the%20.NET%20Framework.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)   
 [Operazioni di base su stringhe](../Topic/Basic%20String%20Operations%20in%20the%20.NET%20Framework.md)   
 [Creazione di nuove stringhe](../Topic/Creating%20New%20Strings%20in%20the%20.NET%20Framework.md)   
 [Tabella di formattazione dei risultati numerici](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)