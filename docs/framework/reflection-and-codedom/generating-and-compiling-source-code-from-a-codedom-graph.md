---
title: "Generating and Compiling Source Code from a CodeDOM Graph | Microsoft Docs"
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
  - "CodeDOM, generating source code"
  - "Code Document Object Model, graphs"
  - "templated code generation"
  - "source code, generating"
  - "dynamically representing source code"
  - "generating CodeDOM graphs"
  - "Code Document Object Model, generating source code"
  - "translating language to language"
  - "compiling assemblies"
  - "generating source code in multiple languages"
  - "graphing with CodeDOM"
  - "dynamic compilation"
  - "assemblies [.NET Framework], CodeDOM"
  - "source code generation"
  - "outputting source code by CodeDOM"
  - "code generators"
  - "compiling source code, multiple languages"
  - "CodeDOM, graphs"
ms.assetid: 6c864c8e-6dd3-4a65-ace0-36879d9a9c42
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Generating and Compiling Source Code from a CodeDOM Graph
Nello spazio dei nomi <xref:System.CodeDom.Compiler> vengono fornite interfacce per la generazione di codice sorgente da oggetti grafo CodeDOM e per la gestione della compilazione con i compilatori supportati.  Un provider di codice è in grado di produrre codice sorgente in un determinato linguaggio di programmazione, in base a un grafo CodeDOM.  Una classe derivata da <xref:System.CodeDom.Compiler.CodeDomProvider> può in genere fornire i metodi per la generazione e la compilazione di codice per il linguaggio supportato dal provider.  
  
