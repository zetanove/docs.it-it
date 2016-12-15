---
title: "Esempio di classe COM (Guida per programmatori C#) | Microsoft Docs"
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
  - "COM, esposizione di oggetti Visual C# in"
  - "esempi [C#], classi COM"
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Esempio di classe COM (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Di seguito è riportato un esempio di una classe esposta come oggetto COM.  Dopo aver inserito questo codice in un file CS e averlo aggiunto al progetto, impostare la proprietà **Registra per interoperabilità COM** su **True**.  Per ulteriori informazioni, vedere [NIB: How to: Register a Component for COM Interop](http://msdn.microsoft.com/it-it/4de7d474-56e8-4027-994d-d47ca4725c5e).  
  
 Per esporre gli oggetti Visual C\# a COM, è necessario dichiarare un'interfaccia di classe, un'interfaccia di eventi se richiesta, nonché la classe stessa.  Per essere visibili a COM è necessario che i membri di classe rispettino le seguenti regole:  
  
-   La classe deve essere pubblica.  
  
-   Le proprietà, i metodi e gli eventi devono essere pubblici.  
  
-   Le proprietà e i metodi devono essere dichiarati nell'interfaccia di classe.  
  
-   Gli eventi devono essere dichiarati nella relativa interfaccia.  
  
 Gli altri membri pubblici della classe non dichiarati in queste interfacce non saranno visibili a COM, ma ad altri oggetti di .NET Framework.  
  
 Per esporre le proprietà e i metodi a COM, è necessario dichiararli nell'interfaccia di classe e contrassegnarli con un attributo `DispId`, nonché implementarli nella classe stessa.  L'ordine con cui i membri vengono dichiarati nell'interfaccia è quello utilizzato per la vtable COM.  
  
 Per esporre gli eventi dalla classe, è necessario dichiararli nell'interfaccia degli eventi e contrassegnarli con un attributo `DispId`.  È opportuno che la classe non implementi questa interfaccia.  
  
 È invece necessario che la classe implementi l'interfaccia di classe. La classe è in grado di implementare più di un'interfaccia, ma la prima implementazione sarà quella dell'interfaccia di classe predefinita.  Implementare i metodi e le proprietà esposte a COM,  che devono essere contrassegnati come pubblici e corrispondere alle dichiarazioni presenti nell'interfaccia della classe.  Dichiarare, inoltre, gli eventi originati dalla classe,  che devono a loro volta essere contrassegnati come pubblici e corrispondere alle dichiarazioni presenti nell'interfaccia degli eventi.  
  
## Esempio  
 [!code-cs[csProgGuideInterop#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/example-com-class_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Interoperabilità](../../../csharp/programming-guide/interop/interoperability.md)   
 [Pagina Compilazione, Progettazione progetti \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp)