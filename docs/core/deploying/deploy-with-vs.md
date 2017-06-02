---
title: Distribuzione di app .NET Core con Visual Studio | Microsoft Docs
description: Informazioni sulla distribuzione di app .NET Core con Visual Studio
keywords: .NET, .NET Core, distribuzione di .NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 04/18/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 01049a21-fd50-4419-9ab2-0e4a2e091050
ms.translationtype: Human Translation
ms.sourcegitcommit: 3ffe3909902659a22cb25bac6dc5aaa4f5b9fde2
ms.openlocfilehash: c6fe1813f0d09207c6730fc5dce682647e25eb03
ms.contentlocale: it-it
ms.lasthandoff: 05/13/2017

---

# <a name="deploying-net-core-apps-with-visual-studio"></a>Distribuzione di app .NET Core con Visual Studio

È possibile distribuire un'app .NET Core come *distribuzione dipendente dal framework*, che include i file binari dell'applicazione ma dipende dalla presenza di .NET Core nel sistema di destinazione oppure come *distribuzione autonoma*, che include l'applicazione e i file binari di .NET Core. Per una panoramica della distribuzione di applicazioni .NET Core, vedere [Distribuzione di applicazioni .NET Core](index.md).

Le sezioni seguenti illustrano l'uso di Microsoft Visual Studio per creare i tipi di distribuzione seguenti:

- Distribuzione dipendente dal framework
- Distribuzione dipendente dal framework con dipendenze di terze parti
- Distribuzione autonoma
- Distribuzione autonoma con dipendenze di terze parti

Per informazioni sull'uso di Visual Studio per sviluppare applicazioni .NET Core, vedere [Prerequisiti per .NET Core in Windows](../windows-prerequisites.md#prerequisites-with-visual-studio-2017).

## <a name="framework-dependent-deployment"></a>Distribuzione dipendente dal framework

Una distribuzione dipendente dal framework senza dipendenze di terze parti richiede la compilazione, il testing e la pubblicazione dell'app. Il processo viene illustrato da un semplice esempio scritto in C#.  

1. Creare il progetto.

   Selezionare **File** > **Nuovo** > **Progetto**. Nella finestra di dialogo **Nuovo progetto** selezionare **.NET Core** nel riquadro dei tipi di progetto **Installati**, quindi selezionare il modello **Console App (.NET Core)** (App console (.NET Core)) nel riquadro al centro. Immettere un nome di progetto, ad esempio "FDD", nella casella di testo **Nome**. Selezionare il pulsante **OK** .

1. Aggiungere il codice sorgente dell'applicazione.

   Aprire il file *Program.cs* nell'editor e sostituire il codice generato automaticamente con il codice seguente. Questo codice richiede all'utente di immettere del testo e visualizza le singole parole immesse dall'utente. Usa l'espressione regolare `\w+` per separare le parole nel testo di input.

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. Creare una build di debug dell'app.

   Selezionare **Compila** > **Compila soluzione**. È anche possibile compilare ed eseguire la build di debug dell'applicazione selezionando **Esegui debug** > **Avvia debug**.

1. Distribuire l'app.

   Dopo aver eseguito il debug e il test del programma, creare i file da distribuire con l'app. Per la pubblicazione da Visual Studio eseguire le operazioni seguenti:

      1. Modificare la configurazione della soluzione da **Debug** a **Release** sulla barra degli strumenti, per creare una versione di rilascio dell'app (invece di una versione di debug).

      1. Fare clic con il pulsante destro del mouse sul progetto (non sulla soluzione) in **Solution Explorer** e selezionare **Pubblica**.

      1. Nella scheda **Pubblica** selezionare **Pubblica**. I file che costituiscono l'applicazione vengono salvati nel file system locale.

      1. La scheda **Pubblica** ora visualizza un unico profilo **FolderProfile**. Le impostazioni di configurazione del profilo vengono visualizzate nella sezione **Riepilogo** della scheda.

   I file risultanti vengono inseriti nella directory `PublishOutput` in una sottodirectory della directory *.\bin\release* del progetto.

Insieme ai file dell'applicazione, il processo di pubblicazione genera un file del database di programma (con estensione pdb) che contiene le informazioni di debug relative all'app. Il file è utile soprattutto per il debug delle eccezioni. È possibile scegliere di non includerlo nel pacchetto dei file dell'applicazione. È tuttavia consigliabile salvarlo perché può risultare utile per il debug della build di rilascio dell'app.

Distribuire il set completo dei file dell'applicazione con il metodo desiderato. È ad esempio possibile inserire i file in un file zip, usare un semplice comando `copy` o distribuire i file con un pacchetto di installazione a scelta. Dopo aver completato l'installazione gli utenti possono eseguire l'applicazione usando il comando `dotnet` e fornendo il nome file dell'applicazione, ad esempio `dotnet fdd.dll`.

