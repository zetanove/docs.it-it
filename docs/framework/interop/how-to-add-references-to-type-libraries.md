---
title: "How to: Add References to Type Libraries | Microsoft Docs"
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
  - "importing type library"
  - "interop assemblies, generating"
  - "type libraries"
  - "COM interop, importing type library"
ms.assetid: f5cfa6ba-cc25-4017-82cd-ba7391859113
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Add References to Type Libraries
Quando si aggiunge un riferimento a una libreria dei tipi, Visual Studio genera un assembly di interoperabilità contenente metadati.  Se è disponibile un assembly di interoperabilità primario, prima della generazione di un nuovo assembly di interoperabilità in Visual Studio verrà utilizzato l'assembly esistente.  
  
### Per aggiungere un riferimento a una libreria dei tipi in Visual Studio  
  
1.  Installare il file COM DLL o EXE nel computer, a meno che non si esegua l'installazione con un file Setup.exe di Windows.  
  
2.  Scegliere **Progetto**, quindi **Aggiungi riferimento**.  
  
3.  In Gestione riferimenti scegliere **COM**.  
  
4.  Selezionare la libreria dei tipi nell'elenco o cercare il file con estensione tlb.  
  
5.  Scegliere **OK**.  
  
6.  In Esplora soluzioni, aprire il menu di scelta rapida per il riferimento appena aggiunto e quindi scegliere **Proprietà**.  
  
7.  Nella finestra **Proprietà** verificare che la proprietà **Incorpora tipi di interoperabilità** sia impostata su **True**.  In questo modo Visual Studio incorporerà nei file eseguibili le informazioni sui tipi COM, eliminando l'esigenza di distribuire assembly di interoperabilità primari con l'app.  
  
> [!NOTE]
>  Le opzioni del menu e della finestra di dialogo possono variare a seconda della versione di Visual Studio in uso.  
  
### Per aggiungere un riferimento a una libreria dei tipi per la compilazione da riga di comando  
  
1.  Generare un assembly di interoperabilità come descritto in [How to: Generate Interop Assemblies from Type Libraries](../../../docs/framework/interop/how-to-generate-interop-assemblies-from-type-libraries.md).  
  
2.  Usare [\/link \(Link to COM Assembly\)](../Topic/-link%20\(C%23%20Compiler%20Options\).md) o l'opzione del compilatore [\/link](../Topic/-link%20\(Visual%20Basic\).md) con il nome dell'assembly di interoperabilità per incorporare informazioni sui tipi COM nei file eseguibili.  
  
## Vedere anche  
 [Importing a Type Library as an Assembly](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)   
 [Exposing COM Components to the .NET Framework](../../../docs/framework/interop/exposing-com-components.md)   
 [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office](../Topic/Walkthrough:%20Embedding%20Type%20Information%20from%20Microsoft%20Office%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [\/link \(Link to COM Assembly\)](../Topic/-link%20\(C%23%20Compiler%20Options\).md)   
 [\/link](../Topic/-link%20\(Visual%20Basic\).md)