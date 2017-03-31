---
title: Reflection (C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: f80a2362-953b-4e8e-9759-cd5f334190d4
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ab40ab2258703670576084eccf7fd7e1b113d08d
ms.lasthandoff: 03/13/2017

---
# <a name="reflection-c"></a>Reflection (C#)
La reflection specifica oggetti di tipo <xref:System.Type>, che descrivono assembly, moduli e tipi. È possibile usare la reflection per creare in modo dinamico un'istanza di un tipo, associare il tipo a un oggetto esistente oppure ottenere il tipo da un oggetto esistente e richiamarne i metodi o accedere ai relativi campi e proprietà. Se si usano attributi nel codice, la reflection consente di accedervi. Per altre informazioni, vedere [Attributi](https://msdn.microsoft.com/library/5x6cd29c).  
  
 Di seguito è riportato un esempio semplice di reflection che usa il metodo statico `GetType` ereditato da tutti i tipi dalla classe di base `Object` per ottenere il tipo di una variabile:  
  
```csharp  
// Using GetType to obtain type information:  
int i = 42;  
System.Type type = i.GetType();  
System.Console.WriteLine(type);  
```  
  
 L'output è:  
  
 `System.Int32`  
  
 L'esempio seguente usa la reflection per ottenere il nome completo dell'assembly caricato.  
  
```csharp  
// Using Reflection to get information from an Assembly:  
System.Reflection.Assembly info = typeof(System.Int32).Assembly;  
System.Console.WriteLine(info);  
```  
  
 L'output è:  
  
 `mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
> [!NOTE]
>  Le parole chiave di C# `protected` e `internal` non hanno significato in IL e non sono usate nelle API di reflection. I termini corrispondenti in IL sono *Famiglia* e *Assembly*. Per identificare un metodo `internal` con la reflection, usare la proprietà <xref:System.Reflection.MethodBase.IsAssembly%2A>. Per identificare un metodo `protected internal`, usare <xref:System.Reflection.MethodBase.IsFamilyOrAssembly%2A>.  
  
## <a name="reflection-overview"></a>Panoramica della reflection  
 La reflection è utile nelle situazioni seguenti:  
  
-   Quando è necessario accedere agli attributi nei metadati del programma. Per altre informazioni, vedere [Recupero di informazioni memorizzate negli attributi](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c).  
  
-   Per esaminare e creare istanze di tipi in un assembly.  
  
-   Per creare nuovi tipi in fase di esecuzione. Usare le classi in <xref:System.Reflection.Emit>.  
  
-   Per eseguire l'associazione tardiva, accedere ai metodi per i tipi creati in fase di esecuzione. Vedere l'argomento relativo a [caricamento e uso dinamico dei tipi](http://msdn.microsoft.com/library/db985bec-5942-40ec-b13a-771ae98623dc).  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Reflection](http://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775)  
  
-   [Visualizzazione delle informazioni sul tipo](http://msdn.microsoft.com/library/7e7303a9-4064-4738-b4e7-b75974ed70d2)  
  
-   [Reflection e tipi generici](http://msdn.microsoft.com/library/f7180fc5-dd41-42d4-8a8e-1b34288e06de)  
  
-   <xref:System.Reflection.Emit>  
  
-   [Recupero di informazioni memorizzate negli attributi](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Assembly in Common Language Runtime](https://msdn.microsoft.com/library/k3677y81)
