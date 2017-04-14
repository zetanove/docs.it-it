---
title: "Nomi degli assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], nomi"
  - "nomi [.NET Framework], assembly"
ms.assetid: 8f8c2c90-f15d-400e-87e7-a757e4f04d0e
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Nomi degli assembly
Il nome di un assembly viene archiviato in metadati e influisce in modo significativo sull'ambito dell'assembly e su come questo viene utilizzato dalle applicazioni.  Un assembly con nome sicuro dispone di un nome completo che include il nome, le impostazioni cultura, la chiave pubblica e il numero di versione dell'assembly.  Tale nome viene spesso definito nome di visualizzazione e per gli assembly caricati può essere ottenuto mediante la proprietà <xref:System.Reflection.Assembly.FullName%2A>.  
  
 Tali informazioni vengono utilizzate dal runtime per individuare l'assembly e distinguerlo da altri assembly aventi lo stesso nome.  Un assembly con nome sicuro denominato `myTypes` può avere, ad esempio, il seguente nome completo:  
  
```  
myTypes, Version=1.0.1234.0, Culture=en-US, PublicKeyToken=b77a5c561934e089c, ProcessorArchitecture=msil  
```  
  
> [!NOTE]
>  L'architettura del processore viene aggiunta all'identità assembly in .NET Framework versione 2.0 in modo che vengano accettate versioni di assembly specifiche del processore.  È possibile creare versioni di assembly la cui identità differisce solo per architettura del processore, ad esempio versioni specifiche del processore a 32 e a 64 bit.  L'architettura del processore non è richiesta per i nomi sicuri.  Per ulteriori informazioni, vedere <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A?displayProperty=fullName>.  
  
 Dal nome completo riportato in esempio si evince che l'assembly `myTypes` dispone di un nome sicuro con un token di chiave pubblica, del valore di impostazioni cultura relativo all'Inglese Stati Uniti e presenta un numero di versione pari a 1.0.1234.0.  L'architettura del processore è "msil", ovvero è basata su codice a 32 bit o a 64 bit con compilazione JIT a seconda del sistema operativo e del processore.  
  
 Quando il codice richiede i tipi contenuti in un assembly, dovrà specificare un nome di assembly completo.  Tale evenienza è definita associazione completa.  Quando si fa riferimento a un assembly in .NET Framework, non è possibile avvalersi dell'associazione parziale, che si ottiene specificando il solo nome dell'assembly.  
  
 Anche quando da un assembly si fa riferimento agli assembly che costituiscono .NET Framework, sarà necessario specificare i nomi completi di tali assembly.  Per fare riferimento alla versione 1.0 dell'assembly System.Data di .NET Framework, occorre ad esempio specificare:  
  
```  
  
System.data, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089  
  
```  
  
 Si noti che la versione corrisponde al numero di versione di tutti gli assembly di .NET Framework forniti con .NET Framework versione 1.0.  Per gli assembly di .NET Framework, il valore delle impostazioni cultura è sempre quello delle impostazioni cultura di sistema e la chiave pubblica è sempre quella mostrata nell'esempio sopra riportato.  
  
 Per includere un riferimento a un assembly in un file di configurazione al fine di impostare un listener di traccia, ad esempio, si includerà il nome completo dell'assembly di sistema di .NET Framework:  
  
```  
<add name="myListener" type="System.Diagnostics.TextWriterTraceListener, System, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
```  
  
> [!NOTE]
>  La distinzione tra maiuscole e minuscole dei nomi degli assembly non risulta rilevante in Common Language Runtime durante l'associazione a un assembly, ma eventuali distinzioni tra maiuscole e minuscole nei nomi degli assembly vengono conservate.  Tali distinzioni assumono rilevanza per diversi strumenti di [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  Si consiglia pertanto di gestire i nomi degli assembly come se la distinzione tra maiuscole e minuscole fosse sempre rilevante.  
  
## Denominazione dei componenti dell'applicazione  
 Per determinare l'identità di un assembly, Common Language Runtime non prende in considerazione il nome file.  È necessario che Common Language Runtime sia in grado di individuare con chiarezza l'identità di un assembly, costituita dal nome, dalla versione, dalle impostazioni cultura e dal nome sicuro dell'assembly.  
  
 Nel caso, ad esempio, di un assembly denominato myAssembly.exe che fa riferimento a un assembly denominato myAssembly.dll, l'associazione sarà corretta se si esegue myAssembly.exe.  Se però un'altra applicazione esegue myAssembly.exe utilizzando il metodo <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=fullName>, quando myAssembly.exe avanzerà la richiesta di associazione a "myAssembly", Common Language Runtime determinerà che "myAssembly" è già caricato. In questo caso, il file myAssembly.dll non viene caricato.  Poiché in myAssembly.exe non è presente il tipo richiesto, si verifica un'eccezione <xref:System.TypeLoadException>.  
  
 Per evitare il verificarsi di questo problema, assicurarsi che agli assembly che costituiscono l'applicazione non sia stato assegnato lo stesso nome oppure salvare gli assembly omonimi in directory diverse.  
  
> [!NOTE]
>  Se si inserisce un assembly con nome sicuro nella Global Assembly Cache, il nome file dell'assembly dovrà corrispondere al nome dell'assembly, fatta eccezione per l'estensione del nome file che sarà, ad esempio, exe o dll.  Se ad esempio il nome file di un assembly è myAssembly.dll, è necessario che il nome dell'assembly sia myAssembly.  Agli assembly privati distribuiti solo nella directory radice dell'applicazione è possibile assegnare un nome di assembly diverso dal nome file.  
  
## Vedere anche  
 [Procedura: determinare il nome completo di un assembly](../../../docs/framework/app-domains/how-to-determine-assembly-fully-qualified-name.md)   
 [Creazione degli assembly](../../../docs/framework/app-domains/create-assemblies.md)   
 [Assembly con nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md)   
 [Global Assembly Cache](../../../docs/framework/app-domains/gac.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)