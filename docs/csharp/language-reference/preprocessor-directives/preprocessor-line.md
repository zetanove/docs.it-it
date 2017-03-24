---
title: "#line (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#line"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#line (direttiva) [C#]"
ms.assetid: 6439e525-5dd5-4acb-b8ea-efabb32ff95b
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# #line (Riferimenti per C#)
`#line` consente di modificare il numero di riga del compilatore e, facoltativamente, l'output del nome del file per gli errori e gli avvisi.  Nell'esempio riportato di seguito viene illustrata la modalità di segnalazione di due avvisi associati a numeri di riga.  La direttiva `#line 200` forza l'impostazione del numero di riga a 200 \(anche se l'impostazione predefinita è \#7\) e fino alla successiva direttiva \#line il nome file viene indicato come "Special".  La direttiva \#line predefinita reimposta la numerazione predefinita delle righe, con il conteggio delle righe rinumerate dalla direttiva precedente.  
  
```  
class MainClass  
{  
    static void Main()  
    {  
#line 200 "Special"  
        int i;    // CS0168 on line 200  
        int j;    // CS0168 on line 201  
#line default  
        char c;   // CS0168 on line 9  
        float f;  // CS0168 on line 10  
#line hidden // numbering not affected  
        string s;   
        double d; // CS0168 on line 13  
    }  
}  
```  
  
## Note  
 La direttiva `#line` può essere utilizzata in un'istruzione automatizzata intermedia nel processo di compilazione.  Se, ad esempio, sono state rimosse delle righe dal file del codice sorgente originale e si desidera che il compilatore generi comunque un output basato sulla numerazione originale delle righe del file, è possibile rimuovere le righe e simulare la numerazione originale tramite `#line`.  
  
 La direttiva `#line hidden` nasconde al debugger le righe successive, in modo che quando lo sviluppatore eseguirà il codice un'istruzione alla volta, verranno eseguite tutte le righe racchiuse tra una direttiva `#line hidden` e la successiva direttiva `#line` \(supposto che non si tratti di un'altra direttiva `#line hidden`\).  Questa opzione può essere utilizzata anche per consentire ad ASP.NET di distinguere il codice definito dall'utente da quello generato dal computer.  Sebbene ASP.NET rappresenti il consumer principale di questa funzionalità, è probabile che altri generatori di codice sorgente ne usufruiranno.  
  
 Una direttiva `#line hidden` non influisce sui nomi di file o sui numeri di riga nella segnalazione degli errori.  Vale a dire che se viene rilevato un errore in un blocco nascosto, nel compilatore verrà segnalato il nome del file corrente e il numero di riga dell'errore.  
  
 La direttiva `#line filename` specifica il nome del file che si desidera venga visualizzato nell'output del compilatore.  Per impostazione predefinita, viene utilizzato il nome effettivo del file del codice sorgente.  Il nome file deve essere racchiuso tra virgolette doppie \(""\) e deve essere preceduto da un numero di riga.  
  
 I file del codice sorgente possono contenere più direttive `#line`.  
  
## Esempio 1  
 Nell'esempio che segue viene illustrato come il debugger ignori le righe nascoste nel codice.  Durante l'esecuzione dell'esempio, verranno visualizzate tre righe di testo.  Tuttavia, quando si imposta un punto di interruzione, come illustrato nell'esempio, e si preme F10 per eseguire il codice un'istruzione alla volta, si noterà che la riga nascosta verrà ignorata.  La stessa cosa si verifica anche se si imposta un punto di interruzione in corrispondenza della riga nascosta.  
  
```  
// preprocessor_linehidden.cs  
using System;  
class MainClass   
{  
    static void Main()   
    {  
        Console.WriteLine("Normal line #1."); // Set break point here.  
#line hidden  
        Console.WriteLine("Hidden line.");  
#line default  
        Console.WriteLine("Normal line #2.");  
    }  
}  
```  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)