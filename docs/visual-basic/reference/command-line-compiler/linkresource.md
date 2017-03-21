---
title: /linkresource (Visual Basic) | Documenti di Microsoft
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
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
caps.latest.revision: 16
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fafde6563340189108a879b82e7e880aca690b39
ms.lasthandoff: 03/13/2017

---
# <a name="linkresource-visual-basic"></a>/linkresource (Visual Basic)
Crea un collegamento a una risorsa gestita.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/linkresource:filename[,identifier[,public|private]]  
' -or-  
/linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>Argomenti  
 `filename`  
 Obbligatorio. File di risorse da collegare all'assembly. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette ("").  
  
 `identifier`  
 Facoltativo. Nome logico per la risorsa. Il nome utilizzato per caricare la risorsa. Il valore predefinito è il nome del file. Facoltativamente, è possibile specificare se il file è pubblico o privato nel manifesto dell'assembly, ad esempio: `/linkres:filename.res,myname.res,public`. Per impostazione predefinita, `filename` è pubblico nell'assembly.  
  
## <a name="remarks"></a>Note  
 Il `/linkresource` opzione consente di incorporare il file di risorse nel file di output, utilizzare il `/resource` opzione per eseguire questa operazione.  
  
 Il `/linkresource` necessaria un'opzione di `/target` diversa da `/target:module`.  
  
 Se `filename` è un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] file di risorse creato, ad esempio, mediante il [Resgen.exe (Generatore di File di risorse)](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4) o nell'ambiente di sviluppo, sono accessibili tramite i membri di <xref:System.Resources>dello spazio dei nomi.</xref:System.Resources> (Per ulteriori informazioni, vedere <xref:System.Resources.ResourceManager>.)</xref:System.Resources.ResourceManager> Per accedere a tutte le altre risorse in fase di esecuzione, utilizzare i metodi che iniziano con `GetManifestResource` nella <xref:System.Reflection.Assembly>classe.</xref:System.Reflection.Assembly>  
  
 Il nome del file può avere qualsiasi formato di file. Ad esempio, è consigliabile includere una DLL nativa dell'assembly, in modo che possa essere installato nella global assembly cache e accedervi dal codice gestito nell'assembly.  
  
 La versione abbreviata di `/linkresource` è `/linkres`.  
  
> [!NOTE]
>  Il `/linkresource` opzione non è disponibile dall'ambiente di sviluppo Visual Studio, è disponibile solo quando si compila dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `In.vb` e collegamenti a file di risorse `Rf.resource`.  
  
```  
vbc /linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [/Resource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
