---
title: "/linkresource (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/linkresource compiler option [Visual Basic]"
  - "-linkresource compiler option [Visual Basic]"
  - "linkresource compiler option [Visual Basic]"
  - "/linkres compiler option [Visual Basic]"
  - "linkres compiler option [Visual Basic]"
  - "-linkres compiler option [Visual Basic]"
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /linkresource (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Crea un collegamento a una risorsa gestita.  
  
## Sintassi  
  
```  
/linkresource:filename[,identifier[,public|private]]  
' -or-  
/linkres:filename[,identifier[,public|private]]  
```  
  
## Argomenti  
 `filename`  
 Obbligatorio.  File di risorse da collegare all'assembly.  Se il nome file contiene uno spazio, racchiudere il nome tra virgolette \(" "\).  
  
 `identifier`  
 Parametro facoltativo.  Nome logico della risorsa  utilizzato per caricarla.  L'impostazione predefinita corrisponde al nome del file.  Se si desidera, è possibile specificare se il file nel manifesto dell'assembly è pubblico o privato, ad esempio `/linkres:filename.res,myname.res,public`.  Per impostazione predefinita, `filename` è pubblico nell'assembly.  
  
## Note  
 L'opzione `/linkresource` non consente di incorporare il file di risorse nel file di output; per farlo, utilizzare l'opzione `/resource`.  
  
 Per  `/linkresource` è necessaria un'opzione `/target` diversa da `/target:module`.  
  
 Se `filename` è un file di risorse [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] creato, ad esempio, mediante [Resgen.exe \(Resource File Generator\)](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md) o nell'ambiente di sviluppo, sarà possibile accedervi con i membri presenti nello spazio dei nomi <xref:System.Resources>.  Per ulteriori informazioni, vedere <xref:System.Resources.ResourceManager>. Per accedere a tutte le altre risorse in fase di esecuzione, utilizzare i metodi della classe<xref:System.Reflection.Assembly> che iniziano con `GetManifestResource`.  
  
 Il nome file può presentare qualsiasi formato.  Può ad esempio risultare opportuno includere una DLL nativa nell'assembly, in modo da consentirne l'installazione nella Global Assembly Cache e l'accesso dal codice gestito nell'assembly.  
  
 La forma breve di `/linkresource` è `/linkres`.  
  
> [!NOTE]
>  L'opzione `/linkresource` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice che segue compila `In.vb` e crea un collegamento al file di risorse `Rf.resource`.  
  
```  
vbc /linkresource:rf.resource in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [\/resource](../../../visual-basic/reference/command-line-compiler/resource.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)