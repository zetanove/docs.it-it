---
title: "/libpath | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "libpath compiler option [Visual Basic]"
  - "/libpath compiler option [Visual Basic]"
  - "-libpath compiler option [Visual Basic]"
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /libpath
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica il percorso degli assembly a cui si fa riferimento.  
  
## Sintassi  
  
```  
/libpath:dirList  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`dirList`|Obbligatorio.  Elenco di directory separate da punto e virgola in cui il compilatore può effettuare la ricerca se un assembly cui viene fatto riferimento non si trova nella cartella di lavoro corrente, ovvero la cartella da cui si richiama il compilatore, o nella directory di sistema di Common Language Runtime.  Se il nome della directory contiene uno spazio, racchiudere il nome tra virgolette \(" "\).|  
  
## Note  
 L'opzione `/libpath` specifica il percorso degli assembly a cui viene fatto riferimento dall'opzione [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md).  
  
 La ricerca dei riferimenti non completi agli assembly viene operata nel seguente ordine:  
  
1.  Directory di lavoro corrente,  ovvero la directory da cui viene richiamato il compilatore.  
  
2.  Directory di sistema di Common Language Runtime.  
  
3.  Directory specificate da `/libpath`.  
  
4.  Directory specificate dalla variabile di ambiente LIB.  
  
 `/libpath` è un'opzione aggiuntiva che, se specificata più volte, determina l'aggiunta di ogni nuovo valore a eventuali valori precedenti.  
  
 Per specificare un riferimento a un assembly, utilizzare `/reference`.  
  
||  
|-|  
|Per impostare \/libpath nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Riferimenti**.<br />3.  Fare clic sul pulsante **Percorsi riferimento...**.<br />4.  Immettere il nome della directory nella casella **Cartella:** della finestra di dialogo **Percorsi riferimento**.<br />5.  Fare clic su **Aggiungi cartella**.|  
  
## Esempio  
 Il codice riportato di seguito compila `T2.vb` per creare un file exe.  Il compilatore cercherà i riferimenti agli assembly nella cartella di lavoro, nella directory radice e nella directory New Assemblies dell'unità C.  
  
```  
vbc /libpath:c:\;"c:\New Assemblies" /reference:t2.dll t2.vb  
```  
  
## Vedere anche  
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)