---
title: "Procedura: identificare un tipo nullable (Guida per programmatori C#) | Microsoft Docs"
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
  - "nullable (tipi) [C#], identificazione"
ms.assetid: d4b67ee2-66e8-40c1-ae9d-545d32c71387
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: identificare un tipo nullable (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare l'operatore [typeof](../../../csharp/language-reference/keywords/typeof.md) di C\# per creare un oggetto <xref:System.Type> che rappresenta un tipo nullable:  
  
```  
System.Type type = typeof(int?);  
```  
  
 È inoltre possibile utilizzare le classi e i metodi dello spazio dei nomi <xref:System.Reflection> per generare gli oggetti <xref:System.Type> che rappresentano tipi nullable.  Tuttavia, se si tenta di ottenere informazioni sul tipo dalle variabili nullable in fase di esecuzione tramite il metodo <xref:System.Object.GetType%2A> o l'operatore `is`, il risultato è un oggetto <xref:System.Type> che rappresenta il tipo sottostante, non il tipo nullable.  
  
 La chiamata di `GetType` in un tipo nullable causa la conversione boxing quando il tipo viene convertito in modo implicito in <xref:System.Object>.  Pertanto, <xref:System.Object.GetType%2A> restituisce sempre un oggetto <xref:System.Type> che rappresenta il tipo sottostante e non il tipo nullable.  
  
```  
int? i = 5;  
Type t = i.GetType();  
Console.WriteLine(t.FullName); //"System.Int32"  
```  
  
 L'operatore [is](../../../csharp/language-reference/keywords/is.md) di C\# agisce anche nel tipo sottostante di un tipo nullable.  Non è pertanto possibile utilizzare `is` per determinare se una variabile è di tipo nullable.  Nell'esempio seguente viene illustrato come l'operatore `is` consideri una variabile \<int\> nullable come int.  
  
```  
static void Main(string[] args)  
{  
  int? i = 5;  
  if (i is int) // true  
    //…  
}  
```  
  
## Esempio  
 Utilizzare il codice seguente per determinare se un oggetto <xref:System.Type> rappresenta un tipo nullable.  Si tenga presente che questo codice restituisce sempre false se l'oggetto `Type` è stato restituito da una chiamata a <xref:System.Object.GetType%2A>, come illustrato in precedenza in questo argomento.  
  
```  
if (type.IsGenericType && type.GetGenericTypeDefinition() == typeof(Nullable<>)) {…}  
```  
  
## Vedere anche  
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Conversione boxing dei tipi nullable](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)