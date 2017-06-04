---
title: "How to: Generate Primary Interop Assemblies Using Tlbimp.exe | Microsoft Docs"
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
  - "primary interop assemblies, generating"
  - "Tlbimp.exe"
  - "Type Library Importer"
ms.assetid: 5419011c-6e57-40f6-8c65-386db8f7a651
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Generate Primary Interop Assemblies Using Tlbimp.exe
È possibile generare un assembly di interoperabilità primario in due modi:  
  
-   Usando l'[Utilità di importazione della libreria dei tipi \(Tlbimp.exe\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) fornita da [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
     Il modo più semplice per produrre assembly di interoperabilità primari consiste nell'usare l'[Tlbimp.exe \(Type Library Importer\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md).  Tlbimp.exe fornisce le misure di sicurezza seguenti:  
  
    -   Verifica di altri assembly di interoperabilità primari registrati prima della creazione di nuovi assembly di interoperabilità per eventuali riferimenti annidati alla libreria dei tipi.  
  
    -   Nessuna generazione di assembly di interoperabilità primari se non viene specificato il nome del contenitore o del file, in modo da assegnare all'assembly di interoperabilità primario un nome sicuro.  
  
    -   Nessuna generazione di assembly di interoperabilità primari se vengono omessi i riferimenti agli assembly dipendenti.  
  
    -   Nessuna generazione di assembly di interoperabilità primari se vengono aggiunti riferimenti ad assembly dipendenti che non sono assembly di interoperabilità primari.  
  
-   Creazione manuale di assembly di interoperabilità primari nel codice sorgente mediante un linguaggio conforme con la specifica CLS \(Common Language Specification\), ad esempio C\#.  Questo approccio è utile quando non è disponibile una libreria dei tipi.  
  
 Per firmare l'assembly con un nome sicuro, è necessario disporre di una coppia di chiavi crittografiche.  Per informazioni dettagliate, vedere [Creazione di una coppia di chiavi](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md).  
  
### Per generare un assembly di interoperabilità primario tramite Tlbimp.exe  
  
1.  Al prompt dei comandi digitare:  
  
     **tlbimp** *tlbfile*  **\/primary \/keyfile:** *filename* **\/out:** *assemblyname*  
  
     In questo comando *tlbfile* è il file che include la libreria dei tipi COM, *filename* è il nome del contenitore o del file che include la coppia di chiavi e *assemblyname* è il nome dell'assembly da firmare con un nome sicuro.  
  
 Gli assembly di interoperabilità primari possono fare riferimento solo ad altri assembly di interoperabilità primari.  Se l'assembly fa riferimento a tipi da una libreria dei tipi COM di terze parti, sarà necessario ottenere un assembly di interoperabilità primario dal server di pubblicazione prima di potere generarne uno.  Se si è il server di pubblicazione, sarà necessario generare un assembly di interoperabilità primario per la libreria dei tipi dipendente prima di generare l'assembly di interoperabilità primario di riferimento.  
  
 Un assembly di interoperabilità primario dipendente con un numero di versione diverso da quello della libreria dei tipi originali non è rilevabile quando installato nella directory corrente.  È necessario registrare l'assembly di interoperabilità primario dipendente nel Registro di sistema di Windows oppure usare l'opzione **\/reference** per assicurarsi che Tlbimp.exe trovi il file DLL dipendente.  
  
 È anche possibile eseguire il wrapping di più versioni di una libreria dei tipi.  Per istruzioni, vedere [How to: Wrap Multiple Versions of Type Libraries](http://msdn.microsoft.com/it-it/79eefe04-a770-4bc3-8ea2-e90ddb8ec31f).  
  
## Esempio  
 L'esempio seguente importa la libreria dei tipi COM `LibUtil.tlb` e firma l'assembly `LibUtil.dll` con un nome sicuro usando il file di chiave `CompanyA.snk`.  Omettendo un nome di spazio dei nomi specifico, questo esempio produce lo spazio dei nomi predefinito, `LibUtil`.  
  
```  
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /out:LibUtil.dll  
```  
  
 Per un nome più descrittivo \(in base alle indicazioni di denominazione *NomeFornitore*.*NomeLibreria*\), l'esempio seguente esegue l'override del nome del file di assembly e del nome di spazio dei nomi predefiniti.  
  
```  
tlbimp LibUtil.tlb /primary /keyfile:CompanyA.snk /namespace:CompanyA.LibUtil /out:CompanyA.LibUtil.dll  
```  
  
 L'esempio seguente importa `MyLib.tlb`, che fa riferimento a `CompanyA.LibUtil.dll` e firma l'assembly `CompanyB.MyLib.dll` con un nome sicuro usando il file di chiave `CompanyB.snk`.  Lo spazio dei nomi, `CompanyB.MyLib`, esegue l'override del nome di spazio dei nomi predefinito.  
  
```  
tlbimp MyLib.tlb /primary /keyfile:CompanyB.snk /namespace:CompanyB.MyLib /reference:CompanyA.LibUtil.dll /out:CompanyB.MyLib.dll  
```  
  
## Vedere anche  
 [How to: Register Primary Interop Assemblies](../../../docs/framework/interop/how-to-register-primary-interop-assemblies.md)