---
title: Assembly e Global Assembly Cache (Visual Basic) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: fcf78ff1-f1ab-4a5d-b6d8-00d2046b6c80
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0b712132becfe47d50d1c06c0e8fd9940b8035e9
ms.lasthandoff: 03/13/2017

---
# <a name="assemblies-and-the-global-assembly-cache-visual-basic"></a>Assembly e Global Assembly Cache (Visual Basic)
Gli assembly costituiscono l'unità fondamentale della distribuzione, del controllo delle versioni, del riutilizzo, dell'ambito di attivazione e delle autorizzazioni di sicurezza per un'applicazione basata su .NET. Gli assembly hanno il formato di un file eseguibile (con estensione exe) o di libreria a collegamento dinamico (con estensione dll) e costituiscono i blocchi predefiniti di .NET Framework. Gli assembly forniscono al Common Language Runtime le informazioni necessarie per riconoscere le implementazioni dei tipi. Un assembly può essere considerato come una raccolta di tipi e risorse che formano un'unità logica di funzionalità e che sono creati per interagire.  
  
 Gli assembly possono contenere uno o più moduli. È ad esempio possibile pianificare i progetti di grandi dimensioni in modo tale che diversi sviluppatori lavorino su moduli distinti che, una volta raggruppati, costituiranno un singolo assembly. Per altre informazioni sui moduli, vedere l'argomento [Procedura: Compilare un assembly su più file](https://msdn.microsoft.com/library/226t7yxe).  
  
 Di seguito sono riportate le proprietà degli assembly:  
  
-   Gli assembly vengono implementati come file con estensione exe o dll.  
  
-   È possibile condividere un assembly tra più applicazioni inserendolo nella Global Assembly Cache. Prima di inserirlo nella Global Assembly Cache, è necessario assegnare a un assembly un nome sicuro. Per altre informazioni, vedere [Assembly con nomi sicuri](https://msdn.microsoft.com/library/wd40t7ad).  
  
-   Gli assembly vengono caricati in memoria solo se sono richiesti. Se non sono usati, non vengono caricati. Questo significa che gli assembly rappresentano un modo efficace per gestire le risorse nei progetti di maggiori dimensioni.  
  
-   È possibile ottenere informazioni su un assembly a livello di codice tramite reflection. Per altre informazioni, vedere [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md).  
  
-   Se si vuole caricare un assembly solo per esaminarlo, usare un metodo quale <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A>.  
  
## <a name="assembly-manifest"></a>Manifesto dell'assembly  
 All'interno di ogni assembly è presente un *manifesto dell'assembly*. Il manifesto dell'assembly è simile a un indice e contiene quanto segue:  
  
-   L'identità dell'assembly, ovvero il nome e la versione.  
  
-   Una tabella di file in cui sono descritti tutti gli altri file che costituiscono l'assembly, ad esempio eventuali altri assembly creati su cui si basano il file con estensione exe o dll o anche i file bitmap o Readme.  
  
-   Un *elenco di riferimenti all'assembly*, ovvero un elenco di tutte le dipendenze esterne. Può trattarsi di file con estensione dll o di altri file richiesti dall'applicazione e che possono essere creati da altri sviluppatori. I riferimenti all'assembly contengono riferimenti a oggetti sia privati che globali. Gli oggetti globali si trovano nella Global Assembly Cache, una zona disponibile per altre applicazioni, simile alla directory System32. Lo spazio dei nomi <xref:Microsoft.VisualBasic?displayProperty=fullName> è un esempio di assembly nella Global Assembly Cache. Gli oggetti privati devono trovarsi in una directory di livello pari o inferiore a quello della directory nella quale è installata l'applicazione.  
  
 Poiché gli assembly contengono informazioni sul contenuto, sul controllo delle versioni e sulle dipendenze, per funzionare in modo corretto le applicazioni create con Visual Basic non si basano sui valori del Registro di sistema. Gli assembly riducono i conflitti tra file con estensione dll e rendono le applicazioni più affidabili e facili da distribuire. In molti casi, è possibile installare un'applicazione basata su .NET semplicemente copiandone i file nel computer di destinazione.  
  
 Per altre informazioni, vedere [Manifesto dell'assembly](https://msdn.microsoft.com/library/1w45z383).  
  
## <a name="adding-a-reference-to-an-assembly"></a>Aggiunta di un riferimento a un assembly  
 Per usare un assembly, è necessario aggiungervi un riferimento. Successivamente, eseguire l'[istruzione Imports](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) per scegliere lo spazio dei nomi degli elementi da usare. Dopo che l'utente ha fatto riferimento a un assembly e lo ha importato, tutte le classi, le proprietà, i metodi e gli altri membri accessibili dei relativi spazi dei nomi risulteranno disponibili per l'applicazione, come se il relativo codice facesse parte del file di origine.  
  
## <a name="creating-an-assembly"></a>Creazione di un assembly  
 Compilare l'applicazione eseguendola dalla riga di comando usando il compilatore della riga di comando. Per informazioni dettagliate sulla compilazione degli assembly dalla riga di comando, vedere [Compilazione dalla riga di comando](../../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md).  
  
> [!NOTE]
>  Per compilare un assembly in Visual Studio, scegliere **Compila** dal menu **Compila**.  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly in Common Language Runtime](https://msdn.microsoft.com/library/k3677y81)   
 [Assembly Friend (Visual Basic)](friend-assemblies.md)   
 [Procedura: Condividere un assembly con altre applicazioni (Visual Basic)](how-to-share-an-assembly-with-other-applications.md)   
 [Procedura: Caricare e scaricare gli assembly (Visual Basic)](how-to-load-and-unload-assemblies.md)   
 [Procedura: Determinare se un file è un assembly (Visual Basic)](how-to-determine-if-a-file-is-an-assembly.md)   
 [Procedura: Creare e usare assembly dalla riga di comando (Visual Basic)](how-to-create-and-use-assemblies-using-the-command-line.md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti in Visual Studio (Visual Basic)](walkthrough-embedding-types-from-managed-assemblies-in-vs.md)   
 [Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office in Visual Studio (Visual Basic)](walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-vs.md)