## Utilizzo di un provider di codice CodeDOM per la generazione di codice sorgente  
 Per generare codice sorgente in un determinato linguaggio, è necessario un grafo CodeDOM che rappresenti la struttura del codice sorgente da generare.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come creare un'istanza del controllo <xref:Microsoft.CSharp.CSharpCodeProvider>.  
  
 [!code-cpp[CodeDomExample#21](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#21)]
 [!code-csharp[CodeDomExample#21](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#21)]
 [!code-vb[CodeDomExample#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#21)]  
  
 Il grafo per la generazione del codice è solitamente contenuto in una <xref:System.CodeDom.CodeCompileUnit>.  Per generare codice per una **CodeCompileUnit** contenente un grafo CodeDOM, chiamare il metodo <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> del provider di codice.  Tale metodo accetta come parametro un <xref:System.IO.TextWriter>, utilizzato per generare il codice sorgente. In alcuni casi è pertanto necessario creare prima un **TextWriter** in cui sia possibile scrivere.  Nell'esempio che segue viene illustrato come generare codice da una **CodeCompileUnit** e come scrivere il codice sorgente generato in un file denominato HelloWorld.cs.  
  
 [!code-cpp[CodeDomExample#22](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#22)]
 [!code-csharp[CodeDomExample#22](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#22)]
 [!code-vb[CodeDomExample#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#22)]  
  
## Utilizzo di un provider di codice CodeDOM per la compilazione di assembly  
 **Avvio della compilazione**  
  
 Per compilare un assembly mediante un provider CodeCom, è necessario disporre di un compilatore e del codice sorgente scritto nel relativo linguaggio o di un grafo CodeDOM da cui generare il codice sorgente da compilare.  
  
 Se si desidera effettuare la compilazione a partire da un grafo CodeDOM, passare la <xref:System.CodeDom.CodeCompileUnit> contenente il grafo al metodo <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A> del provider di codice.  Se si dispone di un file di codice sorgente scritto in un linguaggio accettato dal compilatore, passare il nome del file al metodo <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> del provider CodeDom.  È anche possibile passare una stringa contenente codice sorgente scritto in un linguaggio accettato dal compilatore al metodo <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A> del provider CodeDom.  
  
 **Configurazione dei parametri di compilazione**  
  
 Tutti i metodi standard di avvio della compilazione di un provider CodeDom accettano parametri di tipo <xref:System.CodeDom.Compiler.CompilerParameters> per la specifica delle opzioni da utilizzare per la compilazione.  
  
 Per specificare un nome per il file di assembly ottenuto, utilizzare la proprietà <xref:System.CodeDom.Compiler.CompilerParameters.OutputAssembly%2A> di **CompilerParameters**.  In alternativa, al file di output verrà assegnato un nome predefinito.  
  
 Per impostazione predefinita, un nuovo **CompilerParameters** viene inizializzato con la relativa proprietà <xref:System.CodeDom.Compiler.CompilerParameters.GenerateExecutable%2A> impostata su **false**.  Se si compila un programma eseguibile, la proprietà **GenerateExecutable** deve essere impostata su **true**.  Quando **GenerateExecutable** è impostata su **false**, il compilatore genererà una libreria di classi.  
  
 Se è in corso la compilazione di un eseguibile da un grafo CodeDOM, sarà necessario definire un <xref:System.CodeDom.CodeEntryPointMethod> nel grafo.  In presenza di più punti di ingresso al codice, può essere necessario impostare la proprietà <xref:System.CodeDom.Compiler.CompilerParameters.MainClass%2A> di **CompilerParameters** sul nome della classe che definisce il punto di ingresso da utilizzare.  
  
 Per includere informazioni di debug nell'eseguibile generato, impostare la proprietà <xref:System.CodeDom.Compiler.CompilerParameters.IncludeDebugInformation%2A> su **true**.  
  
 Se il progetto contiene riferimenti a uno o più assembly, è necessario specificare i nomi degli assembly come elementi di uno <xref:System.Collections.Specialized.StringCollection> nella proprietà <xref:System.CodeDom.Compiler.CompilerParameters.ReferencedAssemblies%2A> del **CompilerParameters** utilizzato all'avvio della compilazione.  
  
 È possibile compilare un assembly scritto in memoria piuttosto che su disco impostando la proprietà <xref:System.CodeDom.Compiler.CompilerParameters.GenerateInMemory%2A> su **true**.  Quando un assembly viene generato in memoria, è possibile che il codice ottenga un riferimento all'assembly generato dalla proprietà <xref:System.CodeDom.Compiler.CompilerResults.CompiledAssembly%2A> di un <xref:System.CodeDom.Compiler.CompilerResults>.  Se un assembly viene scritto su disco, sarà possibile ottenere il percorso dell'assembly generato tramite la proprietà <xref:System.CodeDom.Compiler.CompilerResults.PathToAssembly%2A> di un **CompilerResults**.  
  
 Per specificare una stringa personalizzata di argomenti della riga di comando da utilizzare quando si richiama il processo di compilazione, impostare la stringa nella proprietà <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A>.  
  
 Se è necessario un token di sicurezza Win32 per richiamare il processo di compilazione, specificare il token nella proprietà <xref:System.CodeDom.Compiler.CompilerParameters.UserToken%2A>.  
  
 Per collegare un file di risorse Win32 nell'assembly compilato, specificare il nome del file di risorse Win32 nella proprietà <xref:System.CodeDom.Compiler.CompilerParameters.Win32Resource%2A>.  
  
 Per specificare un livello di avviso in corrispondenza del quale interrompere la compilazione, impostare la proprietà <xref:System.CodeDom.Compiler.CompilerParameters.WarningLevel%2A> su un intero che rappresenta il livello di avviso in corrispondenza del quale interrompere la compilazione.  Se vengono rilevati avvisi impostando la proprietà <xref:System.CodeDom.Compiler.CompilerParameters.TreatWarningsAsErrors%2A> su **true**, sarà anche possibile configurare il compilatore per interrompere la compilazione.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come compilare un file di codice sorgente utilizzando un provider CodeDom derivato dalla classe <xref:System.CodeDom.Compiler.CodeDomProvider>.  
  
 [!code-cpp[CodeDomExample#23](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#23)]
 [!code-csharp[CodeDomExample#23](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#23)]
 [!code-vb[CodeDomExample#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#23)]  
  
## Linguaggi supportati  
 Con .NET Framework vengono forniti compilatori e generatori di codice per i seguenti linguaggi: C\#, Visual Basic, C\+\+, e JScript.  Il supporto CodeDOM può essere esteso ad altri linguaggi implementando generatori di codice e compilatori di codice specifici del linguaggio.  
  
## Vedere anche  
 <xref:System.CodeDom>   
 <xref:System.CodeDom.Compiler>   
 [Dynamic Source Code Generation and Compilation](../../../docs/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)   
 [CodeDOM Quick Reference](http://msdn.microsoft.com/it-it/c77b8bfd-0a32-4e36-b59a-4f687f32c524)