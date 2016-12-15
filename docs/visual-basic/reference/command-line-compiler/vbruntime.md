---
title: "/vbruntime | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbruntime"
  - "/vbruntime"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "vbruntime compiler option [Visual Basic]"
  - "-vbruntime compiler option [Visual Basic]"
  - "/vbruntime compiler option [Visual Basic]"
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /vbruntime
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Indica che il compilatore esegue la compilazione senza un riferimento alla libreria di runtime di Visual Basic oppure con un riferimento a una libreria di runtime specifica.  
  
## Sintassi  
  
```  
/vbruntime:{ - | + | * | path }  
```  
  
## Argomenti  
 \-  
 Compila senza un riferimento alla libreria di runtime di Visual Basic.  
  
 \+  
 Compila con un riferimento alla libreria di runtime di Visual Basic predefinita.  
  
 \*  
 Compila senza un riferimento alla Libreria di runtime di Visual Basic e incorpora le funzionalità principali della Libreria di runtime di Visual Basic nell'assembly.  
  
 `path`  
 Compila con un riferimento alla libreria \(DLL\) specificata.  
  
## Note  
 L'opzione del compilatore `/vbruntime` consente di specificare che il compilatore esegue la compilazione senza un riferimento alla libreria di runtime di Visual Basic.  Se si compila senza un riferimento alla libreria di runtime di Visual Basic, gli errori o gli avvisi vengono registrati su costrutti di linguaggio o di codice che generano una chiamata a un helper di runtime di Visual Basic.  L' *helper di runtime di Visual Basic* è una funzione definita in Microsoft.VisualBasic.dll che viene chiamata in fase di esecuzione per eseguire una semantica di linguaggio specifica.  
  
 L'opzione `/vbruntime+` produce lo stesso comportamento che si verifica quando non si specifica alcuna opzione `/vbruntime`.  È possibile utilizzare l'opzione `/vbruntime+` per eseguire l'override di opzioni `/vbruntime` precedenti.  
  
 La maggior parte degli oggetti del tipo di `My` non sono disponibili quando si utilizza `/vbruntime-` o le opzioni di `vbruntime:``path` .  
  
## Incorporamento delle funzionalità di base del runtime di Visual Basic  
 L'opzione `/vbruntime*` consente di eseguire la compilazione senza un riferimento a una libreria di runtime.  Al contrario, la funzionalità principale della libreria di runtime di Visual Basic è incorporata nell'assembly utente.  È possibile utilizzare questa opzione se l'applicazione viene eseguita su piattaforme che non contengono il runtime di Visual Basic.  
  
 I seguenti membri di runtime sono incorporati:  
  
-   Classe <xref:Microsoft.VisualBasic.CompilerServices.Conversions>  
  
-   Metodo <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29>  
  
-   Metodo <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29>  
  
-   Metodo <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbBack>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbCr>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbCrLf>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbFormFeed>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbLf>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbNewLine>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbNullChar>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbNullString>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbTab>  
  
-   Costante <xref:Microsoft.VisualBasic.Constants.vbVerticalTab>  
  
-   Alcuni oggetti del tipo di `My`  
  
 Se si esegue la compilazione utilizzando l'opzione `/vbruntime*` e il codice fa riferimento a un membro dalla libreria di runtime di Visual Basic che non è incorporata con la funzionalità principale, tramite il compilatore viene restituito un errore che indica che il membro non è disponibile.  
  
## Riferimento a una libreria specificata  
 L'argomento `path` può essere utilizzato per compilare con un riferimento a una libreria di runtime personalizzata invece della libreria di runtime di Visual Basic predefinita.  
  
 Se il valore per l'argomento `path` è un percorso completo di una DLL, il compilatore utilizzerà quel file come libreria di runtime.  Se il valore per l'argomento `path` non è il percorso completo di una DLL, il compilatore Visual Basic per prima cosa cercherà la DLL identificata nella cartella corrente.  Quindi, la cercherà nel percorso specificato mediante l'opzione [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md) del compilatore.  Se questa opzione non è utilizzata, il compilatore cercherà la DLL identificata nella cartella di .NET Framework \(`%systemroot%\Microsoft.NET\Framework\versionNumber`\).  
  
## Esempio  
 Nell'esempio seguente è indicato come utilizzare l'opzione `/vbruntime` per compilare con un riferimento a una libreria personalizzata.  
  
```  
vbc /vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## Vedere anche  
 [Core Visual Basic \- Nuova modalità di compilazione in Visual Studio 2010 SP1](http://blogs.msdn.com/b/vbteam/archive/2011/01/10/vb-core-new-compilation-mode-in-visual-studio-2010-sp1.aspx)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)