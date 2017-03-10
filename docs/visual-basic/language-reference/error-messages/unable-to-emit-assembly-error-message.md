---
title: "Unable to emit assembly: &lt;error message&gt; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30145"
  - "bc30145"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30145"
ms.assetid: 2e7eb2b9-eda6-4bdb-95cc-72c7f0be7528
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Unable to emit assembly: &lt;error message&gt;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il compilatore di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] chiama Assembly Linker \(Al.exe, definito anche Alink\) per generare un assembly con un manifesto e il linker segnala un errore nella fase di emissione della creazione dell'assembly.  
  
 **ID errore:** BC30145  
  
### Per correggere l'errore  
  
1.  Esaminare il messaggio di errore riportato e vedere l'argomento [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/it-it/7f125d49-0a03-47a6-9ba9-d61a679a7d4b) per spiegazioni e suggerimenti aggiuntivi.  
  
2.  Provare a firmare manualmente l'assembly, usando [Al.exe \(Assembly Linker\)](../Topic/Al.exe%20\(Assembly%20Linker\).md) o [Sn.exe \(Strong Name Tool\)](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md).  
  
3.  Se l'errore persiste, raccogliere informazioni sulla situazione contingente e informare il Servizio Supporto Tecnico Clienti Microsoft.  
  
### Per firmare manualmente l'assembly  
  
1.  Usare [Sn.exe \(Strong Name Tool\)](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md) per creare un file di coppia di chiavi pubblica\/privata.  
  
     L'estensione di questo file è .snk.  
  
2.  Eliminare il riferimento COM che genera l'errore dal progetto.  
  
3.  Dal menu **Start** di Windows, scegliere **Programmi**, **Microsoft Visual Studio 2008**, **Strumenti di Visual Studio** e infine **Prompt dei comandi di Visual Studio 2008**.  
  
4.  Passare alla directory in cui si desidera posizionare il wrapper dell'assembly.  
  
5.  Digitare il codice seguente.  
  
    ```  
    tlbimp <path to COM reference file> /out:<output assembly name> /keyfile:<path to .snk file>  
    ```  
  
     Il codice da digitare potrebbe essere simile al seguente.  
  
    ```  
    tlbimp c:\windows\system32\msi.dll /out:Interop.WindowsInstaller.dll /keyfile:"c:\documents and settings\mykey.snk"  
    ```  
  
     Se contiene spazi, il file o il percorso deve essere racchiuso tra virgolette doppie \("\).  
  
6.  In [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] aggiungere un riferimento assembly .NET al file appena creato.  
  
## Vedere anche  
 [Al.exe \(Assembly Linker\)](../Topic/Al.exe%20\(Assembly%20Linker\).md)   
 [Al.exe Tool Errors and Warnings](http://msdn.microsoft.com/it-it/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [Sn.exe \(Strong Name Tool\)](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)   
 [Procedura: creare una coppia di chiavi pubblica\/privata](../Topic/How%20to:%20Create%20a%20Public-Private%20Key%20Pair.md)   
 [Comunicazioni con Microsoft](/visual-studio/ide/talk-to-us)