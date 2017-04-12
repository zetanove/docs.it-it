---
title: Reflection (Visual Basic) | Documenti di Microsoft
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
ms.assetid: d991bc0f-d16a-4ac5-9351-70e5c5b9891b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3ae042933575849e105d7b681634a61319c1d6ee
ms.lasthandoff: 03/13/2017

---
# <a name="reflection-visual-basic"></a>Reflection (Visual Basic)
La reflection fornisce oggetti (di tipo <xref:System.Type>) che descrivono gli assembly, moduli e tipi.</xref:System.Type> È possibile utilizzare la reflection per creare un'istanza di un tipo, associare il tipo a un oggetto esistente, o ottenere il tipo da un oggetto esistente e richiamarne i metodi o dinamicamente accedere ai relativi campi e proprietà. Se si utilizza gli attributi nel codice, la reflection consente di accedervi. Per ulteriori informazioni, vedere [attributi](https://msdn.microsoft.com/library/5x6cd29c).  
  
 Di seguito è riportato un esempio semplice di reflection che utilizza il metodo statico `GetType` , ereditato da tutti i tipi del `Object` - classe per ottenere il tipo di una variabile di base:  
  
```vb  
' Using GetType to obtain type information:  
Dim i As Integer = 42  
Dim type As System.Type = i.GetType()  
System.Console.WriteLine(type)  
```  
  
 L'output è:  
  
 `System.Int32`  
  
 Nell'esempio seguente utilizza la reflection per ottenere il nome completo dell'assembly caricato.  
  
```vb  
' Using Reflection to get information from an Assembly:  
Dim info As System.Reflection.Assembly = GetType(System.Int32).Assembly  
System.Console.WriteLine(info)  
```  
  
 L'output è:  
  
 `mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
## <a name="reflection-overview"></a>Cenni preliminari sulla reflection  
 Reflection è utile nelle situazioni seguenti:  
  
-   Quando è necessario accedere agli attributi nei metadati del programma. Per ulteriori informazioni, vedere [il recupero di informazioni memorizzate negli attributi](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c).  
  
-   Per esaminare e creare istanze di tipi in un assembly.  
  
-   Per la creazione di nuovi tipi in fase di esecuzione. Utilizzare le classi in <xref:System.Reflection.Emit>.</xref:System.Reflection.Emit>  
  
-   Per eseguire l'associazione tardiva, accedere ai metodi su tipi creati in fase di esecuzione. Vedere l'argomento [dinamicamente durante il caricamento e utilizzo dei tipi](http://msdn.microsoft.com/library/db985bec-5942-40ec-b13a-771ae98623dc).  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Reflection](http://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775)  
  
-   [Visualizzazione delle informazioni sul tipo](http://msdn.microsoft.com/library/7e7303a9-4064-4738-b4e7-b75974ed70d2)  
  
-   [Reflection e tipi generici](http://msdn.microsoft.com/library/f7180fc5-dd41-42d4-8a8e-1b34288e06de)  
  
-   <xref:System.Reflection.Emit></xref:System.Reflection.Emit>  
  
-   [Recupero di informazioni memorizzate negli attributi](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori Visual Basic](../../../visual-basic/programming-guide/index.md)   
 [Assembly in Common Language Runtime](https://msdn.microsoft.com/library/k3677y81)
