---
title: '@ (Riferimenti per C#) | Microsoft Docs'
ms.date: 2017-02-09
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '@_CSharpKeyword'
- '@'
dev_langs:
- CSharp
helpviewer_keywords:
- '@ special character [C#]'
- '@ language element [C#]'
ms.assetid: 89bc7e53-85f5-478a-866d-1cca003c4e8c
author: rpetrusha
ms.author: ronpet
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: c32a3d83730c8e9ba5e74f74a436174294538d95
ms.contentlocale: it-it
ms.lasthandoff: 05/24/2017

---
# <a name="-c-reference"></a>@ (Riferimenti per C#)

Il carattere speciale `@` funge da identificatore verbatim. Può essere usato nei seguenti modi:

1. Per abilitare le parole chiave di C# da usare come identificatori. Il carattere `@` precede un elemento di codice che il compilatore deve interpretare come identificatore piuttosto che come parola chiave di C#. Nell'esempio seguente il carattere `@` viene usato per definire un identificatore denominato `for` che verrà usato in un ciclo `for`.

   [!code-cs[verbatim1](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#1)]

1. Per indicare che un valore letterale stringa deve essere interpretato come verbatim. Il carattere `@` in questa istanza definisce un *valore letterale stringa verbatim*. Le sequenze di escape semplici, ad esempio `"\\"` per una barra rovesciata, le sequenze di escape esadecimali, ad esempio `"\x0041"` per una A maiuscola, le sequenze di escape Unicode, ad esempio `"\u0041"` per una A maiuscola, vengono interpretate letteralmente. Solo una sequenza di escape per le virgolette doppie (`""`) non viene interpretata letteralmente e produce una virgoletta singola. Nell'esempio seguente vengono definiti due percorsi di file identici, uno usando un valore letterale stringa normale e l'altro usando un valore letterale stringa verbatim. Questo è uno degli usi più comuni dei valori letterali stringa verbatim.

   [!code-cs[verbatim2](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#2)]

   Nell'esempio seguente viene illustrato l'effetto della definizione di un valore letterale stringa normale e di un valore letterale stringa verbatim che contengono le sequenze di caratteri identiche.

   [!code-cs[verbatim3](../../../../samples/snippets/csharp/language-reference/keywords/verbatim1.cs#3)]

1. Per consentire al compilatore di distinguere tra gli attributi in caso di conflitto di denominazione. Un attributo è un tipo che deriva da @System.Attribute. Il nome del relativo tipo in genere include il suffisso **Attribute**, anche se il compilatore non applica questa convenzione. È possibile fare riferimento all'attributo nel codice usando il nome completo del tipo, ad esempio `[InfoAttribute]`, o il nome abbreviato, ad esempio, `[Info]`. Tuttavia, si verifica un conflitto di denominazione se due nomi di tipo di attributo abbreviati sono identici e se un nome di tipo include il suffisso **Attribute** e l'altro no. Ad esempio, il codice seguente non viene compilato perché il compilatore non è in grado di determinare se l'attributo `Info` o `InfoAttribute` viene applicato al metodo `Main`.

   ```csharp
   using System;

   [AttributeUsage(AttributeTargets.Class)]
   public class Info : Attribute
   {
      private string information;
      
      public Info(string info)
      {
          information = info;
      }
   }

   [AttributeUsage(AttributeTargets.Method)]
   public class InfoAttribute : Attribute
   {
      private string information;
      
      public InfoAttribute(string info)
      {
          information = info;
      }
   }

   [Info("A simple executable.")]
   public class Example
   {
      [InfoAttribute("The entry point.")]
      public static void Main()
      {
      }
   }
   ```  

   Se si usa l'identificatore verbatim per identificare l'attributo `Info`, l'esempio viene compilato correttamente.

   [!code-cs[verbatim4](../../../../samples/snippets/csharp/language-reference/keywords/verbatim4.cs#1)]

## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [C# Special Characters](../../../csharp/language-reference/tokens/index.md) (Caratteri speciali di C#)

