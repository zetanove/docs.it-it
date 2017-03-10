---
title: "Procedura: utilizzare propriet&#224; indicizzate nella programmazione dell&#39;interoperabilit&#224; COM (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "proprietà indicizzate [C#]"
  - "programmazione Office [C#, proprietà indicizzate"
  - "proprietà [C#], indicizzati"
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Procedura: utilizzare propriet&#224; indicizzate nella programmazione dell&#39;interoperabilit&#224; COM (Guida per programmatori C#)
Le *proprietà indicizzate* migliorano l'utilizzo delle proprietà COM dotate di parametri nella programmazione C\#.  Tali proprietà operano congiuntamente ad altre funzionalità introdotte in Visual C\# 2010, ad esempio gli [argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md), un nuovo tipo \([dynamic](../../../csharp/language-reference/keywords/dynamic.md)\) e le [informazioni sul tipo incorporate](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md) per migliorare la programmazione di Microsoft Office.  
  
 Nelle versioni precedenti di C\#, i metodi sono accessibili come proprietà solo se il metodo `get` non dispone di parametri e il metodo `set` dispone di un unico parametro di valore.  Non tutte le proprietà COM soddisfano tuttavia tali restrizioni.  Ad esempio, la proprietà [Range](http://go.microsoft.com/fwlink/?LinkId=166053) di Excel dispone di una funzione di accesso `get` che richiede un parametro per il nome dell'intervallo.  In passato, poiché non era possibile accedere direttamente alla proprietà `Range`, era necessario utilizzare il metodo `get_Range`, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideIndexedProperties#1](../../../csharp/programming-guide/interop/codesnippet/csharp/indexedpropscom/program.cs#1)]  
  
 Le proprietà indicizzate consentono invece di scrivere quanto segue:  
  
 [!code-cs[csProgGuideIndexedProperties#2](../../../csharp/programming-guide/interop/codesnippet/csharp/indexedpropscom/program.cs#2)]  
  
> [!NOTE]
>  Nell'esempio precedente viene inoltre utilizzata la funzionalità degli [argomenti facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md), introdotta in Visual C\# 2010, che consente di omettere `Type.Missing`.  
  
 In modo analogo, per impostare il valore della proprietà `Value` di un oggetto [Range](http://go.microsoft.com/fwlink/?LinkId=179211) in Visual C\# 2008 e versioni precedenti sono necessari due argomenti.  Uno fornisce un argomento per un parametro facoltativo che specifica il tipo del valore di intervallo.  L'altro fornisce il valore per la proprietà `Value`.  Prima di Visual C\# 2010, C\# consentiva un solo argomento.  Anziché utilizzare un metodo set normale, è necessario utilizzare il metodo `set_Value` o una proprietà diversa, [Value2](http://go.microsoft.com/fwlink/?LinkId=166050).  Queste tecniche vengono illustrate negli esempi riportati di seguito.  Entrambe impostano il valore della cella A1 su `Name`.  
  
 [!code-cs[csProgGuideIndexedProperties#3](../../../csharp/programming-guide/interop/codesnippet/csharp/indexedpropscom/program.cs#3)]  
  
 Le proprietà indicizzate consentono invece di scrivere il codice riportato di seguito.  
  
 [!code-cs[csProgGuideIndexedProperties#4](../../../csharp/programming-guide/interop/codesnippet/csharp/indexedpropscom/program.cs#4)]  
  
 Non è possibile creare proprietà indicizzate personalizzate.  La funzionalità supporta solo l'utilizzo di proprietà indicizzate esistenti.  
  
## Esempio  
 Nel codice seguente viene illustrato un esempio completo.  Per ulteriori informazioni sulla configurazione di un progetto che accede all'API di Office, vedere [Procedura: accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C\#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md).  
  
 [!code-cs[csProgGuideIndexedProperties#5](../../../csharp/programming-guide/interop/codesnippet/csharp/indexedpropscom/program.cs#5)]  
  
## Vedere anche  
 [Argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Utilizzo del tipo dinamico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Procedura: utilizzare argomenti denominati e facoltativi nella programmazione di Office](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [Procedura: accedere agli oggetti di interoperabilità di Office usando le funzionalità di Visual C\#](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)   
 [Procedura dettagliata: programmazione di Office](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)