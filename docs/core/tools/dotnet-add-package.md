---
title: Comando dotnet-add package | Microsoft Docs
description: Il comando dotnet-add package offre un&quot;opzione utile per aggiungere il riferimento al pacchetto NuGet in un progetto.
keywords: dotnet-add, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 88e0da69-a5ea-46cc-8b46-5493242b7af9
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 806f4383452cb250f302dc30ab2d59f7e4772026
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-add-package"></a>dotnet-add package

## <a name="name"></a>Nome

`dotnet-add package`: aggiunge il riferimento al pacchetto in un file di progetto.

## <a name="synopsis"></a>Riepilogo

```
dotnet add [project] package <package_name> [-v|--version] [-f|--framework] [-n|--no-restore] [-s|--source] [--package-directory]
dotnet add package [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet add package` offre un'opzione utile per aggiungere i riferimenti al pacchetto in un file di progetto. Dopo l'esecuzione del comando viene eseguito un controllo di compatibilità per verificare che il pacchetto che si tenta di aggiungere sia compatibile con tutti i framework nel progetto. Se il controllo ha esito positivo, viene eseguito [restore](dotnet-restore.md) e viene aggiunto il frammento `<PackageReference>` al file di progetto.

Ad esempio, l'aggiunta di `Newtonsoft.Json` in *ToDo.csproj* produce un output simile al seguente:

```
Microsoft (R) Build Engine version 15.1.545.13942
Copyright (C) Microsoft Corporation. All rights reserved.

  Writing /var/folders/gj/1mgg_4jx7mbdqbhw1kgcpcjr0000gn/T/tmpm0kTMD.tmp
info : Adding PackageReference for package 'Newtonsoft.Json' into project 'ToDo.csproj'.
log  : Restoring packages for ToDo.csproj...
info :   GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/newtonsoft.json/index.json 119ms
info :   GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg 27ms
info : Package 'Newtonsoft.Json' is compatible with all the specified frameworks in project 'ToDo.csproj'.
info : PackageReference for package 'Newtonsoft.Json' version '9.0.1' added to file 'ToDo.csproj'.
```

Il file *ToDo.csproj* contiene ora un frammento [`<PackageReference>`](https://docs.microsoft.com/nuget/consume-packages/package-references-in-project-files) per il pacchetto cui viene fatto riferimento.

```xml
<PackageReference Include="Newtonsoft.Json">
  <Version>9.0.1</Version>
</PackageReference>
```

## <a name="arguments"></a>Argomenti

`project`

File di progetto da usare. Se non specificato, il comando ne cerca uno nella directory corrente.

`package_name`

Riferimento al pacchetto da aggiungere.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-v|--version <VERSION>`

Versione del pacchetto.

`-f|--framework <FRAMEWORK>`

Aggiunge un riferimento al pacchetto solo quando la destinazione è un framework specifico.

`-n|--no-restore`

Aggiunge un riferimento al pacchetto senza eseguire l'anteprima del ripristino e il controllo di compatibilità.

`-s|--source <SOURCE>`

Usa un'origine di pacchetto NuGet specifica da usare durante l'operazione di ripristino.

`--package-directory <PACKAGE_DIRECTORY>`

Ripristina il pacchetto nella directory specificata.

## <a name="examples"></a>Esempi

Aggiungere un pacchetto NuGet `Newtonsoft.Json` in un progetto:

`dotnet add package Newtonsoft.Json`

Aggiungere una versione specifica di un pacchetto in un progetto:

`dotnet add ToDo.csproj package Microsoft.Azure.DocumentDB.Core -v 1.0.0`

Aggiungere un pacchetto usando un'origine NuGet specifica:

`dotnet add package Microsoft.AspNetCore.StaticFiles -s https://dotnet.myget.org/F/dotnet-core/api/v3/index.json`

