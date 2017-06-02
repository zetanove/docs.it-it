---
title: "Using the CodeDOM | Microsoft Docs"
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
  - "code compilers"
  - "Code Document Object Model"
  - "Code Document Object Model, graphs"
  - "types, CodeDOM"
  - "namespaces [.NET Framework], CodeDOM"
  - "templated code generation"
  - "dynamically representing source code"
  - "source code models"
  - "CodeDOM"
  - "graphing with CodeDOM"
  - "dynamic compilation"
  - "code generators"
  - "CodeDOM, graphs"
ms.assetid: 0444ddf3-c3f6-44ed-a999-f710d9c3e0cf
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Using the CodeDOM
Con CodeDOM vengono forniti tipi che rappresentano molti tipi comuni di elementi di codice sorgente.  È possibile progettare un programma che compili un modello di codice sorgente utilizzando elementi CodeDOM per assemblare un grafico di oggetti.  Da tale grafico è possibile produrre codice sorgente in uno dei linguaggi di programmazione supportati utilizzando un generatore di codice CodeDOM.  È anche possibile utilizzare CodeDOM per compilare codice sorgente in un assembly binario.  
  
 Di seguito sono riportati alcuni impieghi comuni di CodeDOM:  
  
-   Generazione di codice basata su modelli: generazione di codice per ASP.NET, proxy per client di servizi Web basati su XML, creazioni guidate di codice, strumenti di progettazione e altri sistemi generatori di codice.  
  
-   Compilazione dinamica: supporto per la compilazione di codice in uno o più linguaggi.  
  
## Compilazione di un grafico CodeDOM  
 Con lo spazio dei nomi <xref:System.CodeDom> vengono fornite classi che consentono di rappresentare la struttura logica del codice sorgente, indipendentemente dalla sintassi del linguaggio.  
  
### Struttura di un grafico CodeDOM  
 La struttura di un grafico CodeDOM può essere paragonata a una struttura ad albero di contenitori.  Il contenitore posto più in alto, o radice, di ciascun grafico CodeDOM compilabile è un oggetto <xref:System.CodeDom.CodeCompileUnit>.  Ogni elemento del modello di codice sorgente deve essere collegato al grafico tramite una proprietà di un <xref:System.CodeDom.CodeObject> nel grafo.  
  
### Compilazione di un modello di codice sorgente per un programma di esempio  
 Di seguito viene illustrato come compilare un grafico di oggetti CodeDOM che rappresenta il codice di una semplice applicazione di esempio.  Per il codice sorgente completo di questo esempio, vedere <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=fullName>.  
  
