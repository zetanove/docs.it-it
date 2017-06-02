---
title: "Strumento di analisi composizione (Mefx) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Strumento di analisi composizione [MEF]"
  - "MEF, Strumento di analisi composizione"
  - "Mefx [MEF], Strumento di analisi composizione"
ms.assetid: c48a7f93-83bb-4a06-aea0-d8e7bd1502ad
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Strumento di analisi composizione (Mefx)
Lo strumento di analisi composizione \(Mefx\) è un'applicazione della riga di comando che analizza i file di libreria \(DLL\) e di applicazione \(EXE\) che contengono le parti MEF \(Managed Extensibility Framework\). Lo scopo principale di Mefx è fornire agli sviluppatori un modo per diagnosticare gli errori di composizione nelle relative applicazioni MEF senza la necessità di aggiungere codice di analisi complesso all'applicazione stessa. Può essere utile anche per comprendere le parti di una libreria fornita da terze parti. Questo argomento descrive come usare Mefx e fornisce un riferimento per la relativa sintassi.  
  
<a name="getting_mefx"></a>   
## Come ottenere Mefx  
 Mefx è disponibile in Codeplex in [Managed Extensibility Framework](http://go.microsoft.com/fwlink/?LinkID=187078). Scaricare e decomprimere semplicemente lo strumento.  
  
<a name="basic_syntax"></a>   
## Sintassi di base  
 Mefx viene richiamato dalla riga di comando nel formato seguente:  
  
```  
mefx [files and directories] [action] [options]  
```  
  
 Il primo set di argomenti specifica i file e le directory da cui caricare le parti per l'analisi. Specificare un file con l'opzione `/file:` e una directory con l'opzione `/directory:`. È possibile specificare più file e directory, come illustrato nell'esempio seguente.  
  
```  
mefx /file:MyAddIn.dll /directory:Program\AddIns [action...]  
```  
  
> [!NOTE]
>  Ogni file dll o exe deve essere caricato solo una volta. Se un file viene caricato più volte, lo strumento può restituire informazioni non corrette.  
  
 Dopo l'elenco dei file e delle directory è necessario specificare un comando e tutte le opzioni per il comando.  
  
<a name="listing_available_parts"></a>   
## Elenco delle parti disponibili  
 Usare l'azione `/parts` per elencare tutte le parti dichiarate nei file caricati. Il risultato è un semplice elenco di nomi di parti.  
  
```  
mefx /file:MyAddIn.dll /parts  
MyAddIn.AddIn  
MyAddIn.MemberPart  
```  
  
 Per altre informazioni sulle parti, usare l'opzione `/verbose`. Verranno restituite altre informazioni per tutte le parti disponibili. Per ottenere altre informazioni su una singola parte, usare l'azione `/type` invece di `/parts`.  
  
```  
mefx /file:MyAddIn.dll /type:MyAddIn.AddIn /verbose  
[Part] MyAddIn.MemberPart from: AssemblyCatalog (Assembly=" MyAddIn, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Export] MyAddIn.MemberPart (ContractName=" MyAddIn.MemberPart")  
```  
  
<a name="listing_imports_and_exports"></a>   
## Elenco delle importazioni e delle esportazioni  
 Le azioni `/imports` e `/exports` elencheranno rispettivamente tutte le parti importate e tutte le parti esportate. È anche possibile elencare le parti che importano o esportano un tipo specifico usando le azioni `/importers` o `/exporters`.  
  
```  
mefx /file:MyAddIn.dll /importers:MyAddin.MemberPart  
MyAddin.AddIn  
```  
  
 A queste azioni è anche possibile applicare l'opzione `/verbose`.  
  
<a name="finding_rejected_parts"></a>   
## Individuazione delle parti rifiutate  
 Una volta caricate le parti disponibili, Mefx usa il motore di composizione MEF per comporle. Le parti che non possono essere composte correttamente vengono definite *rifiutate*. Per elencare tutte le parti rifiutate, usare l'azione `/rejected`.  
  
 È possibile usare l'opzione `/verbose` con l'azione `/rejected` per stampare le informazioni dettagliate relative alle parti rifiutate. Nell'esempio seguente la DLL `ClassLibrary1` contiene la parte `AddIn` che importa le parti `MemberPart` e `ChainOne`.`ChainOne` importa `ChainTwo`, ma `ChainTwo` non esiste. Ciò significa che `ChainOne` viene rifiutato causando il rifiuto di `AddIn`.  
  
```  
mefx /file:ClassLibrary1.dll /rejected /verbose  
```  
  
 Di seguito viene mostrato l'output completo del comando precedente:  
  
```  
[Part] ClassLibrary1.AddIn from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Export] ClassLibrary1.AddIn (ContractName="ClassLibrary1.AddIn")  
  [Import] ClassLibrary1.AddIn.memberPart (ContractName="ClassLibrary1.MemberPart")  
    [SatisfiedBy] ClassLibrary1.MemberPart (ContractName="ClassLibrary1.MemberPart") from: ClassLibrary1.MemberPart from: AssemblyCatalog (Assembly="ClassLibrar  
y1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Import] ClassLibrary1.AddIn.chain (ContractName="ClassLibrary1.ChainOne")  
    [Exception] System.ComponentModel.Composition.ImportCardinalityMismatchException: No valid exports were found that match the constraint '((exportDefinition.ContractName == "ClassLibrary1.ChainOne") AndAlso (exportDefinition.Metadata.ContainsKey("ExportTypeIdentity") AndAlso "ClassLibrary1.ChainOne".Equals(exportDefinition.Metadata.get_Item("ExportTypeIdentity"))))', invalid exports may have been rejected.  
   at System.ComponentModel.Composition.Hosting.ExportProvider.GetExports(ImportDefinition definition, AtomicComposition atomicComposition)  
   at Microsoft.ComponentModel.Composition.Diagnostics.CompositionInfo.AnalyzeImportDefinition(ExportProvider host, IEnumerable`1 availableParts, ImportDefinition id)  
    [Unsuitable] ClassLibrary1.ChainOne (ContractName="ClassLibrary1.ChainOne")  
