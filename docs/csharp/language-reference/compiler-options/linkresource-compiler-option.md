---
title: "/linkresource (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/linkresource"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/linkresource compiler option [C#]"
  - "linkres compiler option [C#]"
  - "/linkres compiler option [C#]"
  - "-linkres compiler option [C#]"
  - "-linkresource compiler option [C#]"
  - "linkresource compiler option [C#]"
ms.assetid: 440c26c2-77c1-4811-a0a3-57cce3f5fc96
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /linkresource (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Crea un collegamento a una risorsa di .NET Framework nel file di output.  Il file di risorse non viene aggiunto al file di output.  Questa opzione è diversa dall'opzione [\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md) che incorpora un file di risorse nel file di output.  
  
## Sintassi  
  
```  
/linkresource:filename[,identifier[,accessibility-modifier]]  
```  
  
## Argomenti  
 `filename`  
 Rappresenta il file di risorse .NET Framework cui si desidera stabilire un collegamento dall'assembly.  
  
 `identifier` \(facoltativo\)  
 Nome logico della risorsa, utilizzato per caricare la risorsa stessa.  L'impostazione predefinita corrisponde al nome del file.  
  
 `accessibility-modifier` \(facoltativo\)  
 Rappresenta l'accessibilità della risorsa: public o private.  L'impostazione predefinita è public.  
  
## Note  
 Per impostazione predefinita, le risorse collegate sono pubbliche nell'assembly quando vengono create con il compilatore C\#.  Per renderle private, specificare `private` come modificatore di accessibilità.  Non è consentito alcun modificatore diverso da `public` o `private`.  
  
 Per **\/linkresource** è necessaria un'opzione [\/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) diversa da **\/target:module**.  
  
 Se `filename` è un file di risorse .NET Framework creato, ad esempio, tramite [Resgen.exe](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) oppure nell'ambiente di sviluppo, sarà accessibile con i membri dello spazio dei nomi <xref:System.Resources>.  Per ulteriori informazioni, vedere <xref:System.Resources.ResourceManager?displayProperty=fullName>.  Per tutte le altre risorse, utilizzare i metodi `GetManifestResource`\* nella classe <xref:System.Reflection.Assembly> per accedere alla risorsa in fase di esecuzione.  
  
 Il file specificato in `filename` può avere qualsiasi formato.  Può ad esempio risultare opportuno includere una DLL nativa nell'assembly, in modo da consentirne l'installazione nella Global Assembly Cache e l'accesso dal codice gestito nell'assembly.  Nel secondo esempio riportato di seguito vengono illustrate le operazioni da eseguire a tal fine.  È possibile eseguire la stessa operazione anche in Assembly Linker.  Nel terzo esempio riportato di seguito vengono illustrate le operazioni da eseguire a tal fine.  Per ulteriori informazioni, vedere [Al.exe \(Assembly Linker\)](../Topic/Al.exe%20\(Assembly%20Linker\).md) e [Utilizzo di assembly e della Global Assembly Cache](../Topic/Working%20with%20Assemblies%20and%20the%20Global%20Assembly%20Cache.md).  
  
 **\/linkres** rappresenta la versione abbreviata di **\/linkresource**.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
## Esempio  
 Compilare `in.cs` e stabilire il collegamento al file di risorse `rf.resource`:  
  
```  
csc /linkresource:rf.resource in.cs  
```  
  
## Esempio  
 Compilare `A.cs` in una DLL, creare un collegamento a una DLL N.dll nativa e inserire l'output nella Global Assembly Cache \(GAC\).  In questo esempio i file A.dll e N.dll verranno memorizzati entrambi nella GAC.  
  
```  
csc /linkresource:N.dll /t:library A.cs  
gacutil -i A.dll  
```  
  
## Esempio  
 In questo esempio viene eseguita la stessa operazione descritta in precedenza, ma vengono utilizzate le opzioni di Assembly Linker.  
  
```  
csc /t:module A.cs  
al /out:A.dll A.netmodule /link:N.dll   
gacutil -i A.dll  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Al.exe \(Assembly Linker\)](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [Utilizzo di assembly e della Global Assembly Cache](../Topic/Working%20with%20Assemblies%20and%20the%20Global%20Assembly%20Cache.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)