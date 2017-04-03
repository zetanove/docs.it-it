---
title: Refactoring in funzioni pure (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 2944a0d4-fd33-4e2e-badd-abb0f9be2fcc
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d0243dbc1a884cb48eeebd71079c3b17bc520553
ms.lasthandoff: 03/13/2017


---
# <a name="refactoring-into-pure-functions-c"></a>Refactoring in funzioni pure (C#)
Per le trasformazioni funzionali pure, è fondamentale comprendere come eseguire il refactoring del codice usando funzioni pure.  
  
> [!NOTE]
>  La nomenclatura comune nella programmazione funzionale prevede il refactoring dei programmi tramite funzioni pure. In Visual Basic e C++, ciò è in linea con l'uso di funzioni nei rispettivi linguaggi. Tuttavia, in C# le funzioni sono denominate metodi. Ai fini del presente documento, una funzione pura viene implementata come metodo in C#.  
  
 Come accennato in precedenza, una funzione pura prevede due caratteristiche utili:  
  
-   Non ha effetti collaterali. La funzione non cambia le variabili o i dati di qualsiasi tipo all'esterno della funzione.  
  
-   È coerente. Dato lo stesso set di dati di input, restituirà sempre lo stesso valore di output.  
  
 Per passare alla programmazione funzionale, è possibile eseguire il refactoring del codice esistente per eliminare inutili effetti collaterali e dipendenze esterne. In questo modo, è possibile creare versioni di funzioni pure del codice esistente.  
  
 In questo argomento vengono descritte le caratteristiche presenti e non presenti in una funzione pura. L'[esercitazione sulla modifica del contenuto in un documento WordprocessingML (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md) illustra come modificare un documento WordprocessingML e contiene due esempi su come eseguire il refactoring usando una funzione pura.  
  
## <a name="eliminating-side-effects-and-external-dependencies"></a>Eliminazione di effetti collaterali e dipendenze esterne  
 Negli esempi seguenti vengono confrontate due funzioni non pure e una funzione pura.  
  
### <a name="non-pure-function-that-changes-a-class-member"></a>Funzione non pura che modifica un membro di classe  
 Nel codice seguente la funzione `HypenatedConcat` non è una funzione pura perché modifica il membro dati `aMember` nella classe:  
  
```csharp  
public class Program  
{  
    private static string aMember = "StringOne";  
  
    public static void HypenatedConcat(string appendStr)  
    {  
        aMember += '-' + appendStr;  
    }  
  
    public static void Main()  
    {  
        HypenatedConcat("StringTwo");  
        Console.WriteLine(aMember);  
    }  
}  
```  
  
 L'output del codice è il seguente:  
  
```  
StringOne-StringTwo  
```  
  
 Si noti che è irrilevante se per i dati l'accesso è `public` o `private` oppure se i dati sono un membro `static` o un membro di istanza. Una funzione pura non modifica i dati all'eterno della funzione.  
  
### <a name="non-pure-function-that-changes-an-argument"></a>Funzione non pura che modifica un argomento  
 Inoltre, la versione seguente di questa stessa funzione non è pura, perché modifica il contenuto del parametro, `sb`.  
  
```csharp  
public class Program  
{  
    public static void HypenatedConcat(StringBuilder sb, String appendStr)  
    {  
        sb.Append('-' + appendStr);  
    }  
  
    public static void Main()  
    {  
        StringBuilder sb1 = new StringBuilder("StringOne");  
        HypenatedConcat(sb1, "StringTwo");  
        Console.WriteLine(sb1);  
    }  
}  
```  
  
 Questa versione del programma produce lo stesso output della prima versione, perché la funzione `HypenatedConcat` ha modificato il valore (stato) del primo parametro richiamando la funzione del membro <xref:System.Text.StringBuilder.Append%2A>. Si noti che questa modifica si verifica nonostante il fatto che `HypenatedConcat` usa il passaggio di parametri in base a chiamata per valore.  
  
> [!IMPORTANT]
>  Per i tipi di riferimenti, se un parametro viene passato per valore, il risultato è una copia del riferimento a un oggetto passato. Questa copia è ancora associata agli stessi dati di istanza del riferimento originale, finché la variabile di riferimento non viene assegnata a un nuovo oggetto. La chiamata per riferimento non è necessariamente richiesta affinché una funzione modifichi un parametro.  
  
### <a name="pure-function"></a>Funzione pura  
 Nella versione successiva del programma viene illustrato come implementare la funzione `HypenatedConcat` come funzione pura.  
  
```csharp  
class Program  
{  
    public static string HyphenatedConcat(string s, string appendStr)  
    {  
        return (s + '-' + appendStr);  
    }  
  
    public static void Main(string[] args)  
    {  
        string s1 = "StringOne";  
        string s2 = HyphenatedConcat(s1, "StringTwo");  
        Console.WriteLine(s2);  
    }  
}  
```  
  
 Anche in questo caso, la versione produce la stessa riga di output: `StringOne-StringTwo` Si noti che per mantenere il valore concatenato, viene archiviato nella variabile intermedia `s2`.  
  
 Un approccio che può risultare utile consiste nello scrivere funzioni localmente non pure, ossia che dichiarano e modificano variabili locali, ma globalmente pure. Tali funzioni presentano molte caratteristiche utili in termini di componibilità, ma evitano alcune delle complessità dei linguaggi di programmazione funzionali, ad esempio la necessità di usare la ricorsione quando con un semplice ciclo si otterrebbe lo stesso risultato.  
  
## <a name="standard-query-operators"></a>Operatori di query standard  
 Una caratteristica importante degli operatori di query standard è che vengono implementati come funzioni pure.  
  
 Per altre informazioni, vedere [Panoramica degli operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle trasformazioni funzionali pure (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [Differenze tra programmazione funzionale e programmazione imperativa (C#)](../../../../csharp/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)
