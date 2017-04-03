---
title: "Funzionalità di C# che supportano LINQ | Documentazione Microsoft"
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
helpviewer_keywords:
- LINQ [C#], features supporting LINQ
ms.assetid: 524b0078-ebfd-45a7-b390-f2ceb9d84797
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f844e967e2abb7ea23e04a797017261e33bb4d75
ms.lasthandoff: 03/13/2017

---
# <a name="c-features-that-support-linq"></a>Funzionalità di C# che supportano LINQ
Nella sezione seguente vengono illustrati i nuovi costrutti di linguaggio introdotti in C# 3.0. Sebbene queste nuove funzionalità vengano tutte usate con le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], non sono limitate a [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] e possono essere usate in qualsiasi contesto in cui risultino utili.  
  
## <a name="query-expressions"></a>Espressioni di query  
 Le espressioni di query usano una sintassi dichiarativa simile a SQL o XQuery per eseguire una query sulle Collection IEnumerable. In fase di compilazione la sintassi della query viene convertita nelle chiamate al metodo per l'implementazione di un provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] dei metodi di estensione degli operatori di query standard. Le applicazioni controllano gli operatori di query standard inclusi nell'ambito specificando lo spazio dei nomi adatto con una direttiva `using`. Nell'espressione di query seguente viene usata una matrice di stringhe, raggruppate in base al primo carattere della stringa, e vengono ordinati i gruppi.  
  
```  
var query = from str in stringArray  
            group str by str[0] into stringGroup  
            orderby stringGroup.Key  
            select stringGroup;  
```  
  
 Per altre informazioni, vedere [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md).  
  
## <a name="implicitly-typed-variables-var"></a>Variabili tipizzate in modo implicito (var)  
 Anziché specificare in modo esplicito un tipo quando si dichiara e inizializza una variabile, è possibile usare il modificatore [var](../../../../csharp/language-reference/keywords/var.md) per indicare al compilatore di dedurre e assegnare il tipo, come illustrato di seguito:  
  
```  
var number = 5;  
var name = "Virginia";  
var query = from str in stringArray  
            where str[0] == 'm'  
            select str;  
```  
  
 Le variabili dichiarate come `var` sono fortemente tipizzate esattamente come le variabili in cui il tipo viene specificato in modo esplicito. L'uso di `var` consente di creare tipi anonimi, ma può essere usato per qualsiasi variabile locale. Le matrici possono essere dichiarate anche con la tipizzazione implicita.  
  
 Per altre informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## <a name="object-and-collection-initializers"></a>Inizializzatori di oggetto e di raccolta  
 Gli inizializzatori di oggetti e Collection consentono di inizializzare gli oggetti senza chiamare in modo esplicito un costruttore per l'oggetto. Gli inizializzatori vengono usati in genere nelle espressioni di query quando proiettano i dati di origine in un nuovo tipo di dati. Supponendo di usare una classe denominata `Customer` con le proprietà pubbliche `Name` e `Phone`, l'inizializzatore di oggetto può essere usato come nel codice seguente:  
  
```  
Customer cust = new Customer { Name = "Mike", Phone = "555-1212" };  
```  
  
 Per altre informazioni, vedere [Inizializzatori di oggetto e di Collection](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
## <a name="anonymous-types"></a>Tipi anonimi  
 Un tipo anonimo viene costruito dal compilatore e il nome del tipo è disponibile solo al compilatore. I tipi anonimi costituiscono una valida soluzione per raggruppare temporaneamente un set di proprietà nel risultato di una query senza dovere definire un tipo denominato separato. I tipi anonimi vengono inizializzati con una nuova espressione e un inizializzatore di oggetto, come illustrato di seguito:  
  
```  
select new {name = cust.Name, phone = cust.Phone};  
```  
  
 Per altre informazioni, vedere [Tipi anonimi](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
## <a name="extension-methods"></a>Metodi di estensione  
 Un metodo di estensione è un metodo statico che può essere associato a un tipo, in modo da poter essere chiamato come se fosse un metodo di istanza sul tipo. Questa funzionalità consente in pratica di "aggiungere" nuovi metodi ai tipi esistenti senza doverli effettivamente modificare. Gli operatori query standard sono un set di metodi di estensione che forniscono funzionalità di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per qualsiasi tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>.  
  
 Per altre informazioni, vedere [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  
  
## <a name="lambda-expressions"></a>Espressioni lambda  
 Un'espressione lambda è una funzione inline che usa l'operatore => per separare i parametri di input dal corpo della funzione e, in fase di compilazione, può essere convertita in un delegato o in un albero delle espressioni. Nella programmazione [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] le espressioni lambda vengono usate quando si effettuano chiamate al metodo dirette agli operatori di query standard.  
  
 Per altre informazioni, vedere:  
  
-   [Funzioni anonime](../../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)  
  
-   [Espressioni lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
  
-   [Alberi delle espressioni (C#)](../../../../csharp/programming-guide/concepts/expression-trees/index.md)  
  
## <a name="auto-implemented-properties"></a>Proprietà implementate automaticamente  
 Le proprietà implementate automaticamente rendono più concisa la dichiarazione di proprietà. Quando si dichiara una proprietà come mostrato nel seguente esempio, il compilatore crea un campo sottostante privato anonimo accessibile solo tramite la propertà getter e setter.  
  
```  
public string Name {get; set;}  
```  
  
 Per altre informazioni, vedere [Proprietà implementate automaticamente](../../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Language-Integrated Query (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)
