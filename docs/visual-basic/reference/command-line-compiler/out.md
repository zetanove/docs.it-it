---
title: /out (Visual Basic) | Documenti di Microsoft
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
- /out compiler option [Visual Basic]
- -out compiler option [Visual Basic]
- out compiler option [Visual Basic]
ms.assetid: 9f148c15-0909-4cb8-a2db-777f8a8b45ae
caps.latest.revision: 17
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: e3eb7af88869e4fb161a12914c02f2bc2f41864e
ms.lasthandoff: 03/13/2017

---
# <a name="out-visual-basic"></a>/out (Visual Basic)
Specifica il nome del file di output.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/out:filename  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`filename`|Obbligatorio. Il nome del file di output, che il compilatore crea. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette ("").|  
  
## <a name="remarks"></a>Note  
 Specificare il nome completo e l'estensione del file da creare. In caso contrario, il file .exe lo stesso nome file del codice sorgente che contiene il `Sub Main` procedure e il file DLL prende il nome del primo file di codice sorgente.  
  
 Se si specifica un nome di file senza estensione .exe o. dll, il compilatore aggiunge automaticamente l'estensione, a seconda del valore specificato per il `/target` l'opzione del compilatore.  
  
|Per impostare /out nell'ambiente di sviluppo integrato di Visual Studio|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Applicazione** .<br />3.  Modificare il valore di **nome Assembly** casella.|  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` e crea file di output `T2.exe`.  
  
```  
vbc t2.vb /out:t3.exe  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
