---
title: "/target (Visual Basic) | Microsoft Docs"
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
  - "target compiler options [Visual Basic]"
  - "-target compiler options [Visual Basic]"
  - "/target compiler options [Visual Basic]"
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# /target (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica il formato dell'output del compilatore.  
  
## Sintassi  
  
```  
/target:{exe | library | module | winexe | appcontainerexe | winmdobj}  
```  
  
## Note  
 Nella tabella riportata di seguito viene fornito un riepilogo dei risultati ottenuti utilizzando l'opzione `/target`.  
  
|**Opzione**|**Comportamento**|  
|-----------------|-----------------------|  
|`/target:exe`|Determina la creazione di un'applicazione console eseguibile da parte del compilatore.<br /><br /> Si tratta dell'impostazione predefinita quando non sono specificate opzioni `/target`.  Il file eseguibile creato avrà estensione exe.<br /><br /> Se non diversamente specificato mediante l'opzione `/out`, il nome del file di output corrisponde al nome del file di input che contiene la routine `Sub Main`.<br /><br /> Nei file di codice sorgente che vengono compilati in un file exe è necessaria un'unica routine `Sub Main`.  Utilizzare l'opzione del compilatore `/main` per specificare la classe che contiene la routine `Sub Main`.|  
|`/target:library`|Determina la creazione di una libreria a collegamento dinamico \(DLL\) da parte del compilatore.<br /><br /> La libreria a collegamento dinamico creata avrà estensione dll.<br /><br /> Se non diversamente specificato mediante l'opzione `/out`, il nome del file di output corrisponde al nome del primo file di input.<br /><br /> Per la compilazione di una DLL non è richiesta una routine `Sub Main`.|  
|`/target:module`|Determina la generazione di un modulo che può essere aggiunto a un assembly.<br /><br /> Il file di output verrà creato con un'estensione .  netmodule.<br /><br /> .NET Common Language Runtime non consente il caricamento di un file che non dispone di un assembly.  È possibile tuttavia incorporare tale file nel manifesto assembly di un assembly mediante `/reference`.<br /><br /> Quando il codice di un modulo fa riferimento ai tipi interni di un altro modulo, è necessario incorporare entrambi i moduli in un manifesto assembly mediante l'opzione `/reference`.<br /><br /> L'opzione [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) consente di importare metadati da un modulo.|  
|`/target:winexe`|Determina la creazione di un programma eseguibile \(EXE\) basato su Windows.<br /><br /> Il file eseguibile creato avrà estensione exe.  Per programma basato su Windows si intende un'applicazione che fornisce un'interfaccia utente dalla libreria di classi [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] o con le API Win32.<br /><br /> Se non diversamente specificato mediante l'opzione `/out`, il nome del file di output corrisponde al nome del file di input che contiene la routine `Sub Main`.<br /><br /> Nei file di codice sorgente che vengono compilati in un file exe è necessaria un'unica routine `Sub Main`.  Se nel codice sono presenti più classi contenenti una routine `Sub Main`, utilizzare l'opzione del compilatore `/main` per specificare la classe che contiene `Sub Main`.|  
|`/target:appcontainerexe`|Indica al compilatore di creare un eseguibile applicazioni basate su Windows che deve essere eseguito in un contenitore di app.  Questa impostazione è progettata per essere utilizzata per le applicazioni [!INCLUDE[win8_appname_long](../../../csharp/includes/win8-appname-long-md.md)].<br /><br /> **appcontainerexe** che imposta imposta un bit nel [Eseguibile portabile](http://go.microsoft.com/fwlink/p/?LinkId=236960) campo di caratteristiche.  Questo bit è indicato che l'applicazione deve essere eseguita in un contenitore di app.  Quando questo bit è impostato, viene generato un errore se il metodo `CreateProcess` tenta di avviare l'applicazione all'esterno di un contenitore di app.  Oltre a questa impostazione di bit, **\/target:appcontainerexe** equivale a **\/target:winexe**.<br /><br /> Il file eseguibile creato avrà estensione exe.<br /><br /> Se non diversamente specificato utilizzando l'opzione `/out`, il nome file di output accetta il nome del file di input contenente la routine `Sub Main`.<br /><br /> Nei file di codice sorgente che vengono compilati in un file exe è necessaria un'unica routine `Sub Main`.  Se il codice contiene più di uno classe con una routine `Sub Main`, utilizzare l'opzione del compilatore `/main` specificare che la classe contiene la routine `Sub Main`|  
|`/target:winmdobj`|Indica al compilatore di creare un file temporaneo che è possibile convertire in un file binario di Windows Runtime \(.winmd\).  Il file di .winmd può essere utilizzato dai programmi C\+\+ e JavaScript, oltre ai programmi gestiti di linguaggio.<br /><br /> Il file intermedio viene creato con estensione .winmdobj.<br /><br /> Se non diversamente specificato utilizzando l'opzione `/out`, il nome file di output accetta il nome del primo file di input.  Una routine `Sub Main` non è necessaria.<br /><br /> Il file di .winmdobj è progettato per essere utilizzato come input per lo strumento di esportazione <xref:Microsoft.Build.Tasks.WinMDExp> scrivere un file di metadati di Windows \(WinMD\).  Il file di WinMD con estensione .winmd e contiene sia il codice dalla raccolta originale e le definizioni di WinMD che JavaScript, C\+\+ e l'utilizzo di Windows Runtime.|  
  
 A meno che non sia specificato `/target:module`, l'opzione `/target` determina l'aggiunta di un manifesto assembly di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] in un file di output.  
  
 Per ciascuna istanza di Vbc.exe viene prodotto al massimo un file di output.  Se un'opzione del compilatore quale `/out` o `/target` viene specificata più volte, verrà attivata solo l'ultima elaborata dal compilatore.  Nel manifesto vengono aggiunte le informazioni relative a tutti i file della compilazione.  Nel manifesto di tutti i file di output, a eccezione di quelli creati con l'opzione `/target:module`, sono presenti metadati assembly.  Per visualizzare i metadati di un file di output, utilizzare il [Ildasm.exe \(IL Disassembler\)](../Topic/Ildasm.exe%20\(IL%20Disassembler\).md).  
  
 La forma breve di `/target` è `/t`.  
  
### Per impostare \/target nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Applicazione**.  
  
3.  Modificare il valore della casella **Tipo di applicazione**.  
  
## Esempio  
 Il codice seguente consente di compilare `in.vb`, creando `in.dll`:  
  
```  
vbc /target:library in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [\/out](../../../visual-basic/reference/command-line-compiler/out.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)   
 [\/moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)   
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)