Oltre ai file binari dell'applicazione, il programma di installazione deve aggregare il programma di installazione framework condiviso oppure rilevarlo come prerequisito durante l'installazione dell'applicazione.  L'installazione del framework condiviso richiede l'accesso amministratore o alla radice perché è a livello di computer.

## <a name="framework-dependent-deployment-with-third-party-dependencies"></a>Distribuzione dipendente dal framework con dipendenze di terze parti

In una distribuzione dipendente dal framework con una o più dipendenze di terze parti, le dipendenze devono essere disponibili per il progetto. Prima della compilazione dell'app è necessario eseguire i passaggi aggiuntivi:

1. Usare **Gestione pacchetti NuGet** per aggiungere al progetto un riferimento a un pacchetto NuGet e per installare il pacchetto se non è già disponibile nel sistema. Per aprire lo strumento per la gestione dei pacchetti, selezionare **Strumenti** > **Gestione pacchetti NuGet** > **Gestisci pacchetti NuGet per la soluzione**.

1. Verificare che `Newtonsoft.Json` sia installato nel sistema e, in caso contrario, installarlo. La scheda **Installati** elenca i pacchetti NuGet installati nel sistema. Se `Newtonsoft.Json` non è presente nell'elenco, selezionare la scheda **Sfoglia** e immettere "Newtonsoft.Json" nella casella di ricerca. Selezionare `Newtonsoft.Json`, selezionare il progetto nel riquadro destro e quindi selezionare **Installa**.

1. Se `Newtonsoft.Json` è già installato nel sistema, aggiungerlo al progetto selezionando il progetto nel riquadro destro della scheda **Gestisci i pacchetti per la soluzione**.

Si noti che la portabilità di una distribuzione dipendente dal framework con dipendenze di terze parti corrisponde esattamente alla portabilità delle dipendenze. Se ad esempio una libreria di terze parti supporta solo macOS, l'app non è portabile in sistemi Windows. Questa situazione si verifica se la dipendenza di terze parti stessa dipende da codice nativo. Un buon esempio è il [server Kestrel](http://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel), che richiede una dipendenza nativa da [libuv](https://github.com/libuv/libuv). Quando viene creata una distribuzione dipendente dal framework per un'applicazione con questo tipo di dipendenze di terze parti, l'output pubblicato contiene una cartella per ogni [identificatore di runtime (RID)](../rid-catalog.md#what-are-rids) supportato dalla dipendenza nativa (e presente nel relativo pacchetto NuGet).

## <a name="simpleSelf"></a> Distribuzione autonoma senza dipendenze di terze parti

La pubblicazione di una distribuzione autonoma senza dipendenze di terze parti comporta la creazione del progetto, la modifica del file *csproj*, la compilazione, il test e la pubblicazione dell'app. Il processo viene illustrato da un semplice esempio scritto in C#. 

1. Creare il progetto.

   Selezionare **File** > **Nuovo** > **Progetto**. Nella finestra di dialogo **Aggiungi nuovo progetto** selezionare **.NET Core** nel riquadro dei tipi di progetto **Installati**, quindi selezionare il modello **Console App (.NET Core)** (App console (.NET Core)) nel riquadro al centro. Immettere un nome di progetto, ad esempio "SCD" nella casella di testo **Nome**, quindi selezionare il pulsante **OK**.

1. Aggiungere il codice sorgente dell'applicazione.

   Aprire il file *Program.cs* nell'editor e sostituire il codice generato automaticamente con il codice seguente. Questo codice richiede all'utente di immettere del testo e visualizza le singole parole immesse dall'utente. Usa l'espressione regolare `\w+` per separare le parole nel testo di input.

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. Definire le piattaforme di destinazione per l'app.

   1. Fare clic con il pulsante destro del mouse sul progetto (non sulla soluzione) in **Solution Explorer** e selezionare **Modifica SCD.csproj**.

   1. Creare un tag `<RuntimeIdentifiers>` nella sezione `<PropertyGroup>` del file *csproj* che definisce le piattaforme di destinazione dell'app e specifica l'identificatore di runtime di ogni piattaforma di destinazione. Si noti che è inoltre necessario aggiungere un punto e virgola per separare i RID. Per un elenco degli identificatori di runtime, vedere [Runtime IDentifier catalog](../rid-catalog.md) (Catalogo degli identificatori di runtime). 

   L'esempio seguente indica che l'app viene eseguita in sistemi operativi Windows 10 a 64 bit e nel sistema operativo OS X versione 10.11 a 64 bit.

```xml
<PropertyGroup>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
</PropertyGroup>
```
   Si noti che l'elemento `<RuntimeIdentifiers>` può essere inserito in qualsiasi elemento `<PropertyGroup>` presente nel file *csproj*. Un file di esempio *csproj* completo è disponibile più avanti in questa sezione.

