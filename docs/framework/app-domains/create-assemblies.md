---
title: "Creazione degli assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], creazione"
  - "assembly [.NET Framework], su più file"
  - "assembly su più file"
  - "assembly su file singolo"
ms.assetid: 54832ee9-dca8-4c8b-913c-c0b9d265e9a4
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Creazione degli assembly
È possibile creare assembly su singolo file o su più file utilizzando un IDE, ad esempio [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)], o altri compilatori e strumenti forniti da [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  Il tipo di assembly più semplice è costituito da un singolo file con nome semplice caricato in un singolo dominio applicazione.  Non sono consentiti riferimenti a tale assembly da parte di assembly esterni alla directory dell'applicazione e tale assembly non viene sottoposto a verifica della versione.  Per disinstallare l'applicazione costituita dall'assembly, è sufficiente eliminare la directory in cui si trova tale assembly.  In alcuni casi, l'utilizzo di un assembly con questo tipo di funzionalità è sufficiente agli sviluppatori per distribuire un'applicazione.  
  
 È possibile creare un assembly su più file basandosi su svariati moduli di codice e file di risorse  o creare un assembly che possa essere condiviso da più applicazioni.  Un assembly condiviso, a cui è necessario assegnare un nome sicuro, può essere distribuito nella Global Assembly Cache.  
  
 Per il raggruppamento di moduli di codice e risorse in assembly sono disponibili svariate opzioni, che tengono conto dei seguenti fattori:  
  
-   Controllo delle versioni  
  
     Raggruppare moduli in cui è necessario che siano contenute le stesse informazioni sulla versione.  
  
-   Distribuzione  
  
     Raggruppare moduli di codice e risorse che supportano il modello di distribuzione desiderato.  
  
-   Riutilizzo  
  
     Raggruppare i moduli se è possibile utilizzarli insieme in modo logico per un qualche scopo.  È ad esempio possibile inserire nello stesso assembly un assembly costituito da tipi e delle classi utilizzate raramente per la manutenzione del programma.  Si consiglia inoltre di raggruppare in un assembly i tipi che si desidera condividere con più applicazioni e di firmare tale assembly con un nome sicuro.  
  
-   Sicurezza  
  
     Raggruppare moduli contenenti tipi che richiedono le stesse autorizzazioni di sicurezza.  
  
-   Ambito  
  
     Raggruppare moduli contenenti tipi di cui è necessario limitare la visibilità allo stesso assembly.  
  
 Quando si rendono disponibili assembly Common Language Runtime per applicazioni COM non gestite, sono necessarie alcune considerazioni specifiche.  Per ulteriori informazioni sull'utilizzo del codice non gestito, vedere [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md).  
  
## Vedere anche  
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [Controllo delle versioni degli assembly](../../../docs/framework/app-domains/assembly-versioning.md)   
 [Procedura: compilare un assembly su singolo file](../../../docs/framework/app-domains/how-to-build-a-single-file-assembly.md)   
 [Procedura: Compilare un assembly su più file](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Assembly su più file](../../../docs/framework/app-domains/multifile-assemblies.md)