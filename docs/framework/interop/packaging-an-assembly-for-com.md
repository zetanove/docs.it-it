---
title: "Packaging an Assembly for COM | Microsoft Docs"
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
  - "exposing .NET Framework components to COM"
  - "COM interop, packaging assemblies"
  - "packaging assemblies for COM"
  - "Tlbexp.exe"
  - "TypeLibConverter class"
  - ".NET Services Installation tool"
  - "Assembly Registration tool"
  - "Type Library Exporter"
  - "Reqsvcs.exe"
  - "interoperation with unmanaged code, exposing .NET Framework components"
  - "interoperation with unmanaged code, packaging assemblies"
  - "COM interop, exposing COM components"
  - "Reqasm.exe"
ms.assetid: 39dc55aa-f2a1-4093-87bb-f1c0edb6e761
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Packaging an Assembly for COM
Di seguito sono elencate le informazioni da fornire agli sviluppatori COM che intendono incorporare tipi gestiti nella propria applicazione:  
  
-   Un elenco dei tipi che le applicazioni COM possono utilizzare  
  
     Alcuni tipi gestiti sono invisibili a COM. Alcuni sono visibili ma non creabili. Altri, infine, sono visibili e creabili.  Un assembly può contenere qualsiasi combinazione di tipi invisibili, visibili, non creabili e creabili.  Identificare, per completezza, i tipi dell'assembly che si prevede di esporre a COM, soprattutto se si tratta di un sottoinsieme dei tipi esposti a .NET Framework.  
  
     Per ulteriori informazioni, vedere [Qualificazione di tipi .NET per l'interoperabilità](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md).  
  
-   Istruzioni per il controllo delle versioni  
  
     Le classi gestite che implementano l'interfaccia della classe \(una interfaccia generata dall'interoperabilità COM\) sono soggette a restrizioni relative al controllo delle versioni.  
  
     Per indicazioni sull'utilizzo dell'interfaccia della classe, vedere [Introduzione all'interfaccia della classe](http://msdn.microsoft.com/it-it/733c0dd2-12e5-46e6-8de1-39d5b25df024).  
  
-   Istruzioni per la distribuzione  
  
     Gli assembly con nome sicuro firmati da un editore possono essere installati nella Global Assembly Cache.  Gli assembly non firmati devono essere installati sul computer dell'utente come assembly privati.  
  
     Per ulteriori informazioni, vedere [Considerazioni sulla sicurezza degli assembly](../../../docs/framework/app-domains/assembly-security-considerations.md).  
  
-   Inclusione di librerie dei tipi  
  
     Quando vengono utilizzati da una applicazione COM, i tipi richiedono quasi sempre una libreria dei tipi.  È possibile generare una libreria dei tipi o rimettere tale attività agli sviluppatori COM.  Le seguenti opzioni di [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] consentono di generare una libreria dei tipi:  
  
    -   [Utilità di esportazione della libreria dei tipi](#cpconpackagingassemblyforcomanchor1)  
  
    -   [Classe TypeLibConverter](#cpconpackagingassemblyforcomanchor2)  
  
    -   [Strumento di registrazione degli assembly](#cpconpackagingassemblyforcomanchor3)  
  
    -   [Strumento di installazione dei servizi .NET](#cpconpackagingassemblyforcomanchor4)  
  
     Indipendentemente dal sistema scelto, solo i tipi pubblici definiti nell'assembly che si fornisce verranno inclusi nella libreria dei tipi generata.  
  
     È possibile creare il package di una libreria dei tipi come file separato oppure incorporarla come file di risorse Win32 in un'applicazione basata su .NET.  In Microsoft Visual Basic 6.0, questa attività viene eseguita automaticamente. Se si utilizza [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)], è invece necessario incorporare la libreria dei tipi manualmente.  Per istruzioni, vedere [Procedura: incorporare librerie dei tipi come risorse Win32 nelle applicazioni basate su .NET](http://msdn.microsoft.com/it-it/c97b4b8c-2ab7-4ac7-8fc8-0ba5c5d59c44).  
  
<a name="cpconpackagingassemblyforcomanchor1"></a>   
## Utilità di esportazione della libreria dei tipi  
 L'[utilità di esportazione della libreria dei tipi \(Tlbexp.exe\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md) è uno strumento della riga di comando che converte le classi e le interfacce contenute in un assembly in una libreria dei tipi COM.  Una volta rese disponibili le informazioni sui tipi della classe, i client COM potranno creare un'istanza della classe .NET e chiamarne i metodi, esattamente come se si trattasse di un oggetto COM.  Tlbexp.exe converte un intero assembly in blocco.  Non è possibile utilizzare Tlbexp.exe per generare informazioni sui tipi per un sottoinsieme dei tipi definiti in un assembly.  
  
<a name="cpconpackagingassemblyforcomanchor2"></a>   
## Classe TypeLibConverter  
 La classe <xref:System.Runtime.InteropServices.TypeLibConverter>, inclusa nello spazio dei nomi **System.Runtime.Interop**, consente la conversione delle classi e delle interfacce contenute in un assembly in una libreria dei tipi COM.  Questa API produce le stesse informazioni sui tipi che vengono fornite dall'utilità di esportazione della libreria dei tipi, descritta nella sezione precedente.  
  
 **La classe TypeLibConverter** implementa l'[interfaccia ITypeLibConverter](frlrfSystemRuntimeInteropServicesITypeLibConverterClassTopic).  
  
<a name="cpconpackagingassemblyforcomanchor3"></a>   
## Strumento di registrazione degli assembly  
 Se usato con l'opzione **\/tlb:**, lo [strumento di registrazione degli assembly \(Regasm.exe\)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) è in grado di generare e registrare una libreria dei tipi.  I client COM richiedono che le librerie dei tipi siano installate nel Registro di sistema di Windows.  Se non si utilizza questa opzione, Regasm.exe registra solo i tipi contenuti in un assembly, non la libreria dei tipi.  La registrazioni dei tipi in un assembly e la registrazione della libreria dei tipi sono due attività distinte.  
  
<a name="cpconpackagingassemblyforcomanchor4"></a>   
## Strumento di installazione dei servizi .NET  
 Lo [strumento di installazione dei servizi .NET \(Regsvcs.exe\)](../../../docs/framework/tools/regsvcs-exe-net-services-installation-tool.md) aggiunge classi gestite ai servizi componenti di Windows 2000 e combina in un unico strumento diverse attività.  Oltre a eseguire il caricamento e la registrazione di un assembly, Regsvcs.exe è in grado di generare, registrare e installare la libreria dei tipi in un'applicazione COM\+ 1.0 esistente.  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.TypeLibConverter>   
 <xref:System.Runtime.InteropServices.ITypeLibConverter>   
 [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Qualifying .NET Types for Interoperation](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md)   
 [Introducing the Class Interface](http://msdn.microsoft.com/it-it/733c0dd2-12e5-46e6-8de1-39d5b25df024)   
 [Considerazioni sulla sicurezza degli assembly](../../../docs/framework/app-domains/assembly-security-considerations.md)   
 [Tlbexp.exe \(Type Library Exporter\)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)   
 [Registering Assemblies with COM](../../../docs/framework/interop/registering-assemblies-with-com.md)   
 [How to: Embed Type Libraries as Win32 Resources in Applications](http://msdn.microsoft.com/it-it/c97b4b8c-2ab7-4ac7-8fc8-0ba5c5d59c44)