---
title: 'Impossibile creare l&quot;assembly: &lt;messaggio di errore&gt; | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30145
- bc30145
dev_langs:
- VB
helpviewer_keywords:
- BC30145
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
caps.latest.revision: 11
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
ms.openlocfilehash: dac4b133882c043f9c84e936bad2e36f35fc4c33
ms.lasthandoff: 03/13/2017

---
# <a name="unable-to-emit-assembly-lterror-messagegt"></a>Impossibile creare l'assembly: &lt;messaggio di errore&gt;
Il compilatore di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] chiama Assembly Linker (Al.exe, definito anche Alink) per generare un assembly con un manifesto e il linker segnala un errore nella fase di emissione della creazione dell'assembly.  
  
 **ID errore:** BC30145  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Esaminare il messaggio di errore riportato e vedere l'argomento [Al.exe errori e avvisi](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b) per ulteriori spiegazioni e consigli.  
  
2.  Provare a firmare l'assembly manualmente, utilizzando il [Assembly Linker (Al.exe)](https://msdn.microsoft.com/library/c405shex) o [Sn.exe (strumento nome sicuro)](https://msdn.microsoft.com/library/k5b5tt23).  
  
3.  Se l'errore persiste, raccogliere informazioni sulla situazione contingente e informare il Servizio Supporto Tecnico Clienti Microsoft.  
  
### <a name="to-sign-the-assembly-manually"></a>Per firmare manualmente l'assembly  
  
1.  Utilizzare il [Sn.exe (strumento nome sicuro)](https://msdn.microsoft.com/library/k5b5tt23) per creare un file di coppia di chiavi pubblica/privata.  
  
     L'estensione di questo file è .snk.  
  
2.  Eliminare il riferimento COM che genera l'errore dal progetto.  
  
3.  Da Windows **avviare** dal menu **programmi**, scegliere **Microsoft Visual Studio 2008**, scegliere **Visual Studio Tools**, quindi fare clic su **Prompt dei comandi di Visual Studio 2008**.  
  
4.  Passare alla directory in cui si desidera posizionare il wrapper dell'assembly.  
  
5.  Digitare il codice seguente.  
  
    ```  
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>  
    ```  
  
     Il codice da digitare potrebbe essere simile al seguente.  
  
    ```  
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"  
    ```  
  
     Se contiene spazi, il file o il percorso deve essere racchiuso tra virgolette doppie (").  
  
6.  In [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] aggiungere un riferimento assembly .NET al file appena creato.  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly Linker (Al.exe)](https://msdn.microsoft.com/library/c405shex)   
 [Strumento Al.exe errori e avvisi](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Sn.exe (strumento nome sicuro)](https://msdn.microsoft.com/library/k5b5tt23)   
 [Procedura: Creare una coppia di chiavi pubblica/privata](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)   
 [Comunicazioni con Microsoft](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
