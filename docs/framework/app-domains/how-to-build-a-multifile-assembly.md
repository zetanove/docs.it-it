---
title: "Procedura: Compilare un assembly su pi&#249; file | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], su più file"
  - "punto di ingresso per assembly"
  - "compilazione di assembly"
  - "Al.exe"
  - "riga di comando (compilatori)"
  - "manifesto dell'assembly, assembly su più file"
  - "assembly [.NET Framework], compilazione"
  - "Assembly Linker"
  - "moduli di codice"
  - "assembly su più file"
ms.assetid: 261c5583-8a76-412d-bda7-9b8ee3b131e5
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: Compilare un assembly su pi&#249; file
In questo articolo viene illustrato come creare un assembly su più file e viene visualizzato il codice che illustra ogni passaggio della procedura.  
  
> [!NOTE]
>  L'IDE di Visual Studio per C\# e Visual Basic può essere utilizzato esclusivamente per creare assembly su singolo file.  Per creare assembly su più file, è necessario utilizzare i compilatori della riga di comando o Visual Studio con Visual C\+\+.  
  
### Per creare un assembly su più file  
  
1.  Compilare in moduli di codice tutti i file contenenti spazi dei nomi a cui fanno riferimento altri moduli dell'assembly.  L'estensione predefinita per i moduli di codice è .netmodule.  
  
     Si supponga, ad esempio, che il file `Stringer` abbia uno spazio dei nomi denominato `myStringer`, che include una classe denominata `Stringer`.  Nella classe `Stringer` è disponibile un metodo denominato `StringerMethod`, che consente di scrivere una singola riga nella console.  
  
     [!code-cpp[Conceptual.Assembly.Multifile#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/stringer.cpp#1)]
     [!code-csharp[Conceptual.Assembly.Multifile#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/stringer.cs#1)]
     [!code-vb[Conceptual.Assembly.Multifile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/stringer.vb#1)]  
  
     Per compilare il codice, utilizzare il comando seguente:  
  
     [!code-cpp[Conceptual.Assembly.Multifile#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/stringer.cpp#2)]
     [!code-csharp[Conceptual.Assembly.Multifile#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/stringer.cs#2)]
     [!code-vb[Conceptual.Assembly.Multifile#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/stringer.vb#2)]  
  
     Specificando il parametro *module* con l'opzione di compilatore **\/t:** si indica che è necessario compilare il file come modulo anziché come assembly.  Il compilatore crea un modulo denominato `Stringer.netmodule`, che può essere aggiunto a un assembly.  
  
2.  Compilare tutti gli altri moduli, utilizzando le opzioni di compilatore necessarie per indicare gli altri moduli a cui si fa riferimento nel codice.  In questo passaggio viene utilizzata l'opzione del compilatore **\/addmodule**.  
  
     Nell'esempio riportato di seguito un modulo di codice denominato `Client` contiene un metodo `Main` del punto di ingresso che fa riferimento a un metodo nel modulo `Stringer.dll` creato nel passaggio 1.  
  
     [!code-cpp[Conceptual.Assembly.Multifile#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#3)]
     [!code-csharp[Conceptual.Assembly.Multifile#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#3)]
     [!code-vb[Conceptual.Assembly.Multifile#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#3)]  
  
     Per compilare il codice, utilizzare il comando seguente:  
  
     [!code-cpp[Conceptual.Assembly.Multifile#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#4)]
     [!code-csharp[Conceptual.Assembly.Multifile#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#4)]
     [!code-vb[Conceptual.Assembly.Multifile#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#4)]  
  
     Specificare l'opzione **\/t:module**, poiché tale modulo verrà aggiunto a un assembly in un passaggio successivo.  Specificare l'opzione **\/addmodule** poiché nel codice di `Client` sono presenti riferimenti allo spazio dei nomi creato dal codice in `Stringer.netmodule`.  Il compilatore crea un modulo denominato `Client.netmodule` contenente un riferimento a un altro modulo, `Stringer.netmodule`.  
  
    > [!NOTE]
    >  Nei compilatori di C\# e di Visual Basic viene supportata la creazione diretta di assembly su più file utilizzando le due diverse sintassi descritte di seguito.  
    >   
    >  -   Un assembly su due file viene creato da due compilazioni:  
    >   
    >      [!code-cpp[Conceptual.Assembly.Multifile#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#5)]
      [!code-csharp[Conceptual.Assembly.Multifile#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#5)]
      [!code-vb[Conceptual.Assembly.Multifile#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#5)]  
    > -   Un assembly su due file viene creato da una compilazione:  
    >   
    >      [!code-cpp[Conceptual.Assembly.Multifile#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#6)]
      [!code-csharp[Conceptual.Assembly.Multifile#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#6)]
      [!code-vb[Conceptual.Assembly.Multifile#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#6)]  
  
3.  Utilizzare l'utilità [Assembly Linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) per creare un file di output contenente il manifesto dell'assembly.  In questo file sono contenute informazioni di riferimento per tutti i moduli o le risorse che fanno parte dell'assembly.  
  
     Al prompt dei comandi digitare il seguente comando:  
  
     **al** \<*nome modulo*\> \<*nome modulo*\> … **\/main:**\<*nome metodo*\> **\/out:**\<*nome file*\> **\/target:**\<*tipo file assembly*\>  
  
     Gli argomenti *nome modulo* di questo comando consentono di specificare il nome di ogni modulo da includere nell'assembly.  L'opzione **\/main:** consente di specificare il nome del metodo che corrisponde al punto di ingresso dell'assembly.  L'opzione **\/out:** consente di specificare il nome del file di output, contenente i metadati dell'assembly.  L'opzione **\/target:** consente di specificare che l'assembly è un file eseguibile \(EXE\) da console, un file eseguibile di Windows \(WIN\) o una libreria \(LIB\).  
  
     Nell'esempio seguente l'utilità Al.exe consente di creare un assembly denominato `myAssembly.exe`, che corrisponde al file eseguibile da console.  L'applicazione è costituita da due moduli denominati `Client.netmodule` e `Stringer.netmodule` e dal file eseguibile denominato `myAssembly.exe,` contenente solo i metadati dell'assembly.  Il punto di ingresso dell'assembly è costituito dal metodo `Main` della classe `MainClientApp`, situata nel file `Client.dll`.  
  
    ```  
    al Client.netmodule Stringer.netmodule /main:MainClientApp.Main /out:myAssembly.exe /target:exe   
    ```  
  
     È possibile utilizzare [MSIL Disassembler \(Ildasm.exe\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per esaminare i contenuti di un assembly o determinare se un file sia un assembly o un modulo.  
  
## Vedere anche  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Procedura: Visualizzare il contenuto dell'assembly](../../../docs/framework/app-domains/how-to-view-assembly-contents.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Assembly su più file](../../../docs/framework/app-domains/multifile-assemblies.md)