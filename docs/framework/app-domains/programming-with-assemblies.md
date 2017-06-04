---
title: "Programmazione con gli assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], programmazione"
  - "programmazione di assembly"
ms.assetid: 25918b15-701d-42c7-95fc-c290d08648d6
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Programmazione con gli assembly
Gli assembly costituiscono i blocchi predefiniti di .NET Framework, poiché rappresentano l'unità fondamentale di distribuzione, controllo delle versioni, riutilizzo, ambito di attivazione e autorizzazioni di sicurezza.  Con gli assembly si forniscono a Common Language Runtime le informazioni necessarie sulle implementazioni dei tipi.  e può essere considerato come una raccolta di tipi e risorse che formano un'unità logica di funzionalità e che sono compilati per interagire.  Per Common Language Runtime non esiste alcun tipo all'esterno del contesto di un assembly.  
  
 In questa sezione vengono descritte la creazione di moduli, la creazione di assembly da moduli, la creazione di una coppia di chiavi e la firma di un assembly con un nome sicuro e infine l'installazione di un assembly nella Global Assembly Cache.  In questa sezione viene inoltre descritto come utilizzare [MSIL Disassembler \(Ildasm.exe\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per la visualizzazione delle informazioni relative al manifesto dell'assembly.  
  
> [!NOTE]
>  A partire da .NET Framework versione 2.0, il runtime non carica un assembly compilato con una versione di .NET Framework successiva a quella del runtime attualmente caricato.  Questa indicazione è valida per la combinazione di componenti principali e secondari del numero di versione.  
  
## In questa sezione  
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)  
 Viene fornita una panoramica degli assembly su singolo file o su più file.  
  
 [Nomi degli assembly](../../../docs/framework/app-domains/assembly-names.md)  
 Viene fornita una panoramica sulla denominazione dell'assembly.  
  
 [Procedura: determinare il nome completo di un assembly](../../../docs/framework/app-domains/how-to-determine-assembly-fully-qualified-name.md)  
 Viene descritto come determinare il nome completo di un assembly.  
  
 [Esecuzione di applicazioni Intranet in attendibilità totale](../../../docs/framework/app-domains/running-intranet-applications-in-full-trust.md)  
 Viene descritto come specificare un criterio di sicurezza legacy per gli assembly con attendibilità totale in una condivisione di rete Intranet.  
  
 [Posizione dell'assembly](../../../docs/framework/app-domains/assembly-location.md)  
 Viene fornita una panoramica sulle posizioni in cui trovare l'assembly.  
  
 [Procedura: compilare un assembly su singolo file](../../../docs/framework/app-domains/how-to-build-a-single-file-assembly.md)  
 Viene descritta la modalità di creazione di un assembly su singolo file.  
  
 [Assembly su più file](../../../docs/framework/app-domains/multifile-assemblies.md)  
 Vengono descritte le ragioni per la creazione di assembly a più file.  
  
 [Procedura: Compilare un assembly su più file](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)  
 Viene descritta la modalità di creazione di un assembly su più file.  
  
 [Impostazione degli attributi dell'assembly](../../../docs/framework/app-domains/set-assembly-attributes.md)  
 Vengono descritti gli attributi dell'assembly e la relativa modalità di impostazione.  
  
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)  
 Vengono descritte la modalità e le ragioni per la firma di un assembly con un nome sicuro e vengono incluse specifiche procedure.  
  
 [Ritardo della firma di un assembly](../../../docs/framework/app-domains/delay-sign-assembly.md)  
 Viene descritto come apporre una firma ritardata a un assembly.  
  
 [Utilizzo di assembly e della Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
 Vengono descritte la modalità e le ragioni per l'aggiunta di assembly alla Global Assembly Cache e vengono incluse specifiche procedure.  
  
 [Procedura: Visualizzare il contenuto dell'assembly](../../../docs/framework/app-domains/how-to-view-assembly-contents.md)  
 Viene descritto come utilizzare MSIL Disassembler \(Ildasm.exe\) per la visualizzazione dei contenuti dell'assembly.  
  
 [Inoltro dei tipi in Common Language Runtime](../../../docs/framework/app-domains/type-forwarding-in-the-common-language-runtime.md)  
 Viene descritto come utilizzare l'inoltro di tipi per spostare un tipo in un assembly diverso senza interrompere le applicazioni esistenti.  
  
## Riferimenti  
 <xref:System.Reflection.Assembly>  
 La classe .NET Framework che rappresenta un assembly.  
  
## Sezioni correlate  
 [Procedura: reperire informazioni su tipo e membro da un assembly](../../../docs/framework/app-domains/how-to-obtain-type-and-member-information-from-an-assembly.md)  
 Viene descritto come ottenere a livello di codice informazioni relative al tipo o altre informazioni da un assembly.  
  
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)  
 Viene fornita una panoramica sui concetti di base relativi agli assembly di Common Language Runtime.  
  
 [Controllo delle versioni degli assembly](../../../docs/framework/app-domains/assembly-versioning.md)  
 Vengono forniti cenni preliminari sull'associazione di assembly e sugli attributi <xref:System.Reflection.AssemblyVersionAttribute> e <xref:System.Reflection.AssemblyInformationalVersionAttribute>.  
  
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
 Viene descritta la modalità con cui il runtime determina l'assembly da utilizzare per soddisfare una richiesta di associazione.  
  
 [Reflection](../../../docs/framework/reflection-and-codedom/reflection.md)  
 Viene descritto l'utilizzo della classe **Reflection** per ottenere informazioni su un assembly.