---
title: "Semplificazione del debug di un&#39;immagine | Microsoft Docs"
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
  - "immagini [.NET Framework], debug"
  - "immagine eseguibile per il debug"
  - "debug [.NET Framework], immagini eseguibili per"
ms.assetid: 7d90ea7a-150f-4f97-98a7-f9c26541b9a3
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Semplificazione del debug di un&#39;immagine
Quando si compila codice non gestito, è possibile configurare un'immagine eseguibile per il debug impostando i parametri IDE o le opzioni della riga di comando.  È possibile utilizzare, ad esempio, l'opzione della riga di comando \/**Zi** in Visual C\+\+ per richiedere di generare i file di simboli dell'esecuzione del debug \(estensione file pdb\).  In modo analogo, l'opzione della riga di comando \/**Od** indica al compilatore di disabilitare l'ottimizzazione.  Il codice risultante è più lento in fase di esecuzione, tuttavia l'esecuzione del debug risulta più semplice, se necessaria.  
  
 Quando si compila il codice di gestione .NET Framework, compilatori quali Visual C\+\+, Visual Basic e C\# compilano il programma di origine in Microsoft Intermediate Language \(MSIL\).  MSIL viene quindi sottoposto a compilazione JIT, immediatamente prima dell'esecuzione, nel codice macchina sorgente.  Come con il codice non gestito, è possibile configurare un'immagine eseguibile per l'esecuzione del debug impostando i parametri IDE o le opzioni della riga di comando.  È inoltre possibile configurare la compilazione JIT per l'esecuzione del debug in modo del tutto analogo.  
  
 Questa configurazione JIT presenta due aspetti:  
  
-   È possibile richiedere al compilatore JIT di generare informazioni di registrazione.  In questo modo il debugger può trovare le corrispondenze tra una catena di MSIL e l'equivalente codice macchina e di tenere traccia della posizione di archiviazione delle variabili locali e degli argomenti delle funzioni.  Dal momento che, in .NET Framework versione 2.0, il compilatore JIT genera sempre informazioni di registrazione, non è necessario che tale operazione venga richiesta.  
  
-   È possibile richiedere al compilatore JIT di non ottimizzare il codice macchina risultante.  
  
 In genere, il compilatore che genera l'MSIL imposta queste opzioni del compilatore JIT in modo corretto in base ai parametri IDE o alle opzioni della riga di comando specificate, ad esempio \/**Od**.  
  
 In alcuni casi è possibile modificare il comportamento del compilatore JIT in modo che sia più facile eseguire il debug del codice macchina da esso generato.  È possibile ad esempio generare informazioni di registrazione JIT per una build finale o per l'ottimizzazione dei controlli.  A tale scopo, è possibile utilizzare un file di inizializzazione \(con estensione ini\).  
  
 Se ad esempio il nome dell'assembly su cui si desidera eseguire il debug è MyApp.exe, creare nella stessa cartella di MyApp.exe un file di testo denominato MyApp.ini contenente le tre righe riportate di seguito:  
  
```  
[.NET Framework Debugging Control]  
GenerateTrackingInfo=1  
AllowOptimize=0  
```  
  
 È possibile impostare il valore di ciascuna opzione su 0 o 1 e qualsiasi opzione non presente utilizza 0 per impostazione predefinita.  Impostando `GenerateTrackingInfo` su 1 e `AllowOptimize` su 0, l'esecuzione del debug risulterà più facile.  
  
> [!NOTE]
>  Benché in .NET Framework versione 2.0 il compilatore JIT generi sempre informazioni di registrazione indipendentemente dal valore di `GenerateTrackingInfo`, il valore `AllowOptimize` è ancora operativo.  Se si utilizza il [Ngen.exe \(Native Image Generator\)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) per precompilare l'immagine nativa senza ottimizzazione, il file ini deve essere contenuto nella cartella di destinazione con `AllowOptimize=0` quando viene eseguito Ngen.exe.  Se è stato precompilato un assembly senza ottimizzazione, è necessario rimuovere il codice precompilato utilizzando l'opzione **\/uninstall** di NGen.exe prima di rieseguire Ngen.exe per precompilare il codice come ottimizzato.  Se il file ini non è contenuto nella cartella, per impostazione predefinita Ngen.exe precompila il codice come ottimizzato.  
  
> [!NOTE]
>  <xref:System.Diagnostics.DebuggableAttribute?displayProperty=fullName> controlla le impostazioni per un assembly.  **DebuggableAttribute** include due campi che registrano le impostazioni che determinano se il compilatore JIT deve ottimizzare e\/o generare informazioni di registrazione.  In .NET Framework versione 2.0 il compilatore JIT genera sempre informazioni di registrazione.  
  
> [!NOTE]
>  Per una build finale, i compilatori non impostano alcun **DebuggableAttribute**.  Per impostazione predefinita, il compilatore JIT genera codice macchina con le prestazioni migliori e per il quale l'esecuzione del debug risulta più difficile.  Se si attiva la registrazione JIT si riducono leggermente le prestazioni, mentre se si disabilita l'ottimizzazione si riducono notevolmente.  
  
> [!NOTE]
>  **DebuggableAttribute** si applica a un intero assembly per volta, non ai singoli moduli all'interno dell'assembly.  Gli strumenti di sviluppo devono quindi associare gli attributi personalizzati al token di metadati dell'assembly, se è già stato creato un assembly, oppure alla classe denominata **System.Runtime.CompilerServices.AssemblyAttributesGoHere**.  Lo strumento ALink promuove quindi questi attributi **DebuggableAttribute** da ciascun modulo all'assembly di cui diventano parte.  In caso di conflitto, l'operazione ALink non viene eseguita correttamente.  
  
> [!NOTE]
>  Nella versione 1.0 di .NET Framework il compilatore Microsoft Visual C\+\+ aggiunge **DebuggableAttribute** quando vengono specificate le opzioni del compilatore **\/clr** e **\/Zi** .  Nella versione 1.1 di .NET Framework è necessario aggiungere **DebugabbleAttribute** manualmente al codice oppure utilizzare l'opzione del linker **\/ASSEMBLYDEBUG**.  
  
## Vedere anche  
 [Debugging, Tracing, and Profiling](../../../docs/framework/debug-trace-profile/index.md)   
 [Enabling JIT\-Attach Debugging](../../../docs/framework/debug-trace-profile/enabling-jit-attach-debugging.md)   
 [Enabling Profiling](http://msdn.microsoft.com/it-it/3b669676-f0e0-4ebf-8674-68986dd2020d)