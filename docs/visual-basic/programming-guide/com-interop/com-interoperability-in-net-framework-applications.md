---
title: "COM Interoperability in .NET Framework Applications (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "interoperability, COM and .NET framework objects"
  - "COM interop"
  - "shared components"
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# COM Interoperability in .NET Framework Applications (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando si desidera utilizzare oggetti COM e .NET Framework all'interno della stessa applicazione, è necessario esaminare le differenze relative alla modalità di conservazione in memoria degli oggetti.  Gli oggetti .NET Framework si trovano nella memoria gestita, ovvero la memoria controllata da Common Language Runtime, e possono essere spostati dal runtime in base alle necessità.  Gli oggetti COM si trovano nella memoria non gestita e non ne è previsto lo spostamento in altre posizioni di memoria.  In [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] e [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] sono disponibili strumenti che consentono di controllare l'interazione di questi componenti gestiti e non gestiti.  Per ulteriori informazioni sul codice gestito, vedere [Common Language Runtime](../Topic/Common%20Language%20Runtime%20\(CLR\).md).  
  
 Oltre a utilizzare oggetti COM nelle applicazioni.NET, è anche possibile utilizzare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per sviluppare oggetti cui sia possibile accedere dal codice non gestito tramite COM.  
  
 I collegamenti presenti in questa pagina forniscono dettagli sulle interazioni tra gli oggetti COM e .NET Framework.  
  
## Sezioni correlate  
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)  
 Vengono forniti collegamenti agli argomenti in cui viene illustrata l'interoperabilità COM in Visual Basic, inclusi oggetti COM, controlli ActiveX, DLL Win32, oggetti gestiti ed ereditarietà di oggetti COM.  
  
 [COM Interop Wrapper Error](/visual-cpp/misc/com-interop-wrapper-error)  
 Vengono descritte le conseguenze e le opzioni disponibili nel caso in cui il sistema del progetto non sia in grado di creare un wrapper di interoperabilità COM per un componente specifico.  
  
 [Interoperating with Unmanaged Code](../Topic/Interoperating%20with%20Unmanaged%20Code.md)  
 Viene fornita una breve descrizione di alcuni problemi di interazione tra codice gestito e non gestito e vengono forniti collegamenti a ulteriori informazioni.  
  
 [COM Wrappers](../Topic/COM%20Wrappers.md)  
 Vengono illustrati i wrapper richiamabili tramite runtime, mediante i quali è possibile chiamare i metodi COM dal codice gestito, e i wrapper richiamabili tramite COM, che consentono ai client COM di chiamare i metodi di oggetti .NET.  
  
 [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 Vengono forniti collegamenti agli argomenti in cui viene illustrata l'interoperabilità COM relativamente a wrapper, eccezioni, ereditarietà, threading, eventi, conversioni e marshalling.  
  
 [Tlbimp.exe \(Type Library Importer\)](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)  
 Viene illustrato lo strumento che è possibile utilizzare per convertire le definizioni dei tipi presenti all'interno di una libreria di tipi COM in definizioni equivalenti in un assembly di Common Language Runtime.