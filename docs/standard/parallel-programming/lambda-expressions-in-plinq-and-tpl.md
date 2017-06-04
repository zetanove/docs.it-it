---
title: "Lambda Expressions in PLINQ and TPL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Func delegate, creating with lambda expression"
  - "Action delegate, creating with lambda expression"
  - "lambda expressions, with Action and Func"
ms.assetid: 645b2c17-29d0-4ffa-8684-430743cc2f2d
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Lambda Expressions in PLINQ and TPL
La libreria Task Parallel Library \(TPL\) contiene molti metodi che accettano come parametri di input una delle famiglie di delegati <xref:System.Func%601?displayProperty=fullName> o <xref:System.Action?displayProperty=fullName>.  Questi delegati vengono utilizzati per passare la logica di programma personalizzata al ciclo, all'attività o alla query parallela.  Negli esempi di codice per TPL e PLINQ si utilizzano espressioni lambda per creare istanze di tali delegati come blocchi di codice inline.  In questo argomento viene fornita una breve introduzione ai delegati Func e Action e viene illustrato come utilizzare le espressioni lambda in TPL e PLINQ.  
  
 **Nota** Per ulteriori informazioni sui delegati in generale, vedere [Delegati](../Topic/Delegates%20\(C%23%20Programming%20Guide\).md) e [Delegates](../Topic/Delegates%20\(Visual%20Basic\).md).  Per ulteriori informazioni sulle espressioni lambda in C\# e [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], vedere [Espressioni lambda](../Topic/Lambda%20Expressions%20\(C%23%20Programming%20Guide\).md) e [Lambda Expressions](../Topic/Lambda%20Expressions%20\(Visual%20Basic\).md).  
  
## Delegato Func  
 Un delegato `Func` incapsula un metodo che restituisce un valore.  In una firma Func, l'ultimo parametro di tipo o quello più a destra specifica sempre il tipo restituito.  Una causa comune degli errori del compilatore è dovuta al tentativo di passare due parametri di input a <xref:System.Func%602?displayProperty=fullName>, poiché in effetti questo tipo accetta un solo parametro di input.  Nella libreria di classi .NET Framework sono definite 17 versioni di `Func`: <xref:System.Func%601?displayProperty=fullName>, <xref:System.Func%602?displayProperty=fullName>, <xref:System.Func%603?displayProperty=fullName> e così via fino a <xref:System.Func%6017?displayProperty=fullName>.  
  
## Delegato Action  
 Un delegato <xref:System.Action?displayProperty=fullName> incapsula un metodo \(Sub in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) che non restituisce valori oppure restituisce [void](../Topic/void%20\(C%23%20Reference\).md).  In una firma di tipo Action i parametri di tipo rappresentano solo parametri di input.  Analogamente a Func, nella libreria di classi .NET Framework sono definite 17 versioni di Action, da una versione priva di parametri di tipo fino a una versione avente 16 parametri di tipo.  
  
## Esempio  
 Nell'esempio seguente per il metodo <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=fullName> viene illustrato come esprimere i delegati Func e Action utilizzando espressioni lambda.  
  
 [!code-csharp[System.Threading.Tasks.Parallel#02](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.threading.tasks.parallel/cs/parallelforeach.cs#02)]
 [!code-vb[System.Threading.Tasks.Parallel#02](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.threading.tasks.parallel/vb/parallelforeach.vb#02)]  
  
## Vedere anche  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)