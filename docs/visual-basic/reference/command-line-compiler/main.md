---
title: /Main | Documenti di Microsoft
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
- main compiler option [Visual Basic]
- /main compiler option [Visual Basic]
- -main compiler option [Visual Basic]
ms.assetid: 83fc339d-6652-415d-b205-b5133319b5b0
caps.latest.revision: 19
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
ms.openlocfilehash: dded7621845141896f353d69ab757010c825b975
ms.lasthandoff: 03/13/2017

---
# <a name="main"></a>/main
Specifica la classe o un modulo che contiene il `Sub Main` procedura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/main:location  
```  
  
## <a name="arguments"></a>Argomenti  
 `location`  
 Obbligatorio. Nome completo della classe o del modulo che contiene il `Sub Main` routine da chiamare all'avvio del programma. Può essere nel formato **/main:module** o **/Main**.  
  
## <a name="remarks"></a>Note  
 Utilizzare questa opzione quando si crea un file eseguibile o un programma eseguibile di Windows. Se il **/principale** opzione viene omessa, il compilatore cerca condiviso valido `Sub Main` in tutte le classi pubbliche e moduli.  
  
 Vedere [routine Main in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md) per una descrizione delle varie forme di `Main` procedura.  
  
 Quando `location` è una classe che eredita da <xref:System.Windows.Forms.Form>, il compilatore fornisce un valore predefinito `Main` routine che avvia l'applicazione se la classe non ha `Main` procedura.</xref:System.Windows.Forms.Form> Ciò consente di compilare il codice dalla riga di comando che è stata creata nell'ambiente di sviluppo.  
  
 [!code-vb[VbVbalrCompiler&#16;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/main_1.vb)]  
  
### <a name="to-set-main-in-the-visual-studio-integrated-development-environment"></a>Per impostare /main in Visual Studio ambiente di sviluppo integrato  
  
1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**.  
  
     Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Applicazione** .  
  
3.  Assicurarsi che il **Attiva framework applicazione** casella di controllo è deselezionata.  
  
4.  Modificare il valore di **oggetto di avvio** casella.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` e `T3.vb`, specificando che il `Sub Main` routine è reperibile nella `Test2` classe.  
  
```  
vbc t2.vb t3.vb /main:Test2  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [NIB: versione di Visual Basic di Hello, World](http://msdn.microsoft.com/en-us/9d030b60-e148-4366-a462-69532f02294c)   
 [Routine Main in Visual Basic](../../../visual-basic/programming-guide/program-structure/main-procedure.md)