#### Creazione di una unità di compilazione  
 CodeDOM definisce un oggetto denominato <xref:System.CodeDom.CodeCompileUnit>, in grado di fare riferimento a un grafo di oggetti CodeDOM, che modella il codice sorgente da compilare.  I **CodeCompileUnit** dispongono di proprietà per l'archiviazione di riferimenti ad attributi, spazi dei nomi e assembly.  
  
 Nei provider CodeDom che derivano dalla classe <xref:System.CodeDom.Compiler.CodeDomProvider> sono contenuti i metodi che elaborano il grafico di oggetti a cui fa riferimento un oggetto **CodeCompileUnit**.  
  
 Per creare un grafico di oggetti per una semplice applicazione, occorre assemblare il modello di codice sorgente e farvi riferimento da un'unità **CodeCompileUnit**.  
  
 Per creare una nuova unità di compilazione, è possibile utilizzare la sintassi illustrata nel seguente esempio:  
  
 [!code-cpp[CodeDomExample#12](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#12)]
 [!code-csharp[CodeDomExample#12](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#12)]
 [!code-vb[CodeDomExample#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#12)]  
  
 Un'unità <xref:System.CodeDom.CodeSnippetCompileUnit> può contenere una sezione di codice sorgente che è già nella forma del linguaggio di destinazione, ma non può essere compilata in un altro linguaggio.  
  
#### Definizione di uno spazio dei nomi  
 Per definire uno spazio dei nomi, creare <xref:System.CodeDom.CodeNamespace> e assegnarvi un nome utilizzando il costruttore appropriato o impostandone la proprietà **Name**.  
  
 [!code-cpp[CodeDomExample#13](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#13)]
 [!code-csharp[CodeDomExample#13](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#13)]
 [!code-vb[CodeDomExample#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#13)]  
  
#### Importazione di uno spazio dei nomi  
 Per aggiungere allo spazio dei nomi una direttiva per l'importazione di uno spazio dei nomi, aggiungere un <xref:System.CodeDom.CodeNamespaceImport> che indica lo spazio dei nomi da importare nella raccolta **CodeNamespace.Imports**.  
  
 Nel codice riportato di seguito viene aggiunta un'importazione dello spazio dei nomi **System** alla raccolta **Imports** di un oggetto **CodeNamespace** denominata `samples`:  
  
 [!code-cpp[CodeDomExample#14](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#14)]
 [!code-csharp[CodeDomExample#14](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#14)]
 [!code-vb[CodeDomExample#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#14)]  
  
#### Collegamento di elementi di codice nel grafico di oggetti  
 Tutti gli elementi di codice che compongono un grafo CodeDOM devono essere collegati all'oggetto <xref:System.CodeDom.CodeCompileUnit> che costituisce l'elemento radice della struttura ad albero da una serie di riferimenti tra elementi a cui si fa direttamente riferimento dalle proprietà dell'oggetto radice del grafo.  Per stabilire un riferimento da un oggetto contenitore, impostare un oggetto su una proprietà dell'oggetto contenitore.  
  
 L'istruzione riportata di seguito aggiunge il **CodeNamespace** `samples` alla proprietà di raccolta **Namespaces** dell'oggetto **CodeCompileUnit** radice.  
  
 [!code-cpp[CodeDomExample#15](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#15)]
 [!code-csharp[CodeDomExample#15](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#15)]
 [!code-vb[CodeDomExample#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#15)]  
  
#### Definizione di un tipo  
 Per dichiarare una classe, struttura, interfaccia o enumerazione con CodeDOM, creare un nuovo oggetto <xref:System.CodeDom.CodeTypeDeclaration> e assegnarvi un nome.  Nell'esempio che segue viene mostrata questa operazione utilizzando l'overload di un costruttore per impostare la proprietà **Name**:  
  
 [!code-cpp[CodeDomExample#16](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#16)]
 [!code-csharp[CodeDomExample#16](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#16)]
 [!code-vb[CodeDomExample#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#16)]  
  
 Per aggiungere un tipo a uno spazio dei nomi, aggiungere una <xref:System.CodeDom.CodeTypeDeclaration> che rappresenta il tipo da aggiungere allo spazio dei nomi alla raccolta **Types** di un **CodeNamespace**.  
  
 Nell'esempio che segue viene illustrato come aggiungere una classe `class1` a un **CodeNamespace** denominato `samples`:  
  
 [!code-cpp[CodeDomExample#17](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#17)]
 [!code-csharp[CodeDomExample#17](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#17)]
 [!code-vb[CodeDomExample#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#17)]  
  
#### Aggiunta di membri a una classe  
 Con lo spazio dei nomi <xref:System.CodeDom> vengono forniti diversi elementi che possono essere utilizzati per rappresentare membri di classi.  Ogni membro di classe può essere aggiunto alla raccolta **Members** di una <xref:System.CodeDom.CodeTypeDeclaration>.  
  
#### Definizione di un metodo quale punto di ingresso al codice di un file eseguibile  
 Se si sta compilando il codice di un programma eseguibile, è necessario indicarne il punto d'ingresso creando un <xref:System.CodeDom.CodeEntryPointMethod> che rappresenti il metodo da cui si desidera che l'esecuzione del programma abbia inizio.  
  
 Nel seguente esempio viene illustrato come definire un punto di ingresso che contenga una <xref:System.CodeDom.CodeMethodInvokeExpression> che chiama **System.Console.WriteLine** per scrivere "Hello World\!":  
  
 [!code-cpp[CodeDomExample#18](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#18)]
 [!code-csharp[CodeDomExample#18](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#18)]
 [!code-vb[CodeDomExample#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#18)]  
  
 Nell'istruzione che segue, il metodo `Start`, che funge da punto di ingresso, viene aggiunto alla raccolta **Members** di `class1`:  
  
 [!code-cpp[CodeDomExample#19](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#19)]
 [!code-csharp[CodeDomExample#19](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#19)]
 [!code-vb[CodeDomExample#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#19)]  
  
 Adesso l'oggetto <xref:System.CodeDom.CodeCompileUnit> denominato `compileUnit` contiene il grafo CodeDOM di un semplice programma di esempio.  Per informazioni sulla generazione e sulla compilazione di codice da un grafico CodeDOM, vedere [Generazione di codice sorgente e compilazione di un programma a partire da un grafico CodeDOM](../../../docs/framework/reflection-and-codedom/generating-and-compiling-source-code-from-a-codedom-graph.md).  
  
### Ulteriori informazioni sulla compilazione di un grafico CodeDOM  
 Con CodeDOM viene fornito il supporto dei tipi di elementi di codice più comuni impiegati dai linguaggi di programmazione che supportano Common Language Runtime.  CodeDOM non è progettato per fornire elementi in grado di rappresentare tutte le possibili funzionalità dei linguaggi di programmazione.  Il codice che non può essere rappresentato facilmente con gli elementi CodeDOM può essere incapsulato in un <xref:System.CodeDom.CodeSnippetExpression>, un <xref:System.CodeDom.CodeSnippetStatement>, un <xref:System.CodeDom.CodeSnippetTypeMember> o un <xref:System.CodeDom.CodeSnippetCompileUnit>.  Con CodeDOM non è tuttavia possibile tradurre automaticamente frammenti in altri linguaggi.  
  
 Per la documentazione dei diversi tipi CodeDOM, vedere la documentazione di riferimento relativa allo spazio dei nomi <xref:System.CodeDom>.  
  
 Per una tavola di consultazione rapida che consenta di individuare l'elemento CodeDOM che rappresenta uno specifico tipo di elemento di codice, vedere [CodeDOM Quick Reference](http://msdn.microsoft.com/it-it/c77b8bfd-0a32-4e36-b59a-4f687f32c524).