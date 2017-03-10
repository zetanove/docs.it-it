---
title: "/codepage (Visual Basic) | Microsoft Docs"
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
  - "/codepage compiler option [Visual Basic]"
  - "codepage compiler option [Visual Basic]"
  - "-codepage compiler option [Visual Basic]"
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /codepage (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di specificare la tabella codici da utilizzare per tutti i file di codice sorgente inclusi nella compilazione.  
  
## Sintassi  
  
```  
/codepage:id  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`id`|Necessario.  Il compilatore utilizza la tabella codici specificata da `id` per interpretare la codifica dei file di origine.|  
  
## Note  
 Per compilare il codice sorgente salvato con una codifica specifica, è possibile utilizzare `/codepage` per indicare la tabella codici da utilizzare.  L'opzione `/codepage` viene applicata a tutti i file di codice sorgente inclusi nella compilazione.  Per ulteriori informazioni, vedere [Codifica di caratteri in .NET Framework](../Topic/Character%20Encoding%20in%20the%20.NET%20Framework.md).  
  
 L'opzione `/codepage` non è necessaria se i file del codice di origine sono stati salvati utilizzando la tabella codici ANSI corrente, Unicode o UTF\-8 con una firma.  In [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] tutti i file di codice sorgente vengono salvati per impostazione predefinita con la tabella codici ANSI corrente, a meno che l'utente non specifichi una codifica diversa nella finestra di dialogo **Codifica**.  In [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] la finestra di dialogo **Codifica** viene utilizzata per aprire i file di codice sorgente salvati con una tabella codici diversa.  
  
> [!NOTE]
>  L'opzione `/codepage` non è disponibile dall'interno dell'ambiente di sviluppo di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)], ma solo durante la compilazione dalla riga di comando.  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)