---
title: Distribuzione di app .NET Core con strumenti CLI | Microsoft Docs
description: Informazioni sulla distribuzione di app .NET Core con strumenti dell&quot;interfaccia della riga di comando (CLI)
keywords: .NET, .NET Core, distribuzione di .NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 04/18/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 82ebe16d-5e1c-46cc-91e8-71974296429c
ms.translationtype: Human Translation
ms.sourcegitcommit: 3ffe3909902659a22cb25bac6dc5aaa4f5b9fde2
ms.openlocfilehash: e3736d44c05e8740451ff72b28cd01c384ecd34d
ms.contentlocale: it-it
ms.lasthandoff: 05/13/2017

---

# <a name="deploying-net-core-apps-with-command-line-interface-cli-tools"></a>Distribuire app .NET Core con strumenti dell'interfaccia della riga di comando (CLI)

È possibile distribuire un'app .NET Core come *distribuzione dipendente dal framework*, che include i file binari dell'applicazione ma dipende dalla presenza di .NET Core nel sistema di destinazione, oppure come *distribuzione autonoma*, che include l'applicazione e i file binari di .NET Core. Per una panoramica, vedere [Distribuzione di applicazioni .NET Core](index.md).

Le sezioni seguenti illustrano come usare gli [strumenti dell'interfaccia della riga di comando .NET Core](../tools/index.md) per creare i tipi di distribuzione seguenti:

- Distribuzione dipendente dal framework
- Distribuzione dipendente dal framework con dipendenze di terze parti
- Distribuzione autonoma
- Distribuzione autonoma con dipendenze di terze parti

Con la riga di comando è possibile usare l'editor di codice desiderato. Se l'editor di codice è [Visual Studio Code](https://code.visualstudio.com) è possibile aprire una console dei comandi all'interno dell'ambiente di Visual Studio Code selezionando **Visualizza** > **Terminale integrato**.

## <a name="framework-dependent-deployment"></a>Distribuzione dipendente dal framework

Una distribuzione dipendente dal framework senza dipendenze di terze parti richiede la compilazione, il testing e la pubblicazione dell'app. Il processo viene illustrato da un semplice esempio scritto in C#. 

1. Creare una directory del progetto.

   Creare una directory per il progetto e impostarla come directory corrente.

1. Creare il progetto.

   Nella riga di comando digitare [dotnet new console](../tools/dotnet-new.md) per creare un nuovo progetto console C# in tale directory.

1. Aggiungere il codice sorgente dell'applicazione.

   Aprire il file *Program.cs* nell'editor e sostituire il codice generato automaticamente con il codice seguente. Questo codice richiede all'utente di immettere del testo e visualizza le singole parole immesse dall'utente. Usa l'espressione regolare `\w+` per separare le parole nel testo di input.

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. Aggiornare le dipendenze e gli strumenti del progetto.
 
   Eseguire il comando [dotnet-restore](../tools/dotnet-restore.md) per ripristinare le dipendenze specificate nel progetto.

1. Creare una build di debug dell'app.

   Usare il comando [dotnet build](../tools/dotnet-build.md) per compilare l'applicazione o il comando [dotnet run](../tools/dotnet-run.md) per compilarla ed eseguirla.

1. Distribuire l'app.

   Dopo il debug e il test del programma, creare la distribuzione mediante il comando seguente:

      ```console
      dotnet publish -f netcoreapp1.1 -c Release
      ```
   In questo modo viene creata una versione di rilascio dell'app anziché una versione di debug. I file risultanti vengono inseriti in una directory *publish* in una sottodirectory della directory *bin* del progetto.

Insieme ai file dell'applicazione, il processo di pubblicazione genera un file del database di programma (con estensione pdb) che contiene le informazioni di debug relative all'app. Il file è utile soprattutto per il debug delle eccezioni. È possibile scegliere di non distribuirlo con i file dell'applicazione. È tuttavia consigliabile salvarlo perché può risultare utile per il debug della build di rilascio dell'app.

È possibile distribuire il set completo dei file dell'applicazione con il metodo desiderato. È ad esempio possibile inserire i file in un file zip, usare un semplice comando `copy` o distribuire i file con un pacchetto di installazione a scelta. Dopo aver completato l'installazione gli utenti possono eseguire l'applicazione usando il comando `dotnet` e fornendo il nome file dell'applicazione, ad esempio `dotnet fdd.dll`.

Oltre ai file binari dell'applicazione, il programma di installazione deve aggregare il programma di installazione framework condiviso oppure rilevarlo come prerequisito durante l'installazione dell'applicazione.  L'installazione del framework condiviso richiede l'accesso amministratore o alla radice.

## <a name="framework-dependent-deployment-with-third-party-dependencies"></a>Distribuzione dipendente dal framework con dipendenze di terze parti

In una distribuzione dipendente dal framework con una o più dipendenze di terze parti, tali dipendenze devono essere disponibili per il progetto. Prima dell'esecuzione del comando `dotnet restore` è necessario eseguire due passaggi aggiuntivi:

1. Aggiungere riferimenti alle librerie di terze parti necessarie nella sezione `<ItemGroup>` del file *csproj*. La sezione `<ItemGroup>` seguente contiene una dipendenza da [Json.NET](http://www.newtonsoft.com/json) come libreria di terze parti:

      ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
      </ItemGroup>
      ```

1. Se non lo si è già fatto, scaricare il pacchetto NuGet contenente la dipendenza di terze parti. Per scaricare il pacchetto, eseguire il comando `dotnet restore` dopo l'aggiunta della dipendenza. Poiché la dipendenza viene risolta dalla cache NuGet locale in fase di pubblicazione, deve essere disponibile nel sistema.

Si noti che la portabilità di una distribuzione dipendente dal framework con dipendenze di terze parti corrisponde esattamente alla portabilità delle dipendenze. Se ad esempio una libreria di terze parti supporta solo macOS, l'app non è portabile in sistemi Windows. Questa situazione si verifica se la dipendenza di terze parti stessa dipende da codice nativo. Un buon esempio è il [server Kestrel](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel), che richiede una dipendenza nativa da [libuv](https://github.com/libuv/libuv). Quando viene creata una distribuzione dipendente dal framework per un'applicazione con questo tipo di dipendenze di terze parti, l'output pubblicato contiene una cartella per ogni [identificatore di runtime (RID)](../rid-catalog.md#what-are-rids) supportato dalla dipendenza nativa (e presente nel relativo pacchetto NuGet).

## <a name="simpleSelf"></a> Distribuzione autonoma senza dipendenze di terze parti

Una distribuzione autonoma senza dipendenze di terze parti comporta la creazione del progetto, la modifica del file *csproj*, la compilazione, il test e la pubblicazione dell'app. Il processo viene illustrato da un semplice esempio scritto in C#. L'esempio seguente visualizza come creare una distribuzione autonoma con l'[utilità dotnet](../tools/dotnet.md) dalla riga di comando.

1. Creare una directory per il progetto.

   Creare una directory per il progetto e impostarla come directory corrente.

1. Creare il progetto.

   Nella riga di comando digitare [dotnet new console](../tools/dotnet-new.md) per creare un nuovo progetto console C# in tale directory.

1. Aggiungere il codice sorgente dell'applicazione.

   Aprire il file *Program.cs* nell'editor e sostituire il codice generato automaticamente con il codice seguente. Questo codice richiede all'utente di immettere del testo e visualizza le singole parole immesse dall'utente. Usa l'espressione regolare `\w+` per separare le parole nel testo di input.

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. Definire le piattaforme di destinazione per l'app.

   Creare un tag `<RuntimeIdentifiers>` nella sezione `<PropertyGroup>` del file *csproj* che definisce le piattaforme di destinazione dell'app e specificare l'identificatore di runtime di ogni piattaforma di destinazione. Si noti che è inoltre necessario aggiungere un punto e virgola per separare i RID. Per un elenco degli identificatori di runtime, vedere [Runtime IDentifier catalog](../rid-catalog.md) (Catalogo degli identificatori di runtime). 

   Ad esempio, la sezione `<PropertyGroup>` seguente indica che l'app viene eseguita in sistemi operativi Windows 10 a 64 bit e nel sistema operativo OS X versione 10.11 a 64 bit.

     ```xml
     <PropertyGroup>
         <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
     </PropertyGroup>
     ```

   Si noti che l'elemento `<RuntimeIdentifiers>` può essere visualizzato in qualsiasi `<PropertyGroup>` nel file *csproj*. Un file di esempio *csproj* completo è disponibile più avanti in questa sezione.

1. Aggiornare le dipendenze e gli strumenti del progetto.

   Eseguire il comando [dotnet-restore](../tools/dotnet-restore.md) per ripristinare le dipendenze specificate nel progetto.

1. Creare una build di debug dell'app.

   Dalla riga di comando usare il comando [dotnet build](../tools/dotnet-build.md).

1. Dopo aver eseguito il debug e il test del programma creare i file da distribuire con l'app per ogni piattaforma di destinazione.

   Usare il comando `dotnet publish` per entrambe le piattaforme di destinazione come indicato di seguito:

      ```console
      dotnet publish -c Release -r win10-x64
      dotnet publish -c Release -r osx.10.11-x64
      ```

   In questo modo, viene creata una versione di rilascio dell'app per ogni piattaforma di destinazione anziché una versione di debug. I file risultanti vengono inseriti in una directory *publish* in una sottodirectory della directory *.\bin\Release\netcoreapp1.1\<runtime_identifier>* del progetto. Si noti che ogni sottodirectory contiene il set completo di file (i file dell'app e tutti i file di .NET Core) necessario per avviare l'app.

Insieme ai file dell'applicazione, il processo di pubblicazione genera un file del database di programma (con estensione pdb) che contiene le informazioni di debug relative all'app. Il file è utile soprattutto per il debug delle eccezioni. È possibile scegliere di non includerlo nel pacchetto dei file dell'applicazione. È tuttavia consigliabile salvarlo perché può risultare utile per il debug della build di rilascio dell'app.

Distribuire i file pubblicati con il metodo desiderato. È ad esempio possibile inserire i file in un file zip, usare un semplice comando `copy` o distribuire i file con un pacchetto di installazione a scelta.

Di seguito è riportato il file *csproj* completo per questo progetto.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
</Project>
```

## <a name="self-contained-deployment-with-third-party-dependencies"></a>Distribuzione autonoma con dipendenze di terze parti

Una distribuzione autonoma con una o più dipendenze di terze parti comporta l'aggiunta delle dipendenze. Prima dell'esecuzione del comando `dotnet restore` è necessario eseguire due passaggi aggiuntivi:

1. Aggiungere i riferimenti alle eventuali librerie di terze parti alla sezione `<ItemGroup>` del file *csproj*. La sezione `<ItemGroup>` seguente usa Json.NET come libreria di terze parti.

    ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
      </ItemGroup>
    ```

1. Se non lo si è già fatto, scaricare nel sistema il pacchetto NuGet contenente la dipendenza di terze parti. Per rendere la dipendenza disponibile per l'app, eseguire il comando `dotnet restore` dopo l'aggiunta della dipendenza. Poiché la dipendenza viene risolta dalla cache NuGet locale in fase di pubblicazione, deve essere disponibile nel sistema.

Di seguito è riportato il file *csproj* completo per questo progetto:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
  </ItemGroup>
</Project>
```

Quando si distribuisce l'applicazione, anche le dipendenze di terze parti usate nell'app sono contenute nei file dell'applicazione. Non è necessario che le librerie di terze parti siano già presenti nel sistema in cui viene eseguita l'app.

Si noti che è possibile distribuire una distribuzione autonoma solo con una libreria di terze parti alle piattaforme supportate da tale libreria. Il caso è simile alla presenza di dipendenze di terze parti con dipendenze native in una distribuzione dipendente dal framework, nella quale le dipendenze native devono essere compatibili con la piattaforma in cui viene distribuita l'app.

# <a name="see-also"></a>Vedere anche

[Distribuzione di applicazioni .NET Core](index.md)   
[Catalogo dei RID (Runtime IDentifier) di .NET Core](../rid-catalog.md)   

