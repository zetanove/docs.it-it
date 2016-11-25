---
title: Gestione delle dipendenze negli strumenti dell&quot;anteprima 3 di .NET Core
description: L&quot;anteprima 3 descrive le modifiche relative alla gestione delle dipendenze
keywords: "interfaccia della riga di comando, estendibilità, comandi personalizzati, .NET Core"
author: blackdwarf
manager: wpickett
ms.date: 11/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 74b87cdb-a244-4c13-908c-539118bfeef9
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: e04d5f3b08c7f6885ed9914a91fc308234e6ce3b

---

<a name="managing-dependencies-in-net-core-preview-3-tooling"></a>Gestione delle dipendenze negli strumenti dell'anteprima 3 di .NET Core
----------------------------------------------------

# <a name="overview"></a>Panoramica
Con il passaggio dei progetti .NET Core da project.json a csproj e MSBuild, è stato eseguito un investimento significativo che ha comportato l'unificazione dei file di progetto e degli asset che consentono il monitoraggio delle dipendenze. Per i progetti .NET Core si tratta di un comportamento simile a quello di project.json. Non esiste alcun file JSON o XML separato che tiene traccia delle dipendenze NuGet. Con questa modifica, è stato anche introdotto un altro tipo di *riferimento* nella sintassi csproj denominato `<PackageReference>`. 

Questo documento descrive il nuovo tipo di riferimento. Illustra anche come aggiungere al progetto una dipendenza del pacchetto usando questo nuovo tipo di riferimento. 

# <a name="the-new-packagereference-element"></a>Nuovo elemento <PackageReference>
L'elemento `<PackageReference>` ha la struttura di base seguente:

```xml
<PackageReference Include="<Package_ID>">
    <Version>PACKAGE_VERSION</Version>
</PackageReference>
```

Se si ha familiarità con MSBuild, il nuovo elemento risulterà analogo agli altri [tipi di riferimento]() già esistenti. La chiave è l'istruzione `Include` che specifica l'ID del pacchetto da aggiungere al progetto. L'elemento figlio `<Version>` specifica la versione da ottenere. Le versioni vengono specificate in base alle [regole della versione di NuGet](https://docs.nuget.org/ndocs/create-packages/dependency-versions#version-ranges).  

> **Nota:** se non si ha familiarità con la sintassi `csproj`, è possibile usare la [documentazione di riferimento del progetto MSBuild]().  

Per aggiungere una dipendenza disponibile solo in una destinazione specifica, usare le condizioni:

```xml
<PackageReference Include="<Package_ID>" Condition="'$(TargetFramework)' == 'netcoreapp1.0'">
    <Version>PACKAGE_VERSION</Version>
</PackageReference>
```

Quanto descritto sopra indica che la dipendenza sarà valida solo se la compilazione avviene per una specifica destinazione. `$(TargetFramework)` nella condizione è una proprietà di MSBuild che viene impostata nel progetto. Per le applicazioni .NET Core più comuni, non occorre eseguire questa operazione. 

# <a name="adding-a-dependency-to-your-project"></a>Aggiunta di una dipendenza al progetto
L'aggiunta di una dipendenza al progetto è un'operazione semplice. Di seguito è riportato un esempio che illustra come aggiungere la versione `JSON.net` al progetto `9.0.1`. Naturalmente, è applicabile a qualsiasi altra dipendenza NuGet. 

Quando si apre il file di progetto, verranno visualizzati due o più nodi `<ItemGroup>`. Si noterà che uno dei nodi dispone già degli elementi `<PackageReference>`. È possibile aggiungere la nuova dipendenza a questo nodo o crearne una nuova. La scelta tra queste due opzioni è responsabilità dell'utente, il risultato sarà identico. 

In questo esempio verrà usato il modello predefinito eliminato da `dotnet new`. Si tratta di una semplice applicazione console. Quando si apre il progetto, è possibile visualizzare `<ItemGroup>` con `<PackageReference>` già presente. Vengono quindi aggiunti gli elementi seguenti:

```xml
<PackageReference Include="Newtonsoft.Json">
    <Version>9.0.1</Version>
</PackageReference>
```
Successivamente, salvare il progetto ed eseguire il comando `dotnet restore` per installare la dipendenza. 

Il progetto completo è simile al seguente:

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
  
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <Compile Include="**\*.cs" />
    <EmbeddedResource Include="**\*.resx" />
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NETCore.App">
      <Version>1.0.1</Version>
    </PackageReference>
    <PackageReference Include="Newtonsoft.Json">
        <Version>9.0.1</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161104-2</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
  </ItemGroup>
  
  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

# <a name="removing-a-dependency-from-the-project"></a>Rimozione di una dipendenza dal progetto
La rimozione di una dipendenza dal file di progetto comporta la semplice rimozione di `<PackageReference>` dal file di progetto. 





<!--HONumber=Nov16_HO3-->


