---
title: "&lt;summary&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "<summary>"
  - "summary"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<summary> (tag XML C#)"
  - "summary (tag XML C#)"
ms.assetid: b4c43d92-2067-4eac-a59a-d32f5248c08b
caps.latest.revision: 17
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;summary&gt; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## Sintassi  
  
```  
<summary>description</summary>  
```  
  
#### Parametri  
 `description`  
 Riepilogo relativo all'oggetto.  
  
## Note  
 Il tag \<summary\> deve essere utilizzato per descrivere un tipo o un membro del tipo.  Utilizzare [\<remarks\>](../../../csharp/programming-guide/xmldoc/remarks.md) per aggiungere informazioni supplementari alla descrizione di un tipo.  Utilizzare l'[attributo cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) per abilitare strumenti della documentazione come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061) per creare collegamenti ipertestuali interni alle pagine della documentazione per gli elementi di codice.  
  
 Il testo del tag \<summary\> rappresenta l'unica fonte di informazioni sul tipo in IntelliSense e viene visualizzato anche nel [Object Browser Window](http://msdn.microsoft.com/it-it/3c7f1673-1f0d-41b1-94ca-a3dcfcb82cda).  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  Per creare la documentazione finale basata sul file generato dal compilatore, è possibile creare uno strumento personalizzato o utilizzare uno strumento come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061).  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#12](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_1.cs)]  
  
 Nell'esempio precedente produce il seguente file XML.  
  
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
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come effettuare un riferimento `cref` a un tipo generico.  
  
 [!code-cs[csProgGuideDocComments#11](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_2.cs)]  
  
 Nell'esempio precedente produce il seguente file XML.  
  
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
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)