---
title: Comando dotnet-clean | Microsoft Docs
description: Il comando dotnet-clean consente di pulire la directory corrente.
keywords: dotnet-clean, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 01/31/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: eff65fa1-bab4-4421-8260-d0a284b690b2
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 12144def2095246bb6611522b3dbc2d7e441135a

---

#<a name="dotnet-clean"></a>dotnet-clean

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>Nome 
`dotnet-clean`: pulisce l'output di un progetto. 

## <a name="synopsis"></a>Riepilogo

`dotnet clean [--help] [--output]  [--framework]  
    [--configuration]  [--verbosity]
    [<project>]`

## <a name="description"></a>Descrizione
Il comando `dotnet clean` pulirà l'output della compilazione precedente. Viene implementato come una destinazione di MSBuild, pertanto il progetto verrà valutato. Vengono puliti solo gli output creati durante la compilazione. Vengono pulite sia la cartella intermedia (`obj`) che quella dell'output finale (`bin`). 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui sono stati posizionati i file binari compilati. È necessario definire anche `--framework` quando si specifica questa opzione. Se questa proprietà non è stata specificata durante la fase di compilazione, non è necessario specificarla per la pulitura.

`-f|--framework <FRAMEWORK>`

Framework specificato in fase di compilazione. Se questa proprietà non è stata specificata durante la fase di compilazione, non è necessario specificarla per la pulitura. Il framework deve essere definito nel [file di progetto](csproj.md).

`-c|--configuration [Debug|Release]`

Definisce una configurazione in cui è stata eseguita la compilazione.  Se omessa, il valore predefinito è `Debug`. Se questa proprietà non è stata specificata durante la fase di compilazione, non è necessario specificarla per la pulitura.

`-v|--verbosity [Quiet|Minimal|Normal|Diag]`

Definisce il livello di dettaglio da usare per la chiamata del comando `dotnet clean`. I livelli di dettaglio corrispondono ai [livelli di dettaglio di MSBuild](https://msdn.microsoft.com/en-us/library/ms164311.aspx) standard. 


## <a name="examples"></a>Esempi

Pulire una compilazione predefinita del progetto:

`dotnet clean`

Pulire un progetto compilato con la configurazione di tipo Versione:

`dotnet clean --configuration Release`



<!--HONumber=Feb17_HO2-->


