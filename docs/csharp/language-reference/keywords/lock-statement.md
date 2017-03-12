---
title: "Istruzione lock (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "lock_CSharpKeyword"
  - "lock"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lock (parola chiave) [C#]"
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
caps.latest.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 43
---
# Istruzione lock (Riferimenti per C#)
La parola chiave `lock` contrassegna un blocco di istruzioni come sezione critica ottenendo il blocco a esclusione reciproca per un determinato oggetto, eseguendo un'istruzione e rilasciando in seguito il blocco.  L'esempio seguente illustra un'istruzione `lock`.  
  
```  
  
class Account  
{  
    decimal balance;  
    private Object thisLock = new Object();  
  
    public void Withdraw(decimal amount)  
    {  
        lock (thisLock)  
        {  
            if (amount > balance)  
            {  
                throw new Exception("Insufficient funds");  
            }  
            balance -= amount;  
        }  
    }  
}  
  
```  
  
 Per ulteriori informazioni, vedere [Sincronizzazione di thread](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Note  
 La parola chiave `lock` impedisce a un thread di entrare in una sezione critica del codice se è già presente un altro thread.  Se un altro thread tenta di accedere a un codice bloccato, attenderà \(in stato di blocco\) finché l'oggetto non verrà rilasciato.  
  
 Nella sezione [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md) vengono fornite informazioni sul threading.  
  
 La parola chiave `lock` chiama <xref:System.Threading.Monitor.Enter%2A> all'inizio del blocco e <xref:System.Threading.Monitor.Exit%2A> alla fine del blocco.  <xref:System.Threading.ThreadInterruptedException> viene generato se <xref:System.Threading.Thread.Interrupt%2A> interrompere un thread in attesa di per immettere un'istruzione `lock`.  
  
 In generale è opportuno evitare il blocco su un tipo `public` o su istanze oltre il controllo del codice.  I costrutti comuni `lock (this)`, `lock (typeof (MyType))` e `lock ("myLock")` non rispettano questa regola:  
  
-   `lock (this)` costituisce un problema se l'accesso all'istanza può avvenire pubblicamente.  
  
-   `lock (typeof (MyType))` costituisce un problema se l'accesso a `MyType` può avvenire pubblicamente.  
  
-   `lock("myLock")` costituisce un problema poiché qualsiasi altro codice nel processo che utilizza la stessa stringa condividerà lo stesso blocco.  
  
 La procedura migliore consiste nel definire un oggetto `private` da bloccare o una variabile oggetto `private static` per proteggere i dati comuni a tutte le istanze.  
  
 Non è possibile utilizzare la parola chiave [attendere](../../../csharp/language-reference/keywords/await.md) nel corpo di un'istruzione `lock`.  
  
## Esempio  
 Nell'esempio seguente viene illustrato un utilizzo semplificato dei thread senza blocco in C\#.  
  
 [!code-cs[csrefKeywordsFixedLock#5](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#5)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono utilizzati thread e `lock`.  Finché l'istruzione `lock` è presente, il blocco di istruzioni rimarrà una sezione critica e `balance` non diventerà mai un numero negativo.  
  
 [!code-cs[csrefKeywordsFixedLock#6](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#6)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.Reflection.MethodImplAttributes>   
 <xref:System.Threading.Mutex>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per le istruzioni](../../../csharp/language-reference/keywords/statement-keywords.md)   
 [Monitor](../Topic/Monitors.md)   
 [Interlocked Operations](../Topic/Interlocked%20Operations.md)   
 [AutoResetEvent](../Topic/AutoResetEvent.md)   
 [Sincronizzazione di thread](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)