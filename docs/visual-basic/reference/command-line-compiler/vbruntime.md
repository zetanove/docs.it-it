---
title: /vbruntime | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbruntime
- /vbruntime
dev_langs:
- VB
helpviewer_keywords:
- vbruntime compiler option [Visual Basic]
- -vbruntime compiler option [Visual Basic]
- /vbruntime compiler option [Visual Basic]
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
caps.latest.revision: 17
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
ms.openlocfilehash: 455f950988b540b74874ce38882c59059f77ea8f
ms.lasthandoff: 03/13/2017

---
# <a name="vbruntime"></a>/vbruntime
Indica che il compilatore deve compilare senza un riferimento alla libreria di runtime di Visual Basic oppure con un riferimento a una libreria di runtime specifica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/vbruntime:{ - | + | * | path }  
```  
  
## <a name="arguments"></a>Argomenti  
 \-  
 Compilare senza un riferimento alla libreria di Runtime di Visual Basic.  
  
 \+  
 Esegue la compilazione con un riferimento per il valore predefinito della libreria di Runtime di Visual Basic.  
  
 \*  
 La compilazione senza un riferimento alla libreria di Runtime di Visual Basic e incorpora le funzionalità principali dalla libreria di Runtime di Visual Basic in un assembly.  
  
 `path`  
 Esegue la compilazione con un riferimento alla libreria (DLL) specificato.  
  
## <a name="remarks"></a>Note  
 Il `/vbruntime` l'opzione del compilatore consente di specificare che il compilatore esegue la compilazione senza un riferimento alla libreria di Runtime di Visual Basic. Se esegue la compilazione senza un riferimento alla libreria di Runtime di Visual Basic, errori o avvisi vengono registrati in costrutti di linguaggio o codice che generano una chiamata a un supporto di runtime di Visual Basic. (A *helper di runtime di Visual Basic* è una funzione definita in Microsoft.VisualBasic.dll che viene chiamato in fase di esecuzione per eseguire una semantica di linguaggio specifica.)  
  
 Il `/vbruntime+` opzione produce lo stesso comportamento che si verifica quando non `/vbruntime` viene specificata l'opzione. È possibile utilizzare il `/vbruntime+` opzione per eseguire l'override precedente `/vbruntime` commutatori.  
  
 Maggior parte degli oggetti di `My` tipo non sono disponibili quando si utilizza il `/vbruntime-` o `vbruntime:``path` opzioni.  
  
## <a name="embedding-visual-basic-runtime-core-functionality"></a>Incorporare funzionalità di base di Runtime di Visual Basic  
 Il `/vbruntime*` consente di eseguire la compilazione senza un riferimento a una libreria di runtime. Al contrario, la funzionalità di base dalla libreria di Runtime di Visual Basic è incorporata nell'assembly utente. È possibile utilizzare questa opzione se l'applicazione viene eseguita su piattaforme che non contengono il runtime di Visual Basic.  
  
 I membri di runtime seguenti sono incorporati:  
  
-   <xref:Microsoft.VisualBasic.CompilerServices.Conversions>classe</xref:Microsoft.VisualBasic.CompilerServices.Conversions>  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29>metodo</xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29>  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29>metodo</xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29>  
  
-   <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29>metodo</xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbBack>(costante)</xref:Microsoft.VisualBasic.Constants.vbBack>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCr>(costante)</xref:Microsoft.VisualBasic.Constants.vbCr>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCrLf>(costante)</xref:Microsoft.VisualBasic.Constants.vbCrLf>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbFormFeed>(costante)</xref:Microsoft.VisualBasic.Constants.vbFormFeed>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbLf>(costante)</xref:Microsoft.VisualBasic.Constants.vbLf>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNewLine>(costante)</xref:Microsoft.VisualBasic.Constants.vbNewLine>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullChar>(costante)</xref:Microsoft.VisualBasic.Constants.vbNullChar>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullString>(costante)</xref:Microsoft.VisualBasic.Constants.vbNullString>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbTab>(costante)</xref:Microsoft.VisualBasic.Constants.vbTab>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbVerticalTab>(costante)</xref:Microsoft.VisualBasic.Constants.vbVerticalTab>  
  
-   Alcuni oggetti del `My` tipo  
  
 Se si esegue la compilazione utilizzando il `/vbruntime*` opzione e il codice fa riferimento a un membro dalla libreria di Runtime di Visual Basic che non sono incorporati con le funzionalità di base, il compilatore restituisce un errore che indica che il membro non è disponibile.  
  
## <a name="referencing-a-specified-library"></a>Riferimento a una libreria specificata  
 È possibile utilizzare il `path` argomento per la compilazione con un riferimento a una libreria di runtime personalizzato anziché il valore predefinito della libreria di Runtime di Visual Basic.  
  
 Se il valore per il `path` argomento è un percorso completo di una DLL, il compilatore utilizzerà quel file come libreria di runtime. Se il valore per il `path` argomento non è un percorso completo di una DLL, il compilatore Visual Basic cercherà la DLL identificata nella cartella corrente prima. Quindi, la cercherà nel percorso specificato utilizzando il [/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md) l'opzione del compilatore. Se il `/sdkpath` l'opzione del compilatore non viene utilizzato, il compilatore effettuerà la ricerca per la DLL identificata nella cartella di .NET Framework (`%systemroot%\Microsoft.NET\Framework\versionNumber`).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il `/vbruntime` opzione di compilazione con un riferimento a una libreria personalizzata.  
  
```  
vbc /vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Core di Visual Basic-nuova modalità di compilazione in Visual Studio 2010 SP1](http://blogs.msdn.com/b/vbteam/archive/2011/01/10/vb-core-new-compilation-mode-in-visual-studio-2010-sp1.aspx)   
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
