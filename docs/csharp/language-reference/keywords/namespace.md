---
title: namespace (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- namespace_CSharpKeyword
- namespace
dev_langs:
- CSharp
helpviewer_keywords:
- namespace keyword [C#]
- scope [C#]
ms.assetid: 0a788423-9110-42e0-97d9-bda41ca4870f
caps.latest.revision: 28
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cc90fe67f7c65d53980786c39f2a6f9869eec321
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="namespace-c-reference"></a>namespace (Riferimenti per C#)
La parola chiave `namespace` è usata per dichiarare un ambito che contiene un set di oggetti correlati. È possibile usare uno spazio dei nomi per organizzare gli elementi di codice e creare tipi univoci globali.  
  
 [!code-cs[csrefKeywordsNamespace#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/namespace_1.cs)]  
  
## <a name="remarks"></a>Note  
 All'interno di uno spazio dei nomi, è possibile dichiarare uno o più dei tipi seguenti:  
  
-   un altro spazio dei nomi  
  
-   [class](../../../csharp/language-reference/keywords/class.md)  
  
-   [interface](../../../csharp/language-reference/keywords/interface.md)  
  
-   [struct](../../../csharp/language-reference/keywords/struct.md)  
  
-   [enum](../../../csharp/language-reference/keywords/enum.md)  
  
-   [delegate](../../../csharp/language-reference/keywords/delegate.md)  
  
 Il compilatore aggiunge uno spazio dei nomi predefinito indipendentemente dal fatto che venga dichiarato o meno uno spazio dei nomi in modo esplicito in un file di origine C#. Questo spazio dei nomi senza nome, talvolta chiamato spazio dei nomi globale, è presente in ogni file. Qualsiasi identificatore nello spazio dei nomi globale può essere usato all'interno di uno spazio dei nomi denominato.  
  
 Gli spazi dei nomi hanno in modo implicito accesso pubblico, non modificabile. Per informazioni sui modificatori di accesso che è possibile assegnare agli elementi all'interno di uno spazio dei nomi, vedere [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md).  
  
 È possibile definire uno spazio dei nomi in una o più dichiarazioni. L'esempio seguente definisce due classi come parte dello spazio dei nomi `MyCompany`:  
  
 [!code-cs[csrefKeywordsNamespace#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/namespace_2.cs)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra come chiamare un metodo statico in uno spazio dei nomi annidato.  
  
 [!code-cs[csrefKeywordsNamespace#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/namespace_3.cs)]  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 Per altre informazioni sull'uso degli spazi dei nomi, vedere gli argomenti seguenti:  
  
-   [Spazi dei nomi](../../../csharp/programming-guide/namespaces/index.md)  
  
-   [Uso degli spazi dei nomi](../../../csharp/programming-guide/namespaces/using-namespaces.md)  
  
-   [Procedura: Usare l'alias dello spazio dei nomi globale](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per gli spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [using](../../../csharp/language-reference/keywords/using.md)
