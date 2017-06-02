---
title: "Global Assembly Cache | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "elenchi di controllo di accesso [.NET Framework]"
  - "ACL [.NET Framework]"
  - "assembly [.NET Framework], Global Assembly Cache"
  - "cache [.NET Framework], Global Assembly Cache"
  - "GAC (Global Assembly Cache)"
  - "Global Assembly Cache"
  - "Global Assembly Cache, informazioni"
ms.assetid: cf5eacd0-d3ec-4879-b6da-5fd5e4372202
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Global Assembly Cache
Ogni computer in cui è installato Common Language Runtime dispone di una cache del codice a livello di macchina denominata Global Assembly Cache.  Nella Global Assembly Cache vengono archiviati gli assembly che verranno utilizzati da più applicazioni presenti sul computer.  
  
 Gli assembly devono essere installati nella Global Assembly Cache solo quando è necessario condividerli.  È consigliabile mantenere private le dipendenze degli assembly e inserire gli assembly nella directory dell'applicazione, a meno che non vi sia la specifica esigenza di condividerli.  Non è inoltre necessario installare assembly nella Global Assembly Cache per renderli accessibili all'interoperabilità COM o al codice gestito.  
  
> [!NOTE]
>  In alcune situazioni si preferisce non installare un assembly nella Global Assembly Cache.  Se si inserisce nella Global Assembly Cache uno degli assembly che costituiscono un'applicazione, non sarà più possibile replicare o installare l'applicazione copiando la relativa directory con il comando **xcopy**.  Occorrerà infatti spostare anche l'assembly contenuto nella Global Assembly Cache.  
  
 Un assembly può essere distribuito nella Global Assembly Cache in due modi:  
  
-   Utilizzando un programma di installazione in grado di gestire la Global Assembly Cache.  Questa è la soluzione più indicata.  
  
-   Utilizzando uno strumento di sviluppo denominato [strumento Global Assembly Cache \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md), fornito con [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
    > [!NOTE]
    >  Ai fini della distribuzione, per installare gli assembly nella Global Assembly Cache è necessario utilizzare Windows Installer.  Utilizzare lo strumento della Global Assembly Cache solo in scenari di sviluppo. In questo modo non viene infatti fornito il conteggio dei riferimenti agli assembly e altre funzionalità offerte invece da Windows Installer.  
  
 A partire da .NET Framework 4, per impostazione predefinita la Global Assembly Cache è **%windir%\\Microsoft.NET\\assembly**.  Nelle versioni precedenti di .NET Framework, il percorso predefinito è **%windir%\\assembly**.  
  
 La directory systemroot viene spesso protetta dagli amministratori tramite un elenco di controllo di accesso \(ACL, Access Control List\) che consente di controllare l'accesso in lettura e in esecuzione.  Poiché la Global Assembly Cache è installata in una sottodirectory della directory systemroot, ne eredita l'elenco di controllo di accesso.  Si consiglia di consentire l'eliminazione di file dalla Global Assembly Cache solo agli utenti che dispongono di privilegi di amministratore.  
  
 È necessario che gli assembly distribuiti nella Global Assembly Cache abbiano un nome sicuro.  Quando si aggiunge un assembly alla Global Assembly Cache, viene verificata l'integrità di tutti i file che lo costituiscono.  Tale controllo viene svolto dalla cache per accertare che l'assembly non sia stato compromesso, ad esempio per l'eventualità in cui un file sia stato modificato e il manifesto non rispecchi tale modifica.  
  
## Vedere anche  
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [Utilizzo di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Assembly con nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md)