---
title: "Direttiva using (Riferimenti per C#) | Microsoft Docs"
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
  - "using (direttiva) [C#]"
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
caps.latest.revision: 31
caps.handback.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Direttiva using (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La direttiva `using` ha tre usi:  
  
-   Consentire l'uso di tipi in uno spazio dei nomi in modo da non dover qualificare l'uso di un tipo in tale spazio dei nomi:  
  
    ```c#  
    using System.Text;  
    ```  
  
-   Consentire l'accesso ai membri statici di un tipo senza dover qualificare l'accesso con il nome del tipo:  
  
    ```c#  
    using static System.Math;  
    ```  
  
-   Creare un alias per uno spazio dei nomi o un tipo.  Si tratta di una *direttiva alias using*.  
  
    ```c#  
    using Project = PC.MyCompany.Project;  
    ```  
  
 La parola chiave `using` viene usata anche per creare *istruzioni using*, che garantiscono che gli oggetti <xref:System.IDisposable>, ad esempio file e tipi di carattere, vengano gestiti correttamente.  Per altre informazioni, vedere [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md).  
  
## Tipo using static  
 È possibile accedere ai membri statici di un tipo senza dover qualificare l'accesso con il nome del tipo:  
  
```c#  
using static System.Console;   
using static System.Math;  
class Program   
{   
    static void Main()   
    {   
        WriteLine(Sqrt(3*3 + 4*4));   
    }   
}  
  
```  
  
 `Using static` importa solo i membri statici accessibili e i tipi annidati dichiarati nel tipo specificato.  I membri ereditati non vengono importati.  È possibile eseguire l'importazione da qualsiasi tipo denominato con una direttiva using static, inclusi i moduli Visual Basic.  Se nei metadati vengono visualizzate funzioni di primo livello F\# come membri statici di un tipo denominato il cui nome è un identificatore C\# valido, le funzioni F\# possono essere importate.  
  
 `Using static` crea metodi di estensione dichiarati nel tipo specificato disponibile per la ricerca del metodo di estensione.  Tuttavia, i nomi dei metodi di estensione non vengono importati nell'ambito del riferimento non qualificato nel codice.  
  
 I metodi con lo stesso nome importati da tipi diversi mediante direttive using static diverse nella stessa unità di compilazione o nello stesso spazio dei nomi costituiscono un gruppo di metodi.  La risoluzione dell'overload in questi gruppi di metodi segue le normali regole C\#.  
  
## Note  
 L'ambito di una direttiva `using` è limitato al file in cui viene visualizzata.  
  
 Creare un alias `using` per semplificare la qualifica di un identificatore in uno spazio dei nomi o un tipo.  La parte destra di una direttiva alias deve essere sempre un tipo completo indipendentemente dalle direttive using che lo precedono.  
  
 Creare una direttiva `using` per usare i tipi in uno spazio dei nomi senza dover specificare tale spazio dei nomi.  Una direttiva `using` non offre accesso ad alcuno spazio dei nomi annidato nello spazio dei nomi specificato.  
  
 Gli spazi dei nomi sono disponibili in due categorie: definiti dall'utente e definiti dal sistema.  Gli spazi dei nomi definiti dall'utente vengono definiti nel codice.  Per un elenco di spazi dei nomi definiti dal sistema, vedere [Libreria di classi di .NET Framework](http://go.microsoft.com/fwlink/?LinkID=227195).  
  
 Per esempi relativi a metodi di riferimento in altri assembly, vedere [Creazione e uso di DLL C\#](../Topic/How%20to:%20Create%20and%20Use%20Assemblies%20Using%20the%20Command%20Line%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Esempio 1  
  
### Descrizione  
 Nell'esempio seguente viene illustrato come definire e usare un alias `using` per uno spazio dei nomi.  
  
### Codice  
 [!code-cs[csrefKeywordsNamespace#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_1.cs)]  
  
### Commenti  
 Una direttiva alias using non può contenere un tipo generico aperto nella parte destra.  Ad esempio, non è possibile creare un alias using per List\<T\>, ma è possibile crearne uno per List\<int\>.  
  
## Esempio 2  
  
### Descrizione  
 Nell'esempio seguente viene illustrato come definire una direttiva `using` e un alias `using` per una classe:  
  
### Codice  
 [!code-cs[csrefKeywordsNamespace#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Utilizzo degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)   
 [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)