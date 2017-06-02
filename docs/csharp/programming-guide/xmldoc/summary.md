---
title: '&lt;summary&gt; (Guida per programmatori C#) | Documentazione Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- <summary>
- summary
dev_langs:
- CSharp
helpviewer_keywords:
- <summary> C# XML tag
- summary C# XML tag
ms.assetid: b4c43d92-2067-4eac-a59a-d32f5248c08b
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b74e5bf964ff82f88fe2822257a64eccb5697535
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="ltsummarygt-c-programming-guide"></a>&lt;summary&gt; (Guida per programmatori C#)
## <a name="syntax"></a>Sintassi  
  
```  
<summary>description</summary>  
```  
  
#### <a name="parameters"></a>Parametri  
 `description`  
 Un riepilogo dell'oggetto.  
  
## <a name="remarks"></a>Note  
 Il tag \<summary> deve essere usato per descrivere un tipo o un membro del tipo. Utilizzare [ \<osservazioni >](../../../csharp/programming-guide/xmldoc/remarks.md) per aggiungere informazioni supplementari alla descrizione di un tipo. Utilizzare l'[attributo cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) per abilitare strumenti della documentazione come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061) per creare collegamenti ipertestuali interni alle pagine della documentazione per gli elementi di codice.  
  
 Il testo del tag \<summary> rappresenta l'unica fonte di informazioni sul tipo in IntelliSense e viene visualizzato anche nella finestra Visualizzatore oggetti.  
  
 Compilare con [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare i commenti relativi alla documentazione in un file. Per creare la documentazione finale basata sul file generato dal compilatore, è possibile creare uno strumento personalizzato o usare uno strumento come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061).  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideDocComments#12](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_1.cs)]  
  
 L'esempio precedente produce il seguente XML.  
  
```  
<?xml version="1.0"?>  
<doc>  
    <assembly>  
        <name>YourNamespace</name>  
    </assembly>  
    <members>  
        <member name="T:DotNetEvents.TestClass">  
            text for class TestClass  
        </member>  
        <member name="M:DotNetEvents.TestClass.DoWork(System.Int32)">  
            <summary>DoWork is a method in the TestClass class.  
            <para>Here's how you could make a second paragraph in a description. <see cref="M:System.Console.WriteLine(System.String)"/> for information about output statements.</para>  
            <seealso cref="M:DotNetEvents.TestClass.Main"/>  
            </summary>  
        </member>  
        <member name="M:DotNetEvents.TestClass.Main">  
            text for Main  
        </member>  
    </members>  
</doc>  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene illustrato come effettuare un riferimento `cref` a un tipo generico.  
  
 [!code-cs[csProgGuideDocComments#11](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_2.cs)]  
  
 L'esempio precedente produce il seguente XML.  
  
```  
<?xml version="1.0"?>  
<doc>  
    <assembly>  
        <name>YourNamespace</name>  
    </assembly>  
    <members>  
        <member name="T:ExtensionMethodsDemo1.A">  
            <summary cref="T:ExtensionMethodsDemo1.C`1">  
            </summary>  
        </member>  
        <member name="T:ExtensionMethodsDemo1.B">  
            <summary cref="T:C`1">  
            </summary>  
        </member>  
        <member name="T:ExtensionMethodsDemo1.C`1">  
            <summary cref="T:ExtensionMethodsDemo1.A">  
            </summary>  
            <typeparam name="T"></typeparam>  
        </member>  
    </members>  
</doc>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)

