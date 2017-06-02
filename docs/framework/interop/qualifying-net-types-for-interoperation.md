---
title: "Qualifying .NET Types for Interoperation | Microsoft Docs"
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
  - "COM interop, qualifying .NET types"
  - "qualifying .NET types for interoperation"
  - "interoperation with unmanaged code, qualifying .NET types"
  - "interoperation with unmanaged code, exposing .NET Framework components"
  - "COM interop, exposing COM components"
ms.assetid: 4b8afb52-fb8d-4e65-b47c-fd82956a3cdd
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Qualifying .NET Types for Interoperation
Se si desidera esporre i tipi contenuti in un assembly alle applicazioni COM, vanno tenuti presenti i requisiti di interoperabilità COM in fase di progettazione.  Le indicazioni riportate di seguito consentono di integrare senza difficoltà tipi gestiti \(classi, interfacce, strutture ed enumerazioni\) e tipi COM.  
  
-   È necessario che le classi implementino le interfacce in maniera esplicita.  
  
     Per quanto l'interoperabilità COM fornisca un meccanismo in grado di generare automaticamente un'interfaccia contenente tutti i membri della classe e i membri della relativa classe base, è preferibile fornire interfacce esplicite.  L'interfaccia generata automaticamente è definita interfaccia della classe.  Per indicazioni specifiche, vedere [Introduzione all'interfaccia della classe](http://msdn.microsoft.com/it-it/733c0dd2-12e5-46e6-8de1-39d5b25df024).  
  
     Per incorporare le definizioni di interfaccia nel codice è possibile utilizzare [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C\# e C\+\+ anziché il linguaggio IDL \(Interface Definition Language\) o soluzioni equivalenti.  Per informazioni dettagliate sulla sintassi, vedere la documentazione del proprio linguaggio.  
  
-   È necessario che i tipi gestiti siano pubblici.  
  
     Solo i tipi pubblici di un assembly vengono registrati ed esportati nella libreria dei tipi.  Di conseguenza saranno visibili in COM solo i tipi pubblici.  
  
     I tipi gestiti espongono ad altro codice gestito delle funzionalità che non potrebbero essere esposte a COM.  Non vengono ad esempio esposti ai client COM i costruttori con parametri, i metodi statici e i campi costanti.  Poiché inoltre il runtime effettua il marshalling dei dati in entrata e in uscita da un tipo, è possibile che i dati vengano copiati o trasformati.  
  
-   È necessario che i metodi, le proprietà, i campi e gli eventi siano pubblici.  
  
     Anche i membri dei tipi pubblici, se sono destinati a essere visibili da COM, devono essere pubblici.  È possibile limitare la visibilità di un assembly, di un tipo pubblico o dei membri pubblici di un tipo pubblico utilizzando l'oggetto <xref:System.Runtime.InteropServices.ComVisibleAttribute>.  Tutti i tipi e i membri pubblici sono visibili per impostazione predefinita.  
  
-   Perché possano essere attivati da COM, è necessario che i tipi abbiano un costruttore pubblico predefinito.  
  
     I tipi pubblici gestiti sono visibili a COM.  I client COM non possono tuttavia creare il tipo senza un costruttore pubblico predefinito \(un costruttore senza argomenti\).  Se il tipo viene attivato in altro modo, i client COM potranno comunque utilizzarlo.  
  
-   I tipi non possono essere astratti.  
  
     Né i client COM né i client .NET possono creare tipi astratti.  
  
 Quando la si esporta in COM, la gerarchia di ereditarietà di un tipo gestito viene semplificata.  Anche il controllo delle versioni varia tra ambiente gestito e ambiente non gestito.  I tipi esposti a COM hanno funzionalità di controllo delle versioni diverse da quelle degli altri tipi gestiti.  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.ComVisibleAttribute>   
 [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [Introducing the Class Interface](http://msdn.microsoft.com/it-it/733c0dd2-12e5-46e6-8de1-39d5b25df024)   
 [Applying Interop Attributes](../../../docs/framework/interop/applying-interop-attributes.md)   
 [Packaging an Assembly for COM](../../../docs/framework/interop/packaging-an-assembly-for-com.md)