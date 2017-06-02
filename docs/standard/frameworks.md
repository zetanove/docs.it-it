---
title: Framework di destinazione | Microsoft Docs
description: Informazioni riguardanti i framework di destinazione per le applicazioni e le librerie .NET Core.
keywords: .NET, .NET Core, framework, TFM
author: richlander
ms.author: mairaw
ms.date: 04/27/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6ef56a2e-593d-497b-925a-1e25bb6df2e6
ms.translationtype: Machine Translation
ms.sourcegitcommit: 45835eb80642253f80ea630ae9db1ac766b72b9c
ms.openlocfilehash: 11c1f11e4f8354b7573d03e680cf4a8a16fa26d9
ms.contentlocale: it-it
ms.lasthandoff: 05/11/2017

---

# <a name="target-frameworks"></a>Framework di destinazione

I *framework* definiscono gli oggetti, i metodi e gli strumenti utilizzabili per creare app e librerie. .NET Framework viene usato per creare app e librerie principalmente per l'esecuzione nei sistemi che eseguono un sistema operativo Windows. .NET Core include un framework che consente di compilare app e librerie eseguibili su una vasta gamma di sistemi operativi.

I termini *framework* e *piattaforma* talvolta possono generare confusione a seconda di come sono usati all'interno delle frasi. Nella sua interpretazione peggiore, il termine *piattaforma* ha significati diversi in contesti diversi. Ad esempio, ".NET Core" verrà descritto come "framework .NET Core" nel contesto della compilazione di app e librerie, ma potrà anche essere definito "piattaforma .NET Core" nell'ambito dell'esecuzione del codice di app e librerie. Una *piattaforma di elaborazione* descrive *dove e come* viene eseguita un'applicazione. Dal momento che .NET Core esegue il codice con [.NET Core Common Language Runtime (CoreCLR)](https://github.com/dotnet/coreclr), è anche una piattaforma. Lo stesso vale per .NET Framework, che usa [Common Language Runtime (CLR)](clr.md) per eseguire il codice di app e librerie che è stato sviluppato con oggetti framework, metodi e strumenti di .NET Framework. Nella documentazione si usa spesso il termine "multipiattaforma", che significa essenzialmente "comune a più sistemi operativi e a più architetture (x86, x64, arm)", che è quello che l'autore intende effettivamente.

Gli oggetti e i metodi dei framework sono chiamati Application Programming Interface (API). Le API dei framework sono usate in [Visual Studio](https://www.visualstudio.com/), [Visual Studio per Mac](https://www.visualstudio.com/vs/visual-studio-mac/), [Visual Studio Code](https://code.visualstudio.com/) e altri editor e ambienti di sviluppo integrato (IDE, Integrated Development Environment) per fornire il set corretto di oggetti e metodi per lo sviluppo. I framework vengono anche usati da [NuGet](https://www.nuget.org/) per la produzione e l'uso di pacchetti NuGet, in modo da garantire la creazione e l'uso di pacchetti appropriati per i framework definiti come destinazione all'interno dell'app o della libreria.

Quando si *definisce come destinazione uno o più framework*, sono già stati decisi i set di API e le versioni di tali API da usare. È possibile fare riferimento ai framework in diversi modi: per nome del prodotto, per nome del framework in formato esteso o breve e per famiglia.

## <a name="referring-to-frameworks"></a>Riferimento ai framework

Esistono diversi modi per fare riferimento ai framework, la maggior parte dei quali viene usata all'interno della documentazione di .NET Core. Prendendo .NET Framework 4.6.2 come esempio, vengono usati i formati seguenti:

**Riferimento a un prodotto**

È possibile fare riferimento a una piattaforma .NET o runtime. Entrambi sono ugualmente validi.

* .NET Framework 4.6.2
* .NET 4.6.2

**Riferimento a un framework**

È possibile fare riferimento a un framework o alla destinazione di un framework tramite forme brevi o lunghe del TFM. Entrambi sono ugualmente validi.

* `.NETFramework,Version=4.6.2`
* `net462`

**Riferimento a una famiglia di framework**

È possibile fare riferimento a una famiglia di framework tramite forme brevi o lunghe dell'ID del framework. Entrambi sono ugualmente validi.

* `.NETFramework`
* `net`

## <a name="latest-framework-versions"></a>Versioni più recenti dei framework

La tabella seguente definisce il set di framework che è possibile usare, come si creano i relativi riferimenti e quale versione della [libreria .NET Standard](library.md) viene implementata. Queste versioni di framework sono le versioni stabili più recenti. Non sono visualizzate le versioni non definitive.

| Framework             | Ultima versione | Moniker della versione di .NET Framework di destinazione (TFM, Target Framework Moniker) | Moniker compatto della versione di .NET Framework di destinazione (TFM, Target Framework Moniker) | Versione standard di .NET | Metapackage |
| :-------------------: | :------------: | :----------------------------: | :------------------------------------: | :-------------------: | :---------: |
| .NET Standard         | 1.6.1          | .NET Standard, versione=1.6       | netstandard1.6                         | N/D                   | [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) |
| Applicazione .NET Core | 1.1.1          | .NETCoreApp, versione=1.1        | netcoreapp1.1                          | 1.6                   | [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App) |
| .NET Framework        | 4.6.2          | .NETFramework, versione=4.6.2    | net462                                 | 1,5                   | N/D |

## <a name="supported-frameworks"></a>Framework supportati

In genere si fa riferimento a un framework tramite un breve moniker del framework di destinazione o *TFM* (Target Framework Moniker). In .NET Standard questo viene inoltre generalizzato in *TxM* per consentire un unico riferimento a più framework. I client NuGet supportano i framework seguenti. Gli equivalenti sono visualizzati tra parentesi quadre (`[]`).

| Nome                       | Abbreviazione | TFM/TxM                                    |
| -------------------------- | ------------ | -------------------------------------------- |
| .NET Standard              | netstandard  | netstandard1.0                               |
|                            |              | netstandard1.1                               |
|                            |              | netstandard1.2                               |
|                            |              | netstandard1.3                               |
|                            |              | netstandard1.4                               |
|                            |              | netstandard1.5                               |
|                            |              | netstandard1.6                               |
| .NET Core                  | netcoreapp   | netcoreapp1.0                                |
|                            |              | netcoreapp1.1                                |
| .NET Framework             | net          | net11                                        |
|                            |              | net20                                        |
|                            |              | net35                                        |
|                            |              | net40                                        |
|                            |              | net403                                       |
|                            |              | net45                                        |
|                            |              | net451                                       |
|                            |              | net452                                       |
|                            |              | net46                                        |
|                            |              | net461                                       |
|                            |              | net462                                       |
| Windows Store              | netcore      | netcore [netcore45]                          |
|                            |              | netcore45 [win, win8]                        |
|                            |              | netcore451 [win81]                           |
| .NET Micro Framework       | netmf        | netmf                                        |
| Silverlight                | sl           | sl4                                          |
|                            |              | sl5                                          |
| Windows Phone              | wp           | wp [wp7]                                     |
|                            |              | wp7                                          |
|                            |              | wp75                                         |
|                            |              | wp8                                          |
|                            |              | wp81                                         |
|                            |              | wpa81                                        |
| Piattaforma UWP (Universal Windows Platform) | uap          | uap [uap10.0]                                |
|                            |              | uap10.0 [win10] [netcore50]                  |

## <a name="deprecated-frameworks"></a>Framework deprecati

I framework seguenti sono deprecati. I pacchetti che hanno come destinazione questi framework devono essere migrati alle sostituzioni indicate.

| Framework deprecato | Sostituzione |
| -------------------- | ----------- |
| aspnet50             | netcoreapp  |
| aspnetcore50         |             |
| dnxcore50            |             |
| dnx                  |             |
| dnx45                |             |
| dnx451               |             |
| dnx452               |             |
| dotnet               | netstandard |
| dotnet50             |             |
| dotnet51             |             |
| dotnet52             |             |
| dotnet53             |             |
| dotnet54             |             |
| dotnet55             |             |
| dotnet56             |             |
| netcore50            | uap10.0     |
| win                  | netcore45   |
| win8                 | netcore45   |
| win81                | netcore451  |
| win10                | uap10.0     |
| winrt                | netcore45   |

## <a name="precedence"></a>Precedenza

Alcuni framework sono correlati e compatibili tra loro, ma non necessariamente equivalenti:

| Framework                        | È possibile usare:   |
| -------------------------------- | --------- |
| uap (piattaforma UWP) | win81     |
|                                  | wpa81     |
|                                  | netcore50 |
| win (Windows Store)              | winrt     |
|                                  | winrt45   |

## <a name="net-standard"></a>.NET Standard

[.NET Standard](https://github.com/dotnet/standard) semplifica i riferimenti tra framework compatibili con il codice binario, consentendo a un framework di destinazione singolo di fare riferimento a una combinazione di altri framework. Per altre informazioni, vedere l'argomento [Libreria .NET Standard](library.md).

Lo [strumento Get Nearest Framework degli strumenti NuGet](http://nugettoolsdev.azurewebsites.net/) simula la logica di NuGet usata per la selezione di un framework da molte risorse di framework disponibili in un pacchetto sulla base del framework di progetto. Per usare questo strumento, inserire un framework di progetto e uno o più framework di pacchetto. Selezionare il pulsante **Submit** (Invia). Lo strumento indica se i framework di pacchetto elencati sono compatibili con il framework di progetto fornito.

## <a name="portable-class-libraries"></a>Librerie di classi portabili

Per informazioni sulle librerie di classi portabili, vedere la sezione relativa alle [librerie di classi portabili](https://docs.microsoft.com/nuget/schema/target-frameworks#portable-class-libraries) dell'argomento *Target frameworks* (Framework di destinazione) nella documentazione di NuGet. Stephen Cleary ha creato uno strumento che elenca le librerie di classi portabili supportate. Per altre informazioni, vedere [Framework Profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili dei framework in .NET).

