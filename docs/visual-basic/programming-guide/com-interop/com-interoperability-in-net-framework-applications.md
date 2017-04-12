---
title: "Interoperabilità COM nelle applicazioni .NET Framework (Visual Basic) | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- interoperability, COM and .NET framework objects
- COM interop
- shared components
ms.assetid: f5a72143-c268-4dff-a019-974ad940e17d
caps.latest.revision: 15
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 308ee8e495efa9368ef55d781f6b6dc314db51ac
ms.lasthandoff: 03/13/2017

---
# <a name="com-interoperability-in-net-framework-applications-visual-basic"></a>Interoperabilità COM nelle applicazioni .NET Framework (Visual Basic)
Quando si desidera utilizzare oggetti COM e .NET Framework nella stessa applicazione, è necessario risolvere le differenze nella modalità con cui gli oggetti presenti in memoria. Un oggetto .NET Framework si trova nella memoria gestita, la memoria controllata da common language runtime e possono essere spostati dal runtime in base alle esigenze. Un oggetto COM si trova nella memoria non gestita e non è previsto per spostare in un'altra posizione di memoria. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]e [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] forniscono strumenti per controllare l'interazione tra le gestite e i componenti. Per ulteriori informazioni sul codice gestito, vedere [Common Language Runtime](http://msdn.microsoft.com/library/059a624e-f7db-4134-ba9f-08b676050482).  
  
 Oltre a utilizzare oggetti COM nelle applicazioni .NET, è inoltre consiglia di utilizzare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per sviluppare oggetti accessibili dal codice non gestito tramite COM.  
  
 I collegamenti in questa pagina forniscono dettagli sulle interazioni tra gli oggetti COM e .NET Framework.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Interoperabilità COM](../../../visual-basic/programming-guide/com-interop/index.md)  
 Vengono forniti collegamenti ad argomenti che illustrano l'interoperabilità COM in Visual Basic, inclusi gli oggetti COM, controlli ActiveX, DLL Win32, gli oggetti gestiti ed ereditarietà degli oggetti COM.  
  
 [Errore del wrapper di interoperabilità COM](https://docs.microsoft.com/cpp/misc/com-interop-wrapper-error)  
 Descrive le conseguenze e le opzioni se il sistema di progetto non può creare un wrapper di interoperabilità COM per un particolare componente.  
  
 [Interoperabilità con codice non gestito](https://msdn.microsoft.com/library/sd10k43k)  
 Descrive brevemente alcuni dei problemi di interazione tra codice gestito e e vengono forniti collegamenti per approfondire l'argomento.  
  
 [Wrapper COM](http://msdn.microsoft.com/library/e56c485b-6b67-4345-8e66-fd21835a6092)  
 Vengono illustrati i runtime callable wrapper, che consentono al codice gestito chiamare i metodi COM, e COM callable wrapper, che consentono ai client COM di chiamare metodi oggetto .NET.  
  
 [Interoperabilità COM avanzata](http://msdn.microsoft.com/en-us/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 Vengono forniti collegamenti ad argomenti che illustrano l'interoperabilità COM per quanto riguarda i wrapper, eccezioni, ereditarietà, threading, eventi, conversioni e marshalling.  
  
 [Tlbimp.exe (Type Library Importer)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)  
 Viene descritto lo strumento che è possibile utilizzare per convertire le definizioni dei tipi presenti in una libreria dei tipi COM nelle definizioni equivalenti in un assembly di common language runtime.
