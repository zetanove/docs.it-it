---
title: "How to: Create COM Wrappers | Microsoft Docs"
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
  - "COM,wrappers creating"
  - "COM,wrappers Visual Studio"
ms.assetid: bdf89bea-1623-45ee-a57b-cf7c90395efa
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Create COM Wrappers
È possibile creare wrapper COM \(Component Object Model\) utilizzando le funzionalità di [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] o gli strumenti di .NET Framework Tlbimp.exe e Regasm.exe.  Entrambi i metodi generano due tipi di wrapper COM:  
  
-   Un [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md) da una libreria di tipi per eseguire un oggetto COM nel codice gestito.  
  
-   Un [COM Callable Wrapper](../../../docs/framework/interop/com-callable-wrapper.md) con le impostazioni del Registro di sistema richieste per eseguire un oggetto gestito in un'applicazione nativa.  
  
 In [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)], è possibile aggiungere il wrapper COM come riferimento al progetto.  
  
## Wrapping di oggetti COM in un'applicazione gestita  
  
#### Per creare un Runtime Callable Wrapper utilizzando Visual Studio  
  
1.  Aprire il progetto per l'applicazione gestita.  
  
2.  Scegliere **Mostra tutti i file** dal menu **Progetto**.  
  
3.  Scegliere **Aggiungi riferimento** dal menu **Progetto**.  
  
4.  Nella finestra di dialogo Aggiungi riferimento fare clic sulla scheda **COM**, selezionare il componente che si desidera utilizzare e scegliere **OK**.  
  
     In **Esplora soluzioni** verificare che il componente COM sia stato aggiunto nella cartella Riferimenti nel progetto.  
  
 È ora possibile scrivere codice per accedere all'oggetto COM.  È possibile iniziare dichiarando l'oggetto, ad esempio con un'istruzione `Imports` per [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] o con un'istruzione `Using` per [!INCLUDE[csprcslong](../../../includes/csprcslong-md.md)].  
  
> [!NOTE]
>  Se si desidera programmare i componenti Microsoft Office, installare innanzitutto gli [Assembly di interoperabilità primari di Microsoft Office](http://go.microsoft.com/fwlink/?LinkId=50479) \(informazioni in lingua inglese\) dall'Area download Microsoft.  Nel passaggio 4 selezionare la versione più recente della libreria di oggetti disponibile per il prodotto Office desiderato, ad esempio **Libreria oggetti di Microsoft Word 11.0**.  [](http://msdn.microsoft.com/it-it/c9d2a8b9-69df-4c0b-90ca-4d85bae063c4)  
  
#### Per creare un Runtime Callable Wrapper utilizzando gli strumenti di .NET Framework  
  
-   Eseguire lo strumento [Tlbimp.exe \(Type Library Importer\)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md).  
  
 Questo strumento crea un assembly contenente metadati di runtime per i tipi definiti nella libreria di tipi originale.  
  
## Wrapping di oggetti gestiti in un'applicazione nativa  
  
#### Per creare un COM Callable Wrapper utilizzando Visual Studio  
  
1.  Creare un progetto Libreria di classi per la classe gestita che si desidera eseguire nel codice nativo.  La classe deve disporre di un costruttore predefinito.  
  
     Verificare che nel file AssemblyInfo sia contenuto un numero di versione in quattro parti completo.  Questo numero è obbligatorio per gestire il controllo delle versioni nel Registro di sistema di Windows.  Per ulteriori informazioni sui numeri di versione, vedere [Controllo delle versioni degli assembly](../../../docs/framework/app-domains/assembly-versioning.md).  
  
2.  Scegliere **Proprietà** dal menu **Progetto**.  
  
3.  Fare clic sulla scheda **Compila**.  
  
4.  Selezionare la casella di controllo **Registra per interoperabilità COM**.  
  
 Quando si compila il progetto, l'assembly viene registrato automaticamente per l'interoperabilità COM.  Se si compila un'applicazione nativa in [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)], è possibile utilizzare l'assembly scegliendo **Aggiungi riferimento** dal menu **Progetto**.  
  
#### Per creare un COM Callable Wrapper utilizzando gli strumenti di .NET Framework  
  
-   Eseguire lo strumento [Regasm.exe \(Assembly Registration Tool\)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md).  
  
 Questo strumento legge i metadati dell'assembly e aggiunge le voci necessarie nel Registro di sistema.  I client COM possono pertanto creare classi .NET Framework in modo trasparente.  È possibile utilizzare l'assembly come se fosse una classe COM nativa.  
  
 È possibile eseguire Regasm.exe su un assembly contenuto in qualsiasi directory e quindi eseguire lo [Gacutil.exe \(Global Assembly Cache Tool\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) per spostarlo nella Global Assembly Cache.  Lo spostamento dell'assembly non invalida le voci del Registro di sistema relative al percorso, poiché viene sempre esaminata la Global Assembly Cache se l'assembly non viene trovato altrove.  
  
## Vedere anche  
 [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md)   
 [COM Callable Wrapper](../../../docs/framework/interop/com-callable-wrapper.md)