---
title: /Resource (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- /resource compiler option [Visual Basic]
- -resource compiler option [Visual Basic]
- /res compiler option [Visual Basic]
- res compiler option [Visual Basic]
- -res compiler option [Visual Basic]
- resource compiler option [Visual Basic]
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
caps.latest.revision: 19
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b46800322fd03eb2578cc558cc1d9bb78550aa61
ms.lasthandoff: 03/13/2017

---
# <a name="resource-visual-basic"></a>/resource (Visual Basic)
Incorpora una risorsa gestita in un assembly.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/resource:filename[,identifier[,public|private]]  
' -or-  
/res:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`filename`|Obbligatorio. Il nome del file di risorse da incorporare nel file di output. Per impostazione predefinita, `filename` è pubblico nell'assembly. Racchiudere il nome del file tra virgolette ("") se contiene uno spazio.|  
|`identifier`|Facoltativo. Il nome logico per la risorsa. il nome utilizzato per caricarla. Il valore predefinito è il nome del file. Facoltativamente, è possibile specificare se la risorsa è pubblica o privata nel manifesto dell'assembly, come le operazioni seguenti: `/res:``filename.res`,`myname.res`,`public`|  
  
## <a name="remarks"></a>Note  
 Utilizzare `/linkresource` per collegare una risorsa a un assembly senza inserire il file di risorse nel file di output.  
  
 Se `filename` è un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] file di risorse creato, ad esempio, mediante il [Resgen.exe (Generatore di File di risorse)](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4) o nell'ambiente di sviluppo, sono accessibili tramite i membri di <xref:System.Resources>dello spazio dei nomi (vedere <xref:System.Resources.ResourceManager>Per ulteriori informazioni).</xref:System.Resources.ResourceManager> </xref:System.Resources> Per accedere a tutte le altre risorse in fase di esecuzione, utilizzare uno dei metodi seguenti: <xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>, <xref:System.Reflection.Assembly.GetManifestResourceNames%2A>, o <xref:System.Reflection.Assembly.GetManifestResourceStream%2A>.</xref:System.Reflection.Assembly.GetManifestResourceStream%2A> </xref:System.Reflection.Assembly.GetManifestResourceNames%2A> </xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>  
  
 La versione abbreviata di `/resource` è `/res`.  
  
 Per informazioni su come impostare `/resource` nell'IDE di Visual Studio, vedere [risorse dell'applicazione di gestione (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-resources-dotnet).  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `In.vb` e consente di collegare file di risorse `Rf.resource`.  
  
```  
vbc /res:rf.resource in.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)   
 [/linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
