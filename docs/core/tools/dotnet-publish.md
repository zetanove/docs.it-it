---
title: Comando dotnet-publish | Microsoft Docs
description: Il comando dotnet-publish consente di pubblicare il progetto .NET Core in una directory.
keywords: dotnet-publish, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f2ef275a-7c5e-430a-8c30-65f52af62771
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 78487673d8fa07286605fb806f30083747b17386
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-publish"></a>dotnet-publish

## <a name="name"></a>Nome

`dotnet-publish`: comprime l'applicazione e tutte le relative dipendenze in una cartella, preparandole per la pubblicazione.

## <a name="synopsis"></a>Riepilogo

```
dotnet publish [project] [-f|--framework] [-r|--runtime] [-o|--output] [-c|--configuration] [--version-suffix] [-v|--verbosity]
dotnet publish [-h|--help]
```

## <a name="description"></a>Descrizione

`dotnet publish` compila l'applicazione, legge le relative dipendenze specificate nel file di progetto e pubblica il set di file risultante in una directory. L'output conterrà quanto segue:

1. Codice Intermediate Language (IL) in un assembly con un'estensione `*.dll`.
2. File *deps.json* che contiene tutte le dipendenze del progetto. 
3. File *Runtime.config.json* che specifica il runtime condiviso previsto dall'applicazione e altre opzioni di configurazione per il runtime, ad esempio il tipo di Garbage Collection.
4. Tutte le dipendenze dell'applicazione. Questi dati vengono copiati dalla cache NuGet e nella cartella di output. 

L'output del comando `dotnet publish` è pronto per essere distribuito in un computer remoto per l'esecuzione e costituisce l'unica modalità supportata ufficialmente per preparare l'applicazione per la distribuzione in un altro computer, ad esempio un server, per l'esecuzione. A seconda del tipo di distribuzione specificato dal progetto, è necessario che nel computer remoto sia installato il runtime condiviso di .NET Core. Per altre informazioni, vedere l'argomento [Distribuzione di applicazioni .NET Core](../deploying/index.md).

## <a name="arguments"></a>Argomenti

`project` 

Progetto da pubblicare che, se `project` non è specificato, per impostazione predefinita sarà la directory corrente. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-f|--framework <FRAMEWORK>`

Pubblica l'applicazione per il framework di destinazione specificato. Il framework di destinazione deve essere specificato nel file di progetto.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Pubblica l'applicazione per un determinato runtime. Viene usato durante la creazione di una [distribuzione indipendente](../deploying/index.md#self-contained-deployments-scd). Per un elenco degli identificatori di runtime (RID, Runtime Identifier) che è possibile usare, vedere il [catalogo RID](../rid-catalog.md). L'impostazione predefinita prevede la pubblicazione di un'[app dipendente da framework](../deploying/index.md#framework-dependent-deployments-fdd).

`-o|--output <OUTPUT_PATH>`

Specificare il percorso in cui inserire la directory. Se non specificato, il percorso predefinito sarà *_./bin/[configurazione]/[framework]/_* per applicazioni portabili o *_./bin/[configurazione]/[framework]/[runtime]_* per distribuzioni autonome.

`-c|--configuration {Debug|Release}`

Configurazione da usare durante la compilazione del progetto. Il valore predefinito è `Debug`.

`--version-suffix <VERSION_SUFFIX>`

Definisce l'elemento che deve sostituire `*` nel campo relativo alla versione del file di progetto.

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Pubblicare il progetto trovato nella directory corrente:

`dotnet publish`

Pubblicare l'applicazione usando il file di progetto specificato:

`dotnet publish ~/projects/app1/app1.csproj`
    
Pubblicare il progetto trovato nella directory corrente usando il framework `netcoreapp1.1`:

`dotnet publish --framework netcoreapp1.1`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.1` e il runtime per `OS X 10.10` (questo identificatore di runtime deve esistere nel file di progetto.

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

## <a name="see-also"></a>Vedere anche
* [Framework](../../standard/frameworks.md)
* [Catalogo RID (Runtime IDentifier)](../rid-catalog.md)
