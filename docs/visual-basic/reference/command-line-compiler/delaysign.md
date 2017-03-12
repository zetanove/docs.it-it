---
title: "/delaysign | Microsoft Docs"
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
  - "delaysign compiler option [Visual Basic]"
  - "/delaysign compiler option [Visual Basic]"
  - "-delaysign compiler option [Visual Basic]"
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /delaysign
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica se l'assembly avrà firma completa o parziale.  
  
## Sintassi  
  
```  
/delaysign[+ | -]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo.  Utilizzare `/delaysign-` se si desidera che l'assembly abbia firma completa.  Utilizzare `/delaysign+` se si desidera inserire la chiave pubblica nell'assembly e riservare lo spazio per l'hash firmato.  Il valore predefinito è `/delaysign-`.  
  
## Note  
 L'opzione `/delaysign` non ha alcun effetto se non è abbinata all'opzione [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md) o [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md).  
  
 Quando si richiede un assembly completamente firmato, il compilatore genera un hash per il file che contiene il manifesto, o metadati dell'assembly, e quindi firma l'hash risultante con la chiave privata.  La firma digitale risultante viene archiviata nel file contenente il manifesto.  Se per un assembly si utilizza una firma posticipata, il compilatore non calcola né memorizza la firma ma riserva lo spazio nel file per l'aggiunta della firma in un secondo momento.  
  
 Utilizzando `/delaysign+` ad esempio, uno sviluppatore in un'organizzazione può distribuire versioni di verifica di un assembly non firmate che i tester possono registrare con la Global Assembly Cache e utilizzare.  Quando si completa il lavoro su un assieme, la persona responsabile della chiave privata dell'organizzazione può firmare completamente l'assembly.  Questo contesto protegge la chiave privata dell'organizzazione dalla divulgazione, mentre consente a tutti gli sviluppatori di utilizzare gli assembly.  
  
 Per ulteriori informazioni sulla firma di un assembly, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md).  
  
### Per impostare\/posticipare la firma nell'ambiente di sviluppo integrato di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Firma**.  
  
3.  Impostare il valore nella casella **Solo firma ritardata**.  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [\/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)