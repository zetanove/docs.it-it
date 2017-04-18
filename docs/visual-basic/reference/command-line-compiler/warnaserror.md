---
title: /warnaserror (Visual Basic) | Documenti di Microsoft
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
- warnaserror compiler option [Visual Basic]
- /warnaserror compiler option [Visual Basic]
- -warnaserror compiler option [Visual Basic]
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
caps.latest.revision: 18
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
ms.openlocfilehash: 28f232b1ad8200455550f2f4c1204818c8b143ab
ms.lasthandoff: 03/13/2017

---
# <a name="warnaserror-visual-basic"></a>/warnaserror (Visual Basic)
Indica al compilatore di considerare la prima occorrenza di un avviso come errore.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/warnaserror[+ | -][:numberList]  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|+ &#124; -|Facoltativo. Per impostazione predefinita, `/warnaserror-` è attivo, gli avvisi non impediscono il compilatore dalla produzione di un file di output. Il `/warnaserror` opzione, ovvero lo stesso come `/warnaserror+`, gli avvisi vengono considerati come errori.|  
|`numberList`|Facoltativo. Elenco delimitato da virgole di ID di avviso di numeri a cui il `/warnaserror` opzione si applica. Se è specificato alcun ID avviso, il `/warnaserror` opzione si applica a tutti gli avvisi.|  
  
## <a name="remarks"></a>Note  
 Il `/warnaserror` opzione Considera tutti gli avvisi come errori. I messaggi che verranno in genere segnalati come avvisi vengono invece segnalati come errori. Il compilatore segnala le occorrenze successive dello stesso avviso come avvisi.  
  
 Per impostazione predefinita, `/warnaserror-` è attiva, pertanto gli avvisi per essere esclusivamente informativi. Il `/warnaserror` opzione, ovvero lo stesso come `/warnaserror+`, gli avvisi vengono considerati come errori.  
  
 Se si desidera che solo determinati avvisi vengano considerati errori, è possibile specificare un elenco delimitato da virgole dei numeri degli avvisi da considerare come errori.  
  
> [!NOTE]
>  Il `/warnaserror` opzione controlla la modalità di visualizzazione degli avvisi. Utilizzare il [/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md) opzione per disattivare gli avvisi.  
  
|Per impostare /warnaserror considerare tutti gli avvisi come errori nell'IDE di Visual Studio|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **Project** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Assicurarsi che il **Disabilita tutti gli avvisi** casella di controllo è deselezionata.<br />4.  Controllare il **considera tutti gli avvisi come errori** casella di controllo.|  
  
|Per impostare /warnaserror specifici avvisi vengano considerati come errori nell'IDE di Visual Studio|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **Project** menu, fare clic su **proprietà**.<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Assicurarsi che il **Disabilita tutti gli avvisi** casella di controllo è deselezionata.<br />4.  Assicurarsi che il **considera tutti gli avvisi come errori** casella di controllo è deselezionata.<br />5.  Selezionare **errore** dal **notifica** colonna adiacente all'avviso che deve essere considerato come un errore.|  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `In.vb` viene visualizzato un errore per la prima occorrenza di ogni avviso generato.  
  
```  
vbc /warnaserror in.vb  
```  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` e viene considerato come un errore solo l'avviso per le variabili locali inutilizzate (42024).  
  
```  
vbc /warnaserror:42024 t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)
