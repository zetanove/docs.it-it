---
title: "/keyfile | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/keyfile compiler option [Visual Basic]"
  - "keyfile compiler option [Visual Basic]"
  - "-keyfile compiler option [Visual Basic]"
ms.assetid: ffa82a4b-517a-4c6c-9889-5bae7b534bb8
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /keyfile
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di specificare un file contenente una chiave o una coppia di chiavi allo scopo di assegnare a un assembly un nome sicuro.  
  
## Sintassi  
  
```  
/keyfile:file  
```  
  
## Argomenti  
 `file`  
 Obbligatorio.  Il file che contiene la chiave.  Se il nome file contiene uno spazio, racchiudere il nome tra virgolette \(" "\).  
  
## Note  
 Viene inserita nel manifesto dell'assembly la chiave pubblica e quindi l'assembly finale viene firmato con la chiave privata.  Per generare un file di chiave, immettere `sn -k file` nella riga di comando.  Per ulteriori informazioni, vedere [Sn.exe \(Strong Name Tool\)](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md).  
  
 Se si esegue la compilazione con l'opzione `/target:module`, il nome del file di chiavi verrà conservato nel modulo e incorporato nell'assembly che viene creato quando si compila un assembly con l'opzione [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md).  
  
 È anche possibile passare al compilatore le informazioni di crittografia mediante [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md).  Utilizzare [\/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md) se si desidera che l'assembly sia parzialmente firmato.  
  
 Questa opzione può essere specificata anche come attributo personalizzato \(<xref:System.Reflection.AssemblyKeyFileAttribute>\) nel codice sorgente di qualsiasi modulo MSIL \(Microsoft Intermediate Language\).  
  
 Qualora nella stessa compilazione vengano specificate sia `/keyfile` che [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md) \(tramite opzione della riga di comando o attributo personalizzato\), verrà effettuato prima un tentativo con il contenitore di chiavi.  Se questa operazione viene eseguita correttamente, l'assembly viene firmato con le informazioni incluse nel contenitore di chiavi.  Se il contenitore di chiavi non viene trovato, verrà effettuato un tentativo con il file specificato in `/keyfile`.  In caso di esito positivo, l'assembly viene firmato con le informazioni presenti nel file di chiave e le informazioni sulla chiave verranno installate nel contenitore di chiavi, con un'operazione analoga all'immissione di `sn -i`, per far sì che alla successiva compilazione il contenitore di chiavi sarà valido.  
  
 Si noti che un file di chiave può contenere solo la chiave pubblica.  
  
 Per ulteriori informazioni sulla firma di un assembly, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md).  
  
> [!NOTE]
>  L'opzione `/keyfile` non è disponibile dall'interno dell'ambiente di sviluppo di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice seguente consente di compilare il file di origine `Input.vb` e di specificare un file della chiave.  
  
```  
vbc /keyfile:myfile.sn input.vb  
```  
  
## Vedere anche  
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)