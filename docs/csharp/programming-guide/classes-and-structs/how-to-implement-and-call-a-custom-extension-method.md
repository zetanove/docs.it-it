---
title: 'Procedura: Implementare e chiamare un metodo di estensione personalizzato (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- extension methods [C#], implementing and calling
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
caps.latest.revision: 15
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
ms.openlocfilehash: 9ba08e55e3bc07c2ce6369e2b33ccbe632545d24
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a>Procedura: implementare e chiamare un metodo di estensione personalizzato (Guida per programmatori C#)
In questo argomento viene illustrato come implementare i propri metodi di estensione per qualsiasi tipo all'interno della [libreria di classi .NET Framework](http://go.microsoft.com/fwlink/?LinkID=217856), o per qualsiasi altro tipo .NET che si voglia estendere. Il codice client può usare i metodi di estensione aggiungendo un riferimento alla DLL che li contiene, e aggiungendo una direttiva [using](../../../csharp/language-reference/keywords/using-directive.md) che specifica lo spazio dei nomi in cui vengono definiti i metodi di estensione.  
  
## <a name="to-define-and-call-the-extension-method"></a>Per definire e chiamare il metodo di estensione  
  
1.  Definire una [classe](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md) statica per contenere il metodo di estensione.  
  
     La classe deve essere visibile al codice client. Per altre informazioni sulle regole di accessibilità, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
2.  Implementare il metodo di estensione come metodo statico con almeno la stessa visibilità della classe che lo contiene.  
  
3.  Il primo parametro del metodo specifica il tipo su cui il metodo opera e deve essere preceduto dal modificatore [this](../../../csharp/language-reference/keywords/this.md).  
  
4.  Nel codice chiamante, aggiungere una direttiva `using` per specificare lo [spazio dei nomi](../../../csharp/language-reference/keywords/namespace.md) che contiene la classe del metodo di estensione.  
  
5.  Chiamare i metodi come se fossero metodi di istanza sul tipo.  
  
     Si noti che il primo parametro non viene specificato tramite la chiamata di codice, poiché rappresenta il tipo su cui viene applicato l'operatore e il compilatore conosce già il tipo dell'oggetto. È sufficiente specificare gli argomenti per i parametri da 2 a `n`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente un metodo di estensione denominato `WordCount` viene implementato nella classe `CustomExtensions.StringExtension`. Il metodo opera sulla classe <xref:System.String>, che viene specificata come primo parametro del metodo. Lo spazio dei nomi `CustomExtensions` viene importato nello spazio dei nomi dell'applicazione e il metodo viene chiamato all'interno del metodo `Main`.  
  
 [!code-cs[csProgGuideExtensionMethods#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-implement-and-call-a-custom-extension-method_1.cs)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per eseguire questo codice, copiarlo e incollarlo nel progetto di applicazione console di Visual C# creato in [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)]. Per impostazione predefinita, questo progetto usa la versione 3.5 di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], e ha un riferimento a System.Core.dll e una direttiva `using` per System.Linq. Se uno o più di questi requisiti non sono presenti nel progetto, è possibile aggiungerli manualmente.   
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 I metodi di estensione non presentano vulnerabilità di protezione specifiche. Non possono mai essere usati per rappresentare metodi esistenti su un tipo, perché tutti i conflitti di nomi vengono risolti a favore dell'istanza o del metodo statico definito dal tipo stesso. I metodi di estensione non possono accedere ai dati privati nella classe estesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Metodi di estensione](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [LINQ (Language Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)   
 [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [internal](../../../csharp/language-reference/keywords/internal.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [this](../../../csharp/language-reference/keywords/this.md)   
 [namespace](../../../csharp/language-reference/keywords/namespace.md)
