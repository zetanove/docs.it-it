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
ms.assetid: 8a7e1c52-5c57-4bf5-abad-727450ebeefd
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 1cf1611ab83874ad44855521d21040d102206338

---

#<a name="dotnet-publish"></a>dotnet-publish

> [!WARNING]
> Questo argomento si applica agli strumenti dell'anteprima 2 di .NET Core. Per gli strumenti di .NET Core versione RC4, vedere l'argomento [dotnet-publish (strumenti di .NET Core RC4)](../preview3/tools/dotnet-publish.md).

## <a name="name"></a>Nome

`dotnet-publish`: comprime l'applicazione e tutte le relative dipendenze in una cartella, preparandole per la pubblicazione.

## <a name="synopsis"></a>Riepilogo

`dotnet publish [project] 
    [--help] [--framework]  
    [--runtime] [--build-base-path] [--output]  
    [--version-suffix] [--configuration] [--native-subdirectory] [--no-build]`

## <a name="description"></a>Descrizione

`dotnet publish` compila l'applicazione, legge le relative dipendenze specificate nel file [project.json](project-json.md) e pubblica il set di file risultante in una directory. 

A seconda del tipo di app portabile, la directory risultante conterrà gli elementi seguenti:

1. *Applicazione portabile*: codice di linguaggio intermedio (IL, Intermediate Language) dell'applicazione e tutte le dipendenze gestite dell'applicazione.
    * *Applicazione portabile con dipendenze native*: come sopra, con una sottodirectory per la piattaforma supportata di ogni dipendenza nativa. 
2. *Applicazione autonoma*: come sopra, con in più l'intero runtime per la piattaforma di destinazione.

Per altre informazioni, vedere l'argomento [Distribuzione di applicazioni .NET Core](../deploying/index.md).

## <a name="options"></a>Opzioni

`[project]` 

Progetto da pubblicare che, se `[project]` non è specificato, per impostazione predefinita sarà la directory corrente. Questo valore può essere un percorso del file [project.json](project-json.md) o della directory del progetto contenente il file [project.json](project-json.md). Se non è presente un file [project.json](project-json.md), `dotnet publish` genera un errore. 

`-h|--help`

Stampa una breve guida per il comando.  

`-f|--framework <FRAMEWORK>`

Pubblica l'applicazione per un determinato identificatore del framework (FID, Framework Identifier). Se non specificato, l'identificatore del framework viene letto dal file [project.json](project-json.md#frameworks). Se non viene trovato un framework valido, il comando genera un errore. Se vengono trovati più framework validi, il comando esegue la pubblicazione per tutti i framework validi. 

`-r|--runtime <RUNTIME_IDENTIFIER>`

Pubblica l'applicazione per un determinato runtime. Per un elenco degli identificatori di runtime (RID, Runtime Identifier) che è possibile usare, vedere il [catalogo RID](../rid-catalog.md).

`-b|--build-base-path <OUTPUT_DIRECTORY>`

Directory in cui inserire gli output temporanei.

`-o|--output <OUTPUT_PATH>`

Specificare il percorso in cui inserire la directory. Se non specificato, il percorso predefinito sarà *_./bin/[configurazione]/[framework]/_* per applicazioni portabili o *_./bin/[configurazione]/[framework]/[runtime]_* per distribuzioni autonome.

`--version-suffix [VERSION_SUFFIX]`

Definisce l'elemento che deve sostituire `*` nel campo relativo alla versione del file project.json.

`-c|--configuration [Debug|Release]`

Configurazione da usare durante la pubblicazione. Il valore predefinito è `Debug`.

`[--native-subdirectory]` Meccanismo temporaneo per includere le sottodirectory da risorse native dei pacchetti con dipendenze nell'output. 

`[--no-build]` Non compila i progetti prima della pubblicazione.

## <a name="examples"></a>Esempi

Pubblicare un'applicazione usando il framework presente in `project.json`. Se `project.json` contiene il nodo [runtimes](project-json.md#runtimes), eseguire la pubblicazione per l'identificatore di runtime della piattaforma corrente.

`dotnet publish`

Pubblicare l'applicazione usando il file [project.json](project-json.md) specificato:

`dotnet publish ~/projects/app1/project.json`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.0`:

`dotnet publish --framework netcoreapp1.0`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.0` e il runtime per `OS X 10.10` (questo identificatore di runtime deve esistere nel nodo [runtimes](project-json.md#runtimes) del file `project.json`):

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

## <a name="see-also"></a>Vedere anche
* [Framework](../../standard/frameworks.md)
* [Catalogo RID (Runtime IDentifier)](../rid-catalog.md)


<!--HONumber=Feb17_HO2-->


