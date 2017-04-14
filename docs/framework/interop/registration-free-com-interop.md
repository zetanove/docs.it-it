---
title: "Registration-Free COM Interop | Microsoft Docs"
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
  - "assemblies [.NET Framework], interop"
  - "COM interop, registration-free COM interop"
  - "registration-free COM interop"
  - "manifests [.NET Framework]"
  - "registration-free activation"
  - "object activation"
  - "registration-free COM interop, about registration-free COM interop"
ms.assetid: 90f308b9-82dc-414a-bce1-77e0155e56bd
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Registration-Free COM Interop
L'interoperabilità COM senza registrazione consente di attivare un componente senza usare il Registro di sistema di Windows per memorizzare informazioni sugli assembly.  Anziché registrare un componente su un computer durante la distribuzione, vengono creati file manifesto di tipo Win32 contenenti informazioni sull'associazione e sull'attivazione in fase di progettazione.  L'attivazione di un oggetto è controllata da tali file manifesto, anziché da chiavi del Registro di sistema.  
  
 Usando l'attivazione senza registrazione per gli assembly, anziché effettuarne la registrazione durante la distribuzione, è possibile usufruire di due vantaggi:  
  
-   È possibile controllare la versione della DLL che verrà attivata in caso di installazione di più versioni in un computer.  
  
-   Gli utenti finali possono copiare l'applicazione in una directory appropriata del computer tramite XCOPY o FTP.  L'applicazione potrà quindi essere eseguita da tale directory.  
  
 Questa sezione descrive i due tipi di manifesto necessari per l'interoperabilità COM senza registrazione: il manifesto dell'applicazione e quello del componente.  Questi manifesti sono costituiti da file XML.  Un manifesto dell'applicazione, creato dallo sviluppatore di un'applicazione, contiene metadati che descrivono gli assembly e le relative dipendenze.  Un manifesto del componente, creato dallo sviluppatore di un componente, contiene informazioni altrimenti inserite nel Registro di sistema di Windows.  
  
### Requisiti per l'interoperabilità COM senza registrazione  
  
1.  Il supporto per l'interoperabilità COM senza registrazione varia leggermente a seconda del tipo di assembly di libreria; in particolare, se l'assembly non è gestito \(COM side\-by\-side\) o gestito \(basato su .NET\).  La tabella seguente illustra il sistema operativo e i requisiti di versione di .NET Framework per ogni tipo di assembly.  
  
    |Tipo di assembly|Sistema operativo|Versione di .NET Framework|  
    |----------------------|-----------------------|--------------------------------|  
    |Assembly side\-by\-side COM|Microsoft Windows XP|Non richiesto|  
    |Basato su .NET|Windows XP con SP2|NET Framework versione 1.1 o successiva.|  
  
     La famiglia Windows Server 2003 supporta anche l'interoperabilità COM senza registrazione per gli assembly basati su .NET.  
  
     Affinché una classe basata su .NET sia compatibile con l'attivazione senza registrazione da COM, la classe deve avere un costruttore predefinito e deve essere pubblica.  
  
### Configurazione di componenti COM per l'attivazione senza registrazione  
  
1.  Affinché un componente COM partecipi all'attivazione senza registrazione è necessario distribuirlo come assembly side\-by\-side.  Gli assembly side\-by\-side non sono gestiti.  Per altre informazioni, vedere "Using Side\-by\-side Assemblies" in MSDN Library.  
  
     Per usare gli assembly side\-by\-side COM, uno sviluppatore di applicazioni basate su .NET deve fornire un manifesto dell'applicazione che contenga le informazioni di associazione e attivazione.  Il supporto per gli assembly side\-by\-side è integrato nel sistema operativo Windows XP.  Il runtime COM, supportato dal sistema operativo, esegue l'analisi di un manifesto dell'applicazione per informazioni sull'attivazione quando il componente attivato non è presente nel Registro di sistema.  
  
     L'attivazione senza registrazione è facoltativa per i componenti COM installati in Windows XP.  Per istruzioni dettagliate sull'aggiunta di un assembly side\-by\-side a un'applicazione, cercare "Using Side\-by\-side Assemblies" in MSDN Library.  
  
    > [!NOTE]
    >  L'esecuzione side\-by\-side è una funzionalità di .NET Framework che consente di eseguire contemporaneamente sullo stesso computer più versioni del runtime e più versioni delle applicazioni e dei componenti che usano una versione del runtime.  L'esecuzione side\-by\-side e gli assembly side\-by\-side sono meccanismi diversi per fornire la funzionalità side\-by\-side.  
  
## Vedere anche  
 [How to: Configure .NET Framework\-Based COM Components for Registration\-Free Activation](../../../docs/framework/interop/configure-net-framework-based-com-components-for-reg.md)