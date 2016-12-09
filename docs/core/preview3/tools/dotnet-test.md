---
title: Comando dotnet-test | .NET Core SDK
description: Il comando &quot;dotnet test&quot; viene usato per eseguire unit test in un determinato progetto.
keywords: dotnet-test, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 3a0fa917-eb0a-4d7e-9217-d06e65455675
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 66c9f949980612f6e21b6d441c004cc09f4eb7d3

---

#<a name="dotnet-test"></a>dotnet-test

## <a name="name"></a>Nome

`dotnet-test` - Driver di test .NET

## <a name="synopsis"></a>Riepilogo

`dotnet test [project] [--help] 
    [--settings] [--listTests] [--testCaseFilter] 
    [--testAdapterPath] [--logger] 
    [--configuration] [--output] [--framework] [--diag]
    [--noBuild]`  

## <a name="description"></a>Descrizione

Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto. Gli unit test sono progetti della libreria di classi con dipendenze dal framework di unit test (ad esempio, NUnit o xUnit) e dal Test Runner dotnet per tale framework di unit test. Sono disponibili come pacchetti NuGet e vengono ripristinati come dipendenze ordinarie per il progetto.

Anche i progetti di test devono specificare il test runner. Quest'ultimo viene specificato usando un normale elemento `<PackageReference>`, come illustrato nel file di progetto di esempio seguente:

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
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161104-2</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.NET.Test.Sdk">
      <Version>15.0.0-preview-20161024-02</Version>
    </PackageReference>
    <PackageReference Include="xunit">
      <Version>2.2.0-beta3-build3402</Version>
    </PackageReference>
    <PackageReference Include="xunit.runner.visualstudio">
      <Version>2.2.0-beta4-build1188</Version>
    </PackageReference>
  </ItemGroup>

  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

## <a name="options"></a>Opzioni

`[project]`
    
Specifica un percorso del progetto di test. Se omesso, per impostazione predefinita sarà la directory corrente.

`-h|--help`

Stampa una breve guida per il comando.

`-s | --settings <SETTINGS_FILE>`

Impostazioni da usare durante l'esecuzione di test. 

`-lt | --listTests`

Elenca tutti i test individuati nel progetto corrente. 

`-tcf | --testCaseFilter <EXPRESSION>`

Filtra i test nel progetto corrente usando l'espressione specificata. 

`-tap | --testAdapterPath <TEST_ADAPTER_PATH>`

Usa gli adattatori di test personalizzati dal percorso specificato in questa esecuzione di test. 

`--logger <LOGGER>`

Specifica un logger per i risultati di test. 

`-c|--configuration <Debug|Release>`

Configurazione in cui eseguire la compilazione. Il valore predefinito è `Release`. 

`-o|--output [OUTPUT_DIRECTORY]`

Directory in cui trovare i file binari da eseguire.

`-f|--framework [FRAMEWORK]`

Cerca i file binari di test per un framework specifico.

`-r|--runtime [RUNTIME_IDENTIFIER]`

Cerca i file binari di test per il runtime specificato.

`--noBuild` 

Non compila il progetto di test prima di eseguirlo. 

`-d | --diag <DIAGNOSTICS_FILE>`

Abilita la modalità di diagnostica per la piattaforma di test e scrive messaggi di diagnostica nel file specificato. 

## <a name="examples"></a>Esempi

Eseguire i test nel progetto nella directory corrente:

`dotnet test` 

Eseguire i test nel progetto test1:

`dotnet test ~/projects/test1/test1.csproj` 

## <a name="see-also"></a>Vedere anche

[Framework](../../../standard/frameworks.md)

[Catalogo RID (Runtime IDentifier)](../../rid-catalog.md)



<!--HONumber=Nov16_HO3-->


