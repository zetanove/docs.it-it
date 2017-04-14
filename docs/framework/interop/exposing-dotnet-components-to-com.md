---
title: "Exposing .NET Framework Components to COM | Microsoft Docs"
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
  - "interoperation with unmanaged code, exposing .NET Framework components"
  - "COM interop, exposing COM components"
ms.assetid: e42a65f7-1e61-411f-b09a-aca1bbce24c6
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Exposing .NET Framework Components to COM
Per gli sviluppatori, creare un tipo .NET e utilizzarlo da codice non gestito sono due attività distinte.  In questa sezione vengono forniti diversi suggerimenti per la creazione di codice gestito in grado di interagire con client COM:  
  
-   [Qualificazione di tipi .NET per l'interoperabilità](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md).  
  
     È necessario che tutti i tipi gestiti, i metodi, le proprietà, i campi e gli eventi che si desidera esporre a COM siano pubblici.  I tipi devono disporre di un costruttore pubblico predefinito, che costituisce l'unico costruttore che può essere chiamato tramite COM.  
  
-   [Applicazione di attributi di interoperabilità](../../../docs/framework/interop/applying-interop-attributes.md).  
  
     L'aggiunta di attributi personalizzati al codice gestito migliora l'interoperabilità di un componente.  
  
-   [Preparazione di un assembly per COM](../../../docs/framework/interop/packaging-an-assembly-for-com.md).  
  
     È possibile che gli sviluppatori COM richiedano un riepilogo delle procedure a cui attenersi per fare riferimento agli assembly e per distribuirli.  
  
 In questa sezione vengono inoltre illustrate le attività relative all'utilizzo di un tipo gestito da un client COM.  
  
#### Per utilizzare un tipo gestito da COM  
  
1.  [Registrare gli assembly presso COM](../../../docs/framework/interop/registering-assemblies-with-com.md).  
  
     I tipi contenuti in un assembly \(e nelle librerie dei tipi\) devono essere registrati in fase di progettazione.  Se non si fornisce un programma di installazione che registra l'assembly, occorrerà indicare agli sviluppatori COM di utilizzare Regasm.exe.  
  
2.  [Fare riferimento a tipi .NET da COM](../../../docs/framework/interop/how-to-reference-net-types-from-com.md).  
  
     Gli sviluppatori COM possono fare riferimento ai tipi contenuti in un assembly utilizzando le tecniche e gli strumenti consueti.  
  
3.  [Chiamare un oggetto .NET](http://msdn.microsoft.com/it-it/40c9626c-aea6-4bad-b8f0-c1de462efd33).  
  
     Gli sviluppatori COM possono chiamare i metodi dell'oggetto .NET così come chiamano i metodi di qualunque tipo non gestito.  L'API COM **CoCreateInstance**, ad esempio, attiva oggetti .NET.  
  
4.  [Distribuire un'applicazione per l'accesso COM](http://msdn.microsoft.com/it-it/fb63564c-c1b9-4655-a094-a235625882ce).  
  
     Un assembly con nome sicuro può essere installato nella Global Assembly Cache e richiede la firma del relativo editore.  Gli assembly che non dispongono di un nome sicuro devono essere installati nella directory dell'applicazione del client.  
  
## Vedere anche  
 [Interoperating with Unmanaged Code](../../../docs/framework/interop/index.md)   
 [COM Interop Sample: COM Client and .NET Server](../../../docs/framework/interop/com-interop-sample-com-client-and-net-server.md)