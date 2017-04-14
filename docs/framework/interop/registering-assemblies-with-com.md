---
title: "Registering Assemblies with COM | Microsoft Docs"
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
  - "COM interop, registering assemblies"
  - "unregistering assemblies"
  - "interoperation with unmanaged code, registering assemblies"
  - "registering assemblies"
ms.assetid: 87925795-a3ae-4833-b138-125413478551
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Registering Assemblies with COM
Per la registrazione o l'annullamento della registrazione di un assembly da utilizzare con COM, è possibile eseguire uno strumento della riga di comando, denominato [strumento di registrazione degli assembly \(Regasm.exe\)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md).  Regasm.exe aggiunge informazioni sulla classe al Registro di sistema in modo dai client COM possono utilizzare la classe di .NET Framework in.  La classe <xref:System.Runtime.InteropServices.RegistrationServices> fornisce la funzionalità equivalente.  
  
 Prima dell'attivazione da un COM client, è necessario che un componente gestito venga registrato nel Registro di sistema di Windows.  Nella tabella riportata di seguito vengono illustrate le chiave in genere aggiunte al Registro di sistema di Windows mediante Regasm.exe.  000000 indica il valore effettivo del GUID.  
  
|GUID|Descrizione|Chiave del Registro di sistema|  
|----------|-----------------|------------------------------------|  
|CLSID|Identificatore di classe|HKEY\_CLASSES\_ROOT\\CLSID\\{000…000}|  
|IID|Identificatore di interfaccia|HKEY\_CLASSES\_ROOT\\Interface\\{000…000}|  
|LIBID|Identificatore di libreria|HKEY\_CLASSES\_ROOT\\TypeLib\\{000…000}|  
|ProgID|Identificatore a livello di codice|HKEY\_CLASSES\_ROOT\\000…000|  
  
 Nella chiave HKCR\\CLSID\\{0000…0000}, il valore predefinito viene impostato sul ProgID della classe e vengono aggiunti due nuovi valori denominati, Class e Assembly.  Il runtime legge il valore di Assembly dal Registro di sistema e lo passa al sistema di risoluzione assembly del runtime.  Il sistema di risoluzione assembly tenta di trovare l'assembly in base a informazioni quali il nome e il numero di versione dell'assembly stesso.  Affinché venga individuato dal sistema di risoluzione assembly, un assembly deve trovarsi in uno dei seguenti percorsi:  
  
-   Nella Global Assembly Cache. È necessario che costituisca un assembly con nome sicuro.  
  
-   Nella directory dell'applicazione.  Gli assembly caricati dal percorso di un'applicazione saranno accessibili soltanto da quella applicazione.  
  
-   In un percorso file specificato con l'opzione **\/codebase** in Regasm.exe.  
  
 Mediante Regasm.exe viene inoltre creata la chiave InProcServer32 sotto la chiave HKCR\\CLSID\\{0000…0000}.  Il valore predefinito della chiave viene impostato sul nome della DLL con cui viene inizializzato Common Language Runtime \(Mscoree.dll\).  
  
## Analisi delle voci del Registro di sistema  
 L'interoperabilità COM fornisce un'implementazione di class factory standard per creare un'istanza di ciascuna classe .NET Framework.  I client possono chiamare **DllGetClassObject** sulla DLL gestita per ottenere una class factory e creare oggetti, esattamente come farebbero con qualunque altro componente COM.  
  
 Per la sottochiave di `InprocServer32`, un riferimento a In luogo di una classica libreria dei tipi COM tradizionale indicare che Common Language Runtime crea l'oggetto gestito.  
  
## Vedere anche  
 [Exposing .NET Framework Components to COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [How to: Reference .NET Types from COM](../../../docs/framework/interop/how-to-reference-net-types-from-com.md)   
 [Calling a .NET Object](http://msdn.microsoft.com/it-it/40c9626c-aea6-4bad-b8f0-c1de462efd33)   
 [Deploying an Application for COM Access](http://msdn.microsoft.com/it-it/fb63564c-c1b9-4655-a094-a235625882ce)