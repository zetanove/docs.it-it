---
title: "Winmdexp.exe (Windows Runtime Metadata Export Tool) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Windows Runtime Metadata Export Tool"
  - "Winmdexp.exe"
ms.assetid: d2ce0683-343d-403e-bb8d-209186f7a19d
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Winmdexp.exe (Windows Runtime Metadata Export Tool)
Lo strumento di esportazione dei metadati di [!INCLUDE[wrt](../../../includes/wrt-md.md)] \(Winmdexp.exe\) trasforma un modulo .NET Framework in un file che contiene metadati di [!INCLUDE[wrt](../../../includes/wrt-md.md)].  Anche se gli assembly .NET Framework e i file di metadati di [!INCLUDE[wrt](../../../includes/wrt-md.md)] utilizzano lo stesso formato fisico, esistono differenze nel contenuto delle tabelle dei metadati, con la conseguenza che gli assembly .NET Framework non sono automaticamente utilizzabili come componenti di [!INCLUDE[wrt](../../../includes/wrt-md.md)].  Il processo di trasformazione di un modulo .NET Framework in un componente di [!INCLUDE[wrt](../../../includes/wrt-md.md)] è denominato *esportazione*.  In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] il file di metadati di Windows \(.winmd\) risultante contiene sia i metadati che l'implementazione.  
  
 Quando si utilizza il modello **Componente di [!INCLUDE[wrt](../../../includes/wrt-md.md)]**, che si trova in **Windows Store** per C\# e Visual Basic in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] o in [!INCLUDE[vs_dev11_ext](../../../includes/vs-dev11-ext-md.md)], la destinazione del compilatore è un file .winmdobj; una successiva istruzione di compilazione chiama Winmdexp.exe per esportare il file .winmdobj in un file .winmd.  Questo è il modo consigliato di compilare un componente di [!INCLUDE[wrt](../../../includes/wrt-md.md)].  Utilizzare direttamente Winmdexp.exe quando si desidera un maggiore controllo sul processo di compilazione rispetto a quello offerto da Visual Studio.  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, utilizzare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per ulteriori informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
winmdexp [options] winmdmodule  
```  
  
#### Parametri  
  
|Argomento o opzione|Descrizione|  
|-------------------------|-----------------|  
|`winmdmodule`|Specifica il modulo \(.winmdobj\) da esportare.  È consentito un solo modulo.  Per creare questo modulo, utilizzare l'opzione del compilatore `/target` con destinazione `winmdobj`.  Vedere [\/target:winmdobj \(creare un file intermedio per Windows Runtime\)](../Topic/-target:winmdobj%20\(C%23%20Compiler%20Options\).md) or [\/target](../Topic/-target%20\(Visual%20Basic\).md) in MSDN Library.|  
|`/docfile:` `docfile`<br /><br /> `/d:` `docfile`|Specifica il file di documentazione XML di output che verrà prodotto da Winmdexp.exe.  In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] il file di output è sostanzialmente lo stesso file di documentazione XML di input.|  
|`/moduledoc:` `docfile`<br /><br /> `/md:` `docfile`|Specifica il nome del file di documentazione XML che il compilatore ha creato con `winmdmodule`.|  
|`/modulepdb:` `symbolfile`<br /><br /> `/mp:` `symbolfile`|Specifica il nome del file del database di programma \(PDB\) contenente i simboli per `winmdmodule`.|  
|`/nowarn:` `warning`|Non visualizza il numero di avviso specificato.  Per *warning*, fornire solo la parte numerica del codice di errore, senza zeri iniziali.|  
|`/out:` `file`<br /><br /> `/o:` `file`|Specifica il nome del file di metadati di Windows \(.winmd\) di output.|  
|`/pdb:` `symbolfile`<br /><br /> `/p:` `symbolfile`|Specifica il nome del file del database di programma \(PDB\) di output che conterrà i simboli per il file di metadati di Windows \(.winmd\) esportato.|  
|`/reference:` `winmd`<br /><br /> `/r:` `winmd`|Specifica un file di metadati \(.winmd o assembly\) a cui fare riferimento durante l'esportazione.  Se si utilizzano gli assembly di riferimento contenuti in "\\Programmi \(x86\)\\Reference Assemblies\\Microsoft\\Framework\\.NETCore\\v4.5" \("\\Programmi\\..." su computer a 32 bit\), includere i riferimenti sia a System.Runtime.dll che a mscorlib.dll.|  
|`/utf8output`|Specifica che la codifica dei messaggi di output deve essere UTF\-8.|  
|`/warnaserror+`|Specifica di considerare tutti gli avvisi come errori.|  
|**@** `responsefile`|Specifica un file di risposta \(.rsp\) contenente le opzioni \(e facoltativamente `winmdmodule`\).  Ogni riga in `responsefile` deve contenere un solo argomento o opzione.|  
  
## Note  
 Winmdexp.exe non è progettato per convertire un assembly .NET Framework arbitrario in un file .winmd.  Richiede un modulo compilato con l'opzione `/target:winmdobj` e prevede delle restrizioni aggiuntive.  La più importante di queste restrizioni è che tutti i tipi esposti nella superficie dell'API dell'assembly devono essere tipi di [!INCLUDE[wrt](../../../includes/wrt-md.md)].  Per ulteriori informazioni, vedere la sezione "Dichiarazioni di tipi nei componenti di Windows Runtime" nell'articolo [Creazione di componenti Windows Runtime in C\# e Visual Basic](http://go.microsoft.com/fwlink/p/?LinkID=238313) in Windows Dev Center.  
  
 Quando si scrive un'app [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] o un componente di [!INCLUDE[wrt](../../../includes/wrt-md.md)] con C\# o Visual Basic, .NET Framework fornisce supporto per rendere la programmazione con [!INCLUDE[wrt](../../../includes/wrt-md.md)] più naturale.  Questo aspetto viene trattato nell'articolo [Supporto .NET Framework per applicazioni Windows Store e Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md).  Nel processo, alcuni tipi di uso comune di [!INCLUDE[wrt](../../../includes/wrt-md.md)] vengono mappati ai tipi .NET Framework.  Winmdexp.exe inverte questo processo e produce una superficie API che utilizza i tipi di [!INCLUDE[wrt](../../../includes/wrt-md.md)] corrispondenti.  Ad esempio, per i tipi che vengono costruiti dall'interfaccia <xref:System.Collections.Generic.IList%601> viene effettuato il mapping ai tipi costruiti dall'interfaccia [IVector\<T\>](http://go.microsoft.com/fwlink/p/?LinkId=251132) di [!INCLUDE[wrt](../../../includes/wrt-md.md)].  
  
## Vedere anche  
 [Supporto .NET Framework per applicazioni Windows Store e Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)   
 [Creazione di componenti Windows Runtime in C\# e Visual Basic](http://go.microsoft.com/fwlink/p/?LinkID=238313)   
 [Winmdexp.exe Error Messages](../../../docs/framework/tools/winmdexp-exe-error-messages.md)   
 [Build, Deployment, and Configuration Tools \(.NET Framework\)](http://msdn.microsoft.com/it-it/b8c921be-6012-4181-b8d4-ab15813fc9a7)