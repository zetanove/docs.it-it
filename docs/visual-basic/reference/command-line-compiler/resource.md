---
title: "/resource (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/resource compiler option [Visual Basic]"
  - "-resource compiler option [Visual Basic]"
  - "/res compiler option [Visual Basic]"
  - "res compiler option [Visual Basic]"
  - "-res compiler option [Visual Basic]"
  - "resource compiler option [Visual Basic]"
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /resource (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di incorporare una risorsa gestita in un assembly.  
  
## Sintassi  
  
```  
/resource:filename[,identifier[,public|private]]  
' -or-  
/res:filename[,identifier[,public|private]]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`filename`|Obbligatorio.  Nome del file di risorse da incorporare nel file di output.  Per impostazione predefinita, `filename` è pubblico nell'assembly.  Racchiudere il nome file tra virgolette \(""\) se contiene uno spazio.|  
|`identifier`|Parametro facoltativo.  Nome logico della risorsa, utilizzato per caricare la risorsa stessa.  L'impostazione predefinita corrisponde al nome del file.  Se si desidera, è possibile specificare se la risorsa nel manifesto dell'assembly è pubblica o privata, come nel seguente esempio: `/res:``filename.res`,`myname.res`,`public`|  
  
## Note  
 Utilizzare `/linkresource` per collegare una risorsa a un assembly senza inserire il file di risorse nel file di output.  
  
 Se `filename` è un file di risorse [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] creato, ad esempio, mediante [Resgen.exe \(Resource File Generator\)](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) o nell'ambiente di sviluppo, sarà possibile accedervi con i membri presenti nello spazio dei nomi <xref:System.Resources> \(per ulteriori informazioni, vedere <xref:System.Resources.ResourceManager>\).  Per accedere a tutte le altre risorse in fase di esecuzione, utilizzare uno dei seguenti metodi: <xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>, <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> o <xref:System.Reflection.Assembly.GetManifestResourceStream%2A>.  
  
 La forma abbreviata di `/resource` è `/res`.  
  
 Per informazioni su come impostare `/resource` nell'IDE di Visual Studio, vedere [Gestione delle risorse delle applicazioni \(.NET\)](/visual-studio/ide/managing-application-resources-dotnet).  
  
## Esempio  
 Il codice riportato di seguito consente di compilare `In.vb` e di collegare il file di risorse `Rf.resource`.  
  
```  
vbc /res:rf.resource in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)   
 [\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)