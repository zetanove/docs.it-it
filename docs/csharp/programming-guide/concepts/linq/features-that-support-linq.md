---
title: "C# Features That Support LINQ | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "LINQ [C#], features supporting LINQ"
ms.assetid: 524b0078-ebfd-45a7-b390-f2ceb9d84797
caps.latest.revision: 23
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# C# Features That Support LINQ
Nella sezione seguente vengono illustrati i nuovi costrutti di linguaggio introdotti in C\# 3.0.  Sebbene queste nuove funzionalità vengano tutte utilizzate con le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)], non sono limitate a [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] e possono essere utilizzate in qualsiasi contesto in cui risultino utili.  
  
## Espressioni di query  
 Le espressioni di query utilizzano una sintassi dichiarativa simile a SQL o XQuery per eseguire una query sulle raccolte IEnumerable.  In fase di compilazione la sintassi della query viene convertita nelle chiamate al metodo per l'implementazione di un provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] dei metodi di estensione degli operatori di query standard.  Le applicazioni controllano gli operatori di query standard inclusi nell'ambito specificando lo spazio dei nomi adatto con una direttiva `using`.  Nell'espressione di query seguente viene utilizzata una matrice di stringhe, raggruppate in base al primo carattere della stringa, e vengono ordinati i gruppi.  
  
```  
var query = from str in stringArray  
            group str by str[0] into stringGroup  
            orderby stringGroup.Key  
            select stringGroup;  
```  
  
 Per ulteriori informazioni, vedere [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md).  
  
## Variabili tipizzate in modo implicito \(var\)  
 Anziché specificare in modo esplicito un tipo quando si dichiara e inizializza una variabile, è possibile utilizzare il modificatore [var](../../../../csharp/language-reference/keywords/var.md) per indicare al compilatore di dedurre e assegnare il tipo, come illustrato di seguito:  
  
```  
var number = 5;  
var name = "Virginia";  
var query = from str in stringArray  
            where str[0] == 'm'  
            select str;  
```  
  
 Le variabili dichiarate come `var` sono fortemente tipizzate esattamente come le variabili in cui il tipo viene specificato in modo esplicito.  L'utilizzo di `var` consente di creare tipi anonimi, ma può essere utilizzato per qualsiasi variabile locale.  Le matrici possono essere dichiarate anche con la tipizzazione implicita.  
  
 Per ulteriori informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## Inizializzatori di oggetto e di raccolta  
 Gli inizializzatori di oggetto e di raccolta consentono di inizializzare gli oggetti senza chiamare in modo esplicito un costruttore per l'oggetto.  Gli inizializzatori vengono utilizzati in genere nelle espressioni di query quando proiettano i dati di origine in un nuovo tipo di dati.  Supponendo di utilizzare una classe denominata `Customer` con le proprietà pubbliche `Name` e `Phone`, l'inizializzatore di oggetto può essere utilizzato come nel codice seguente:  
  
```  
Customer cust = new Customer { Name = "Mike", Phone = "555-1212" };  
```  
  
 Per ulteriori informazioni, vedere [Inizializzatori di oggetto e di raccolta](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
## Tipi anonimi  
 Un tipo anonimo viene costruito dal compilatore e il nome del tipo è disponibile solo al compilatore.  I tipi anonimi costituiscono una valida soluzione per raggruppare temporaneamente un insieme di proprietà nel risultato di una query senza dovere definire un tipo denominato separato.  I tipi anonimi vengono inizializzati con una nuova espressione e un inizializzatore di oggetto, come illustrato di seguito:  
  
```  
select new {name = cust.Name, phone = cust.Phone};  
```  
  
 Per ulteriori informazioni, vedere [Tipi anonimi](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
## Metodi di estensione  
 Un metodo di estensione è un metodo statico che può essere associato a un tipo, in modo da poter essere chiamato come se fosse un metodo di istanza sul tipo.  Questa funzionalità consente in pratica di "aggiungere" nuovi metodi ai tipi esistenti senza doverli effettivamente modificare.  Gli operatori di query standard costituiscono un set di metodi di estensione che forniscono funzionalità di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] per qualsiasi tipo che implementi <xref:System.Collections.Generic.IEnumerable%601>.  
  
 Per ulteriori informazioni, vedere [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  
  
## Espressioni lambda  
 Un'espressione lambda è una funzione inline che utilizza l'operatore \=\> per separare i parametri di input dal corpo della funzione e, in fase di compilazione, può essere convertita in un delegato o in una struttura ad albero dell'espressione.  Nella programmazione [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] le espressioni lambda vengono utilizzate quando si effettuano chiamate al metodo dirette agli operatori di query standard.  
  
 Per ulteriori informazioni, vedere:  
  
-   [Funzioni anonime](../../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)  
  
-   [Espressioni lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
  
-   [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)  
  
## Proprietà implementate automaticamente  
 Le proprietà implementate automaticamente rendono la dichiarazione di proprietà più concisa.  Quando si dichiara una proprietà come illustrato nell'esempio seguente, il compilatore creerà un campo di supporto anonimo privato accessibile esclusivamente tramite il metodo get e set della proprietà.  
  
```  
public string Name {get; set;}  
```  
  
 Per ulteriori informazioni, vedere [Proprietà implementate automaticamente](../../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).  
  
## Vedere anche  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Visual Basic Features That Support LINQ](../../../../visual-basic/programming-guide/concepts/linq/features-that-support-linq.md)