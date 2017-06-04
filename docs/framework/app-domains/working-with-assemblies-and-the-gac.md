---
title: "Utilizzo di assembly e della Global Assembly Cache | Microsoft Docs"
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
  - "GAC (Global Assembly Cache), vantaggi"
  - "Global Assembly Cache, vantaggi"
ms.assetid: 8a18e5c2-d41d-49ef-abcb-7c27e2469433
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Utilizzo di assembly e della Global Assembly Cache
Se si desidera condividere un assembly con più applicazioni, è possibile installare tale assembly nella Global Assembly Cache.  Questa cache di codice su computer è disponibile in ogni computer in cui è installato Common Language Runtime  Nella Global Assembly Cache vengono archiviati gli assembly che verranno utilizzati da più applicazioni presenti sul computer.  Per essere installato nella Global Assembly Cache, è necessario che un assembly disponga di un nome sicuro.  
  
> [!NOTE]
>  È necessario che il nome di assembly e il nome file, esclusa l'estensione, degli assembly inseriti nella Global Assembly Cache corrispondano.  È ad esempio necessario che a un assembly con nome assembly myAssembly sia assegnato un nome file myAssembly.exe o myAssembly.dll.  
  
 Si consiglia di condividere gli assembly installandoli nella Global Assembly Cache solo quando necessario.  È consigliabile mantenere private le dipendenze degli assembly e inserire gli assembly nella directory dell'applicazione, a meno che non vi sia la specifica esigenza di condividerli.  Non è inoltre necessario installare assembly nella Global Assembly Cache per renderli accessibili all'interoperabilità COM o al codice gestito.  
  
 Numerose sono le ragioni per l'installazione di un assembly nella Global Assembly Cache:  
  
-   Posizione condivisa.  
  
     È possibile inserire nella Global Assembly Cache gli assembly che vengono utilizzati dalle applicazioni.  Se ad esempio tutte le applicazioni utilizzano un assembly inserito nella Global Assembly Cache, è possibile aggiungere un'istruzione relativa ai criteri di versione nel file Machine.config che reindirizza i riferimenti all'assembly.  
  
-   Sicurezza dei file.  
  
     La directory systemroot viene spesso protetta dagli amministratori tramite un elenco di controllo di accesso \(ACL, Access Control List\), che consente di controllare l'accesso in lettura e in esecuzione.  Poiché la Global Assembly Cache è installata nella directory systemroot, ne eredita l'elenco di controllo di accesso.  Si consiglia di consentire l'eliminazione di file dalla Global Assembly Cache solo agli utenti che dispongono di privilegi di amministratore.  
  
-   Gestione di più versioni.  
  
     Nella Global Assembly Cache è possibile mantenere più copie di assembly con lo stesso nome ma con informazioni relative alla versione diverse.  
  
-   Posizione di ricerca aggiuntiva.  
  
     Prima di effettuare ricerche o utilizzare le informazioni relative al codice presenti in un file di configurazione, Common Language Runtime cerca nella Global Assembly Cache un assembly corrispondente alla richiesta di assembly.  
  
 Si noti che sono possibili scenari in cui non si desideri esplicitamente installare un assembly nella Global Assembly Cache.  Se si inserisce nella Global Assembly Cache uno degli assembly che costituiscono un'applicazione, non sarà più possibile replicare o installare l'applicazione utilizzando XCOPY per copiare la directory dell'applicazione.  In questo caso è necessario spostare anche l'assembly nella Global Assembly Cache.  
  
## In questa sezione  
 [Procedura: installare un assembly nella Global Assembly Cache](../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)  
 Vengono descritte le modalità di installazione di un assembly nella Global Assembly Cache.  
  
 [Procedura: visualizzare il contenuto della Global Assembly Cache](../../../docs/framework/app-domains/how-to-view-the-contents-of-the-gac.md)  
 Viene illustrato come utilizzare lo [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) per visualizzare il contenuto della Global Assembly Cache.  
  
 [Procedura: rimuovere un assembly dalla Global Assembly Cache](../../../docs/framework/app-domains/how-to-remove-an-assembly-from-the-gac.md)  
 Viene illustrato come utilizzare lo [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) per rimuovere un assembly dalla Global Assembly Cache.  
  
 [Utilizzo dei componenti serviti con la Global Assembly Cache](../../../docs/framework/app-domains/use-serviced-components-with-the-gac.md)  
 Viene spiegato il motivo per cui è consigliabile inserire nella Global Assembly Cache i componenti serviti \(componenti COM\+ gestiti\).  
  
## Sezioni correlate  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)  
 Viene fornita una panoramica sulla creazione degli assembly.  
  
 [Global Assembly Cache](../../../docs/framework/app-domains/gac.md)  
 Viene descritta la Global Assembly Cache.  
  
 [Procedura: Visualizzare il contenuto dell'assembly](../../../docs/framework/app-domains/how-to-view-assembly-contents.md)  
 Viene illustrato come utilizzare [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per visualizzare informazioni sul linguaggio MSIL \(Microsoft Intermediate Language\) in un file.  
  
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
 Viene illustrato come Common Language Runtime individua e carica gli assembly da cui è costituita l'applicazione.  
  
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)  
 Vengono descritti gli assembly, ossia i blocchi predefiniti delle applicazioni gestite.