from: ClassLibrary1.ChainOne from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
      [Because] PartDefinitionIsRejected, The part providing the export is rejected because of other issues.  
  
[Part] ClassLibrary1.ChainOne from: AssemblyCatalog (Assembly="ClassLibrary1, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")  
  [Primary Rejection]  
  [Export] ClassLibrary1.ChainOne (ContractName="ClassLibrary1.ChainOne")  
  [Import] ClassLibrary1.ChainOne.chain (ContractName="ClassLibrary1.ChainTwo")  
    [Exception] System.ComponentModel.Composition.ImportCardinalityMismatchException: No valid exports were found that match the constraint '((exportDefinition.ContractName == "ClassLibrary1.ChainTwo") AndAlso (exportDefinition.Metadata.ContainsKey("ExportTypeIdentity") AndAlso "ClassLibrary1.ChainTwo".Equals(exportDefinition.Metadata.get_Item("ExportTypeIdentity"))))', invalid exports may have been rejected.  
   at System.ComponentModel.Composition.Hosting.ExportProvider.GetExports(ImportDefinition definition, AtomicComposition atomicComposition)  
   at Microsoft.ComponentModel.Composition.Diagnostics.CompositionInfo.AnalyzeImportDefinition(ExportProvider host, IEnumerable`1 availableParts, ImportDefinition id)  
```  
  
 Le informazioni interessanti sono contenute nei risultati `[Exception]` e `[Unsuitable]`. Il risultato `[Exception]` fornisce informazioni sul motivo per cui una parte è stata rifiutata. Il risultato `[Unsuitable]` indica il motivo per cui non è possibile usare una parte con una diversa corrispondenza per soddisfare un'importazione. In questo caso il motivo è dovuto al fatto che la parte stessa è stata rifiutata a causa di importazioni mancanti.  
  
<a name="analyzing_primary_causes"></a>   
## Analisi delle cause principali  
 Se alcune parti sono collegate in una lunga catena di dipendenza, un problema che riguarda la parte finale può causare il rifiuto dell'intera catena. La diagnosi di questi problemi può essere difficile perché la causa radice dell'errore non è sempre ovvia. Per risolvere il problema, è possibile usare l'azione `/causes`, che tenta di individuare la causa radice di qualsiasi rifiuto a cascata.  
  
 Se si usa l'azione `/causes` dell'esempio precedente, vengono elencate solo le informazioni relative a `ChainOne`, la cui importazione non soddisfatta rappresenta la causa radice del rifiuto di `AddIn`. L'azione `/causes` può essere usata sia con l'opzione normale che con l'opzione `/verbose`.  
  
> [!NOTE]
>  Nella maggior parte dei casi, Mefx sarà in grado di diagnosticare la causa radice di un errore a cascata. Tuttavia, nei casi in cui le parti vengono aggiunte a un contenitore a livello di codice, nei casi che riguardano contenitori gerarchici o nei casi che riguardano implementazioni personalizzate di `ExportProvider`, Mefx non sarà in grado di diagnosticare la causa. In generale, i casi descritti precedentemente devono essere evitati laddove possibile, poiché la diagnosi degli errori è generalmente complessa.  
  
<a name="white_lists"></a>   
## Elenchi degli elementi consentiti  
 L'opzione `/whitelist` consente di specificare un file di testo che elenca le parti di cui è previsto il rifiuto. I rifiuti imprevisti verranno quindi contrassegnati. Ciò può essere utile quando si analizza una libreria incompleta o una sottolibreria in cui mancano alcune dipendenze. L'opzione `/whitelist` può essere applicata alle azioni `/rejected` o `/causes`.  
  
 Si consideri un file denominato test.txt che contiene il testo "ClassLibrary1.ChainOne". Se si esegue l'azione `/rejected` con l'opzione `/whitelist` dell'esempio precedente, verrà generato l'output seguente:  
  
```  
mefx /file:ClassLibrary1.dll /rejected /whitelist:test.txt  
[Unexpected] ClassLibrary1.AddIn  
ClassLibrary1.ChainOne  
```