---
title: "Procedura: determinare il nome completo di un assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], nomi"
  - "nomi [.NET Framework], assembly"
  - "nomi [.NET Framework], nomi completi di tipi"
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: determinare il nome completo di un assembly
Per individuare il nome completo di un assembly nella Global Assembly Cache, usare lo strumento Global Assembly Cache \([Gacutil.exe](../../../docs/framework/tools/gacutil-exe-gac-tool.md)\).  Vedere [Procedura: visualizzare il contenuto della Global Assembly Cache](../../../docs/framework/app-domains/how-to-view-the-contents-of-the-gac.md).  
  
 Per gli assembly che non si trovano nella Global Assembly Cache è possibile ottenere il nome completo dell'assembly in diversi modi: è possibile usare il codice per restituire le informazioni alla console o a una variabile oppure [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per esaminare i metadati dell'assembly che contengono il nome completo.  
  
-   Se l'assembly è già stato caricato dall'applicazione, è possibile recuperare il valore della proprietà <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName> per ottenere il nome completo.  È possibile usare questo approccio indipendentemente dalla presenza dell'assembly nella GAC.  Nell'esempio viene illustrata una situazione di questo tipo.  
  
-   Se si conosce il percorso del file system dell'assembly, è possibile chiamare il metodo statico \(`Shared` in Visual Basic\) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=fullName> per ottenere il nome completo dell'assembly.  Di seguito è riportato un semplice esempio.  
  
     [!code-csharp[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/cs/getassemblyname1.cs#1)]
     [!code-vb[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/vb/getassemblyname1.vb#1)]  
  
-   È possibile usare [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per esaminare i metadati dell'assembly che contengono il nome completo.  
  
 Per altre informazioni sull'impostazione degli attributi dell'assembly, ad esempio, versione, impostazioni cultura e nome dell'assembly, vedere [Impostazione degli attributi dell'assembly](../../../docs/framework/app-domains/set-assembly-attributes.md).  Per altre informazioni sull'assegnazione di un nome sicuro all'assembly, vedere [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md).  
  
## Esempio  
 Il codice seguente mostra come visualizzare il nome completo di un assembly contenente una classe specificata nella console.  Poiché contiene il nome di un assembly già caricato dall'app, non è importante che l'assembly sia contenuto nella GAC.  
  
 [!code-cpp[Assembly.Fullname#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Assembly.FullName/CPP/example2.cpp#2)]
 [!code-csharp[Assembly.Fullname#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Assembly.FullName/CS/example2.cs#2)]
 [!code-vb[Assembly.Fullname#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Assembly.FullName/VB/example2.vb#2)]  
  
## Vedere anche  
 [Nomi degli assembly](../../../docs/framework/app-domains/assembly-names.md)   
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)   
 [Global Assembly Cache](../../../docs/framework/app-domains/gac.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)