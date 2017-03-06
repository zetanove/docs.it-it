---
title: Comando dotnet-publish | Microsoft Docs
description: Il comando dotnet-publish consente di pubblicare il progetto .NET Core in una directory.
keywords: dotnet-publish, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f2ef275a-7c5e-430a-8c30-65f52af62771
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 0d222382640fc239760f8f51c69f1f306674d7ca

---

#<a name="dotnet-publish-net-core-tools-rc4"></a>dotnet-publish (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [dotnet-publish](../../tools/dotnet-publish.md).

## <a name="name"></a>Nome

`dotnet-publish`: comprime l'applicazione e tutte le relative dipendenze in una cartella, preparandole per la pubblicazione.

## <a name="synopsis"></a>Riepilogo

`dotnet publish [project] 
    [--help] [--framework]  
    [--runtime] [--output]  
    [--version-suffix] [--configuration]`

## <a name="description"></a>Descrizione

`dotnet publish` compila l'applicazione, legge le relative dipendenze specificate nel file di progetto e pubblica il set di file risultante in una directory. 

A seconda del tipo di app portabile, la directory risultante conterrà gli elementi seguenti:

1. *Distribuzione dipendente dal framework*: codice di linguaggio intermedio (IL, Intermediate Language) dell'applicazione e tutte le dipendenze gestite dell'applicazione.
2. *Distribuzione autonoma*: come sopra, con in più l'intero runtime per la piattaforma di destinazione.

Per altre informazioni, vedere l'argomento [Distribuzione di applicazioni .NET Core](../deploying/index.md).

## <a name="options"></a>Opzioni

`[project]` 

Progetto da pubblicare che, se `[project]` non è specificato, per impostazione predefinita sarà la directory corrente. 

`-h|--help`

Stampa una breve guida per il comando.  

`-f|--framework <FRAMEWORK>`

Pubblica l'applicazione per un determinato identificatore del framework (FID, Framework Identifier). 

`-r|--runtime <RUNTIME_IDENTIFIER>`

Pubblica l'applicazione per un determinato runtime. Per un elenco degli identificatori di runtime (RID, Runtime Identifier) che è possibile usare, vedere il [catalogo RID](../../rid-catalog.md).

`-o|--output <OUTPUT_PATH>`

Specificare il percorso in cui inserire la directory. Se non specificato, il percorso predefinito sarà *_./bin/[configurazione]/[framework]/_* per applicazioni portabili o *_./bin/[configurazione]/[framework]/[runtime]_* per distribuzioni autonome.

`--version-suffix [VERSION_SUFFIX]`

Definisce l'elemento che deve sostituire `*` nel campo relativo alla versione del file di progetto.

`-c|--configuration [Debug|Release]`

Configurazione da usare durante la pubblicazione. Il valore predefinito è `Debug`.

## <a name="examples"></a>Esempi

Pubblicare un'applicazione.

`dotnet publish`

Pubblicare l'applicazione usando il file di progetto specificato

`dotnet publish ~/projects/app1/app1.csproj`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.0`:

`dotnet publish --framework netcoreapp1.0`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.0` e il runtime per `OS X 10.10` (questo identificatore di runtime deve esistere nel file di progetto.

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

## <a name="see-also"></a>Vedere anche
* [Framework](../../../standard/frameworks.md)
* [Catalogo RID (Runtime IDentifier)](../../rid-catalog.md)



<!--HONumber=Feb17_HO2-->


