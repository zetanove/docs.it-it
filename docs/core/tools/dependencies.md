---
title: Gestione delle dipendenze negli strumenti di .NET Core | Microsoft Docs
description: Viene illustrato come gestire le dipendenze con gli strumenti di .NET Core.
keywords: "interfaccia della riga di comando, estendibilità, comandi personalizzati, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 74b87cdb-a244-4c13-908c-539118bfeef9
ms.translationtype: Human Translation
ms.sourcegitcommit: 25847dd6921e547074f4501d34d865dfb1b98b59
ms.openlocfilehash: de496d96120df1ec275bb4a69f01b6266b0b5a89
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---

# <a name="managing-dependencies-with-net-core-sdk-10"></a>Gestione delle dipendenze con .NET Core SDK 1.0

Con il passaggio dei progetti .NET Core da project.json a csproj e MSBuild, è stato eseguito un investimento significativo che ha comportato l'unificazione del file di progetto e degli asset che consentono il monitoraggio delle dipendenze. Per i progetti .NET Core si tratta di un comportamento simile a quello di project.json. Non esiste alcun file JSON o XML separato che tiene traccia delle dipendenze NuGet. Con questa modifica, è stato anche introdotto un altro tipo di *riferimento* nella sintassi csproj denominato `<PackageReference>`. 

Questo documento descrive il nuovo tipo di riferimento. Illustra anche come aggiungere al progetto una dipendenza del pacchetto usando questo nuovo tipo di riferimento. 

## <a name="the-new-packagereference-element"></a>Nuovo elemento \<PackageReference>
L'elemento `<PackageReference>` ha la struttura di base seguente:

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" />
```

Se si ha familiarità con MSBuild, il nuovo elemento risulterà analogo agli altri tipi di riferimento già esistenti. La chiave è l'istruzione `Include` che specifica l'ID del pacchetto da aggiungere al progetto. L'elemento figlio `<Version>` specifica la versione da ottenere. Le versioni vengono specificate in base alle [regole della versione di NuGet](https://docs.microsoft.com/nuget/create-packages/dependency-versions#version-ranges).

> [!NOTE]
> Se non si ha familiarità con la sintassi `csproj`, vedere la [documentazione di riferimento del progetto MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-project-file-schema-reference) per altre informazioni.  

Per aggiungere una dipendenza disponibile solo in una destinazione specifica, usare le condizioni come nell'esempio seguente:

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" Condition="'$(TargetFramework)' == 'netcoreapp1.0'" />
```

Quanto descritto sopra indica che la dipendenza sarà valida solo se la compilazione avviene per una specifica destinazione. `$(TargetFramework)` nella condizione è una proprietà di MSBuild che viene impostata nel progetto. Per le applicazioni .NET Core più comuni, non occorre eseguire questa operazione. 

## <a name="adding-a-dependency-to-your-project"></a>Aggiunta di una dipendenza al progetto
L'aggiunta di una dipendenza al progetto è un'operazione semplice. Di seguito è riportato un esempio che illustra come aggiungere Json.NET versione `9.0.1` al progetto. Naturalmente, è applicabile a qualsiasi altra dipendenza NuGet. 

Quando si apre il file di progetto, verranno visualizzati due o più nodi `<ItemGroup>`. Si noterà che uno dei nodi dispone già degli elementi `<PackageReference>`. È possibile aggiungere la nuova dipendenza a questo nodo o crearne una nuova. La scelta tra queste due opzioni è responsabilità dell'utente, il risultato sarà identico. 

In questo esempio verrà usato il modello predefinito eliminato da `dotnet new console`. Si tratta di una semplice applicazione console. Quando si apre il progetto, è possibile visualizzare `<ItemGroup>` con `<PackageReference>` già presente. Vengono quindi aggiunti gli elementi seguenti:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
```
Successivamente, salvare il progetto ed eseguire il comando `dotnet restore` per installare la dipendenza. 

Il progetto completo è simile al seguente:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
</Project>
```

## <a name="removing-a-dependency-from-the-project"></a>Rimozione di una dipendenza dal progetto
La rimozione di una dipendenza dal file di progetto comporta la semplice rimozione di `<PackageReference>` dal file di progetto.

