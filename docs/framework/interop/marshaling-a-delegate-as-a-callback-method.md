---
title: "Marshaling a Delegate as a Callback Method | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "data marshaling, Callback sample"
  - "marshaling, Callback sample"
ms.assetid: 6ddd7866-9804-4571-84de-83f5cc017a5a
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Marshaling a Delegate as a Callback Method
In questo esempio viene dimostrato come passare i delegati a una funzione non gestita per la quale sono previsti puntatori a funzione.  Un delegato è una classe che può contenere un riferimento a un metodo ed è equivalente a un puntatore a funzione indipendente dai tipi o a una funzione callback.  
  
> [!NOTE]
>  Quando si utilizza un delegato in una chiamata, Common Language Runtime consente di proteggerlo dalla procedura di Garbage Collection per la durata di tale chiamata.  Se tuttavia il delegato viene memorizzato dalla funzione non gestita per essere utilizzato al termine della chiamata, è necessario evitare manualmente l'operazione di Garbage Collection finché la funzione non gestita non termina l'uso del delegato.  Per ulteriori informazioni, vedere [Esempio di HandleRef](http://msdn.microsoft.com/it-it/ab23b04e-1d53-4ec7-b27a-e892d9298959) ed [Esempio di GCHandle](http://msdn.microsoft.com/it-it/6acce798-0385-4ded-a790-77da842c113f).  
  
 Nell'esempio di callback vengono utilizzate le seguenti funzioni non gestite, illustrate con la dichiarazione di funzione originale:  
  
-   **TestCallBack** esportata da PinvokeLib.dll.  
  
    ```  
    void TestCallBack(FPTR pf, int value);  
    ```  
  
-   **TestCallBack2** esportata da PinvokeLib.dll.  
  
    ```  
    void TestCallBack2(FPTR2 pf2, char* value);  
    ```  
  
 [PinvokeLib.dll](http://msdn.microsoft.com/it-it/5d1438d7-9946-489d-8ede-6c694a08f614) è una libreria non gestita personalizzata contenente un'implementazione per le funzioni elencate in precedenza.  
  
 In questo esempio, la classe `LibWrap` contiene i prototipi gestiti per i metodi `TestCallBack` e `TestCallBack2`.  Entrambi i metodi passano un delegato a una funzione di callback come parametro.  La firma del delegato deve corrispondere a quella del metodo a cui fa riferimento.  I delegati `FPtr` e `FPtr2` ad esempio hanno firme identiche ai metodi `DoSomething` e `DoSomething2`.  
  
## Dichiarazione dei prototipi  
 [!code-cpp[Conceptual.Interop.Marshaling#37](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/callback.cpp#37)]
 [!code-csharp[Conceptual.Interop.Marshaling#37](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/callback.cs#37)]
 [!code-vb[Conceptual.Interop.Marshaling#37](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/callback.vb#37)]  
  
## Chiamata delle funzioni  
 [!code-cpp[Conceptual.Interop.Marshaling#38](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interop.marshaling/cpp/callback.cpp#38)]
 [!code-csharp[Conceptual.Interop.Marshaling#38](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/callback.cs#38)]
 [!code-vb[Conceptual.Interop.Marshaling#38](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/callback.vb#38)]  
  
## Vedere anche  
 [Miscellaneous Marshaling Samples](http://msdn.microsoft.com/it-it/a915c948-54e9-4d0f-a525-95a77fd8ed70)   
 [Platform Invoke Data Types](http://msdn.microsoft.com/it-it/16014d9f-d6bd-481e-83f0-df11377c550f)   
 [Creating Prototypes in Managed Code](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)