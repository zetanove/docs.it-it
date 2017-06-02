---
title: "How to: Create an XML Documentation File Using CodeDOM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CodeDOM, generating XML documentation"
  - "XML documentation, creating using CodeDOM"
  - "Code Document Object Model, generating XML documentation"
ms.assetid: e3b80484-36b9-41dd-9d21-a2f9a36381dc
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Create an XML Documentation File Using CodeDOM
CodeDOM può essere utilizzato per creare codice in grado di generare documentazione XML.  Il processo comporta la creazione del grafico CodeDOM che contiene i commenti per la documentazione XML, la generazione del codice e la compilazione del codice generato con l'opzione che crea l'output di tale documentazione.  
  
### Per creare un grafico CodeDOM contenente i commenti per la documentazione XML  
  
1.  Creare un oggetto <xref:System.CodeDom.CodeCompileUnit> contenente il grafico CodeDOM per l'applicazione di esempio.  
  
2.  Utilizzare il costruttore <xref:System.CodeDom.CodeCommentStatement.%23ctor%2A> con il parametro `docComment` impostato su `true` per creare il testo e gli elementi di commento della documentazione XML.  
  
     [!code-csharp[CodeDomHelloWorldSample#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#4)]
     [!code-vb[CodeDomHelloWorldSample#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#4)]  
  
### Per generare il codice da CodeCompileUnit  
  
1.  Utilizzare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> per generare il codice e creare un file di origine da compilare.  
  
     [!code-csharp[CodeDomHelloWorldSample#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#5)]
     [!code-vb[CodeDomHelloWorldSample#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#5)]  
  
### Per compilare il codice e generare il file di documentazione  
  
1.  Aggiungere l'opzione di compilazione **\/doc** alla proprietà <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> di un oggetto <xref:System.CodeDom.Compiler.CompilerParameters> e passare l'oggetto al metodo <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> per creare il file di documentazione XML quando il codice viene compilato.  
  
     [!code-csharp[CodeDomHelloWorldSample#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#6)]
     [!code-vb[CodeDomHelloWorldSample#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#6)]  
  
## Esempio  
 Nell'esempio di codice seguente viene creato un grafico CodeDOM con i commenti della documentazione, viene generato un file di codice a partire da tale grafico, viene compilato il file e viene creato un file di documentazione XML associato.  
  
 [!code-csharp[CodeDomHelloWorldSample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#1)]
 [!code-vb[CodeDomHelloWorldSample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#1)]  
  
 Nell'esempio di codice viene creata la documentazione XML seguente nel file HelloWorldDoc.xml.  
  
```  
<?xml version="1.0" ?>   
<doc>  
  <assembly>  
    <name>HelloWorld</name>   
  </assembly>  
  <members>  
    <member name="T:Samples.Class1">  
      <summary>  
        Create a Hello World application.   
        <seealso cref="M:Samples.Class1.Main" />   
      </summary>  
    </member>  
    <member name="M:Samples.Class1.Main">  
      <summary>  
        Main method for HelloWorld application.   
        <para>Add a new paragraph to the description.</para>   
      </summary>  
    </member>  
  </members>  
</doc>  
```  
  
## Compilazione del codice  
  
-   Per essere eseguito correttamente, questo esempio di codice richiede il set di autorizzazioni `FullTrust`.  
  
## Vedere anche  
 [Documenting Your Code with XML](../Topic/Documenting%20Your%20Code%20with%20XML%20\(Visual%20Basic\).md)   
 [Commenti relativi alla documentazione XML](../Topic/XML%20Documentation%20Comments%20\(C%23%20Programming%20Guide\).md)   
 [Documentazione di XML](../Topic/XML%20Documentation%20\(Visual%20C++\).md)