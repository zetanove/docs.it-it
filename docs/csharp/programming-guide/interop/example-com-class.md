---
title: Esempio di classe COM (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- examples [C#], COM classes
- COM, exposing Visual C# objects to
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2525d322bf3284c82356253d1383edbcd3928084
ms.lasthandoff: 03/13/2017

---
# <a name="example-com-class-c-programming-guide"></a>Esempio di classe COM (Guida per programmatori C#)
Di seguito è riportato un esempio di una classe esposta come oggetto COM. Dopo aver inserito questo codice in un file con estensione cs e averlo aggiunto al progetto, impostare la proprietà **Registra per interoperabilità COM** su **True**. Per altre informazioni, vedere [Procedura: registrare un componente per l'interoperabilità COM](http://msdn.microsoft.com/en-us/4de7d474-56e8-4027-994d-d47ca4725c5e).  
  
 Per esporre gli oggetti Visual C# a COM è necessario dichiarare un'interfaccia di classe e un'interfaccia di eventi, se necessaria, oltre alla classe stessa. Per essere visibili per COM i membri della classe devono rispettare le regole seguenti:  
  
-   La classe deve essere public.  
  
-   Le proprietà, i metodi e gli eventi devono essere public.  
  
-   Le proprietà e i metodi devono essere dichiarati nell'interfaccia di classe.  
  
-   Gli eventi devono essere dichiarati nell'interfaccia eventi.  
  
 Gli altri membri public della classe non dichiarati in queste interfacce non saranno visibili per COM ma lo saranno per altri oggetti di .NET Framework.  
  
 Per esporre le proprietà e i metodi a COM, è necessario dichiararli nell'interfaccia di classe e contrassegnarli con un attributo `DispId`, nonché implementarli nella classe stessa. L'ordine con cui i membri vengono dichiarati nell'interfaccia è quello usato per la vtable COM.  
  
 Per esporre gli eventi all'esterno della classe, è necessario dichiararli nell'interfaccia eventi e contrassegnarli con un attributo `DispId`. La classe non deve implementare questa interfaccia.  
  
 La classe implementa l'interfaccia di classe. È in grado di implementare più interfacce, ma la prima implementazione sarà quella dell'interfaccia di classe predefinita. A questo punto, implementare i metodi e le proprietà esposte a COM, che devono essere contrassegnati come public e corrispondere alle dichiarazioni presenti nell'interfaccia di classe. Dichiarare anche gli eventi generati dalla classe, che devono essere contrassegnati come public e corrispondere alle dichiarazioni presenti nell'interfaccia eventi.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideInterop#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/example-com-class_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Interoperabilità](../../../csharp/programming-guide/interop/index.md)   
 [Pagina Compilazione, Creazione progetti (C#)](https://docs.microsoft.com/visualstudio/ide/reference/build-page-project-designer-csharp)