1. Creare una build di debug dell'app.

   Selezionare **Compila** > **Compila soluzione**. È anche possibile compilare ed eseguire la build di debug dell'applicazione selezionando **Esegui debug** > **Avvia debug**.

1. Pubblicare l'app.

   Dopo aver eseguito il debug e il test del programma creare i file da distribuire con l'app per ogni piattaforma di destinazione.

   Per pubblicare l'app da Visual Studio eseguire le operazioni seguenti:

      1. Modificare la configurazione della soluzione da **Debug** a **Release** sulla barra degli strumenti, per creare una versione di rilascio dell'app (invece di una versione di debug).

      1. Fare clic con il pulsante destro del mouse sul progetto (non sulla soluzione) in **Esplora soluzioni** e selezionare **Pubblica**. 

      1. Nella scheda **Pubblica** selezionare **Pubblica**. I file che costituiscono l'applicazione vengono salvati nel file system locale.

      1. La scheda **Pubblica** ora visualizza un unico profilo **FolderProfile**. Le impostazioni di configurazione del profilo vengono visualizzate nella sezione **Riepilogo** della scheda. **Runtime di destinazione** identifica il runtime pubblicato e **Percorso di destinazione** identifica il percorso in cui sono stati salvati i file per la distribuzione autonoma.

      1. Per impostazione predefinita tutti i file pubblicati vengono salvati in una singola directory. Per praticità è consigliabile creare un profilo separato per ogni runtime di destinazione e inserire i file pubblicati in una directory specifica per la piattaforma. Questo richiede la creazione di un profilo di pubblicazione separato per ogni piattaforma di destinazione. A questo punto ricompilare l'applicazione per ogni piattaforma procedendo nel modo seguente:

         1. Selezionare **Crea nuovo profilo** nella finestra di dialogo **Pubblica**.

         1. Nella finestra di dialogo **Selezionare una destinazione di pubblicazione**, in **Scegliere una cartella** impostare il percorso su *bin\Release\PublishOutput\win10-x64*. Scegliere **OK**.

         1. Selezionare il nuovo profilo (**FolderProfile1**) nell'elenco dei profili e assicurarsi che **Runtime di destinazione** sia `win10-x64`. In caso contrario, selezionare **Impostazioni**. Nella finestra di dialogo **Impostazioni profilo** impostare **Runtime di destinazione** su `win10-x64` e selezionare **Salva**. In alternativa selezionare **Annulla**.

         1. Selezionare **Pubblica** per pubblicare l'app per le piattaforme Windows 10 a 64 bit.

         1. Eseguire nuovamente la procedura per creare un profilo per la piattaforma `osx.10.11-x64`. Il valore di **Percorso di destinazione** deve essere *bin\Release\PublishOutput\osx.10.11-x64* e **Runtime di destinazione** deve essere `osx.10.11-x64`. Il nome assegnato a questo profilo in Visual Studio è **FolderProfile2**.

      Si noti che ogni percorso di destinazione contiene il set completo di file (i file dell'app e tutti i file di .NET Core) necessari per l'avvio dell'app.

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

Una distribuzione autonoma con una o più dipendenze di terze parti comporta l'aggiunta delle dipendenze. Prima della compilazione dell'app è necessario eseguire i passaggi aggiuntivi:

1. Usare **Gestione pacchetti NuGet** per aggiungere al progetto un riferimento a un pacchetto NuGet e per installare il pacchetto se non è già disponibile nel sistema. Per aprire lo strumento per la gestione dei pacchetti, selezionare **Strumenti** > **Gestione pacchetti NuGet** > **Gestisci pacchetti NuGet per la soluzione**.

1. Verificare che `Newtonsoft.Json` sia installato nel sistema e, in caso contrario, installarlo. La scheda **Installati** elenca i pacchetti NuGet installati nel sistema. Se `Newtonsoft.Json` non è presente nell'elenco, selezionare la scheda **Sfoglia** e immettere "Newtonsoft.Json" nella casella di ricerca. Selezionare `Newtonsoft.Json`, selezionare il progetto nel riquadro destro e quindi selezionare **Installa**.

1. Se `Newtonsoft.Json` è già installato nel sistema aggiungerlo al progetto selezionando il progetto stesso nel riquadro destro della scheda **Gestisci i pacchetti per la soluzione**.

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

Si noti che è possibile distribuire una distribuzione autonoma solo con una libreria di terze parti alle piattaforme supportate da tale libreria. Il caso è simile alla presenza di dipendenze di terze parti con dipendenze native in una distribuzione dipendente dal framework: le dipendenze native esistono nella piattaforma di destinazione solo se sono state installate in precedenza in tale piattaforma.

# <a name="see-also"></a>Vedere anche
[Distribuzione di applicazioni .NET Core](index.md)   
[Catalogo dei RID (Runtime IDentifier) di .NET Core](../rid-catalog.md)   

