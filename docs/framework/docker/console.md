---
title: Esecuzione di applicazioni console in Docker
description: Informazioni su come eseguire un&quot;applicazione console .NET Framework esistente in un contenitore Docker di Windows.
author: spboyer
keywords: .NET, Contenitore, Console, Applicazioni
ms.date: 09/28/2016
ms.topic: article
ms.prod: .net-framework-4.6
ms.technology: vs-ide-deployment
ms.devlang: dotnet
ms.assetid: 85cca1d5-c9a4-4eb2-93e6-4f878de07fd7
translationtype: Human Translation
ms.sourcegitcommit: 890c058bd09893c2adb185e1d8107246eef2e20a
ms.openlocfilehash: 4f1034763e4dae3711694b441b7a64b40cc99456
ms.lasthandoff: 04/18/2017

---

# <a name="running-console-applications-in-windows-containers"></a>Esecuzione di applicazioni console in contenitori Windows

Le applicazioni console vengono usate per scopi diversi, dalla semplice esecuzione di query sullo stato ad attività di elaborazione di immagini documento a esecuzione prolungata. In ogni caso, la possibilità di avviare e ridimensionare tali applicazioni dipende da limitazioni relative all'acquisizione di hardware, ai tempi di avvio e all'esecuzione di più istanze.

Lo spostamento delle applicazioni console per l'uso di contenitori Docker e Windows Server consente di avviare tali applicazioni partendo da uno stato originario, in modo che possano eseguire l'operazione e arrestarsi correttamente. In questo argomento verranno illustrati i passaggi necessari per spostare un'applicazione console in un contenitore basato su Windows e avviarla tramite uno script di PowerShell.

L'applicazione console di esempio è un esempio semplice che prende un argomento, in questo caso una domanda, e restituisce una risposta casuale. Potrebbe trattarsi di prendere un `customer_id` ed elaborarne le imposte o di creare un'anteprima per un argomento `image_url`.

Oltre alla risposta, `Environment.MachineName` è stato aggiunto per illustrare la differenza tra l'esecuzione dell'applicazione in locale e in un contenitore di Windows. Quando si esegue l'applicazione localmente, deve essere restituito il nome del computer locale mentre, durante l'esecuzione in un contenitore di Windows, viene restituito l'id di sessione del contenitore.

L'[esempio completo](https://github.com/dotnet/docs/tree/master/samples/framework/docker/ConsoleRandomAnswerGenerator) è disponibile nel repository dotnet/docs su GitHub. Per istruzioni sul download, vedere [Esempi ed esercitazioni](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

È necessario avere familiarità con alcuni termini di Docker prima di iniziare lo spostamento dell'applicazione in un contenitore.

> Una *immagine Docker* è un modello di sola lettura che definisce l'ambiente per un contenitore in esecuzione, inclusi il sistema operativo, i componenti di sistema e le applicazioni.

Una delle caratteristiche principali delle immagini Docker è che sono costituite da un'immagine di base. Ogni nuova immagine aggiunge un piccolo set di funzionalità a un'immagine esistente. 

> Un *contenitore Docker* è un'istanza di un'immagine in esecuzione. 

Un'applicazione viene ridimensionata eseguendo la stessa immagine in più contenitori.
Concettualmente, è molto simile all'esecuzione della stessa applicazione in più host.

Per altre informazioni sull'architettura Docker, vedere [Docker Overview](https://docs.docker.com/engine/understanding-docker/) (Panoramica di Docker) nel sito di Docker. 

Lo spostamento dell'applicazione non richiede che pochi passaggi.

1. [Compilare l'applicazione](#building-the-application)
1. [Creazione di un documento Dockerfile per l'immagine](#creating-the-dockerfile)
1. [Processo di compilazione ed esecuzione del contenitore Docker](#creating-the-image)

## <a name="prerequisites"></a>Prerequisiti
I contenitori di Windows sono supportati in [Aggiornamento dell'anniversario di Windows 10](https://www.microsoft.com/en-us/software-download/windows10/) o [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server).

> [!NOTE]
>Se si usa Windows Server 2016, è necessario abilitare manualmente i contenitori poiché il programma di installazione di Docker per Windows non abilita tale funzionalità. Assicurarsi che tutti gli aggiornamenti siano stati eseguiti per il sistema operativo e seguire le istruzioni dell'articolo [Distribuzione di host contenitore - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment) per installare le funzionalità di Docker e dei contenitori.

Per il supporto dei contenitori Windows è necessario avere Docker per Windows versione 1.12 Beta 26 o versione successiva. Per impostazione predefinita, Docker abilita contenitori basati su Linux. Per passare ai contenitori Windows, fare clic con il pulsante destro del mouse sull'icona di Docker nell'area di notifica e selezionare **Switch to Windows containers** (Passa a contenitori Windows). Docker eseguirà il processo di modifica e potrebbe essere necessario un riavvio.

![Contenitori di Windows](./media/console/SwitchContainer.png)

## <a name="building-the-application"></a>Compilazione dell'applicazione
In genere le applicazioni console vengono distribuite attraverso un programma di installazione, FTP o una distribuzione di condivisione file. Quando si esegue la distribuzione in un contenitore, le risorse devono essere compilate e inserite temporaneamente in un percorso che può essere usato quando viene creata l'immagine Docker.

In *build.ps1* lo script usa [MSBuild](https://msdn.microsoft.com/library/dd393574.aspx) per compilare l'applicazione per completare l'attività di creazione delle risorse. Vi sono alcuni parametri che vengono passati a MSBuild per finalizzare le risorse necessarie. Il nome del file di progetto o della soluzione da compilare, il percorso dell'output e, infine, la configurazione (Release o Debug).

Nella chiamata a `Invoke-MSBuild` `OutputPath` è impostato su **publish** e `Configuration` è impostato su **Release**. 

```
function Invoke-MSBuild ([string]$MSBuildPath, [string]$MSBuildParameters) {
    Invoke-Expression "$MSBuildPath $MSBuildParameters"
}

Invoke-MSBuild -MSBuildPath "MSBuild.exe" -MSBuildParameters ".\ConsoleRandomAnswerGenerator.csproj /p:OutputPath=.\publish /p:Configuration=Release"
```

## <a name="creating-the-dockerfile"></a>Creazione del documento Dockerfile
L'immagine di base usata per un'applicazione console .NET Framework è `microsoft/windowsservercore`, disponibile pubblicamente nell'[hub Docker](https://hub.docker.com/r/microsoft/windowsservercore/). L'immagine di base contiene un'installazione minima di Windows Server 2016, .NET Framework 4.6.2 e viene usata come immagine di base del sistema operativo per i contenitori Windows.

```
FROM microsoft/windowsservercore
ADD publish/ /
ENTRYPOINT ConsoleRandomAnswerGenerator.exe
```
La prima riga del documento Dockerfile definisce l'immagine di base tramite l'istruzione [`FROM`](https://docs.docker.com/engine/reference/builder/#/from). Successivamente, l'istruzione [`ADD`](https://docs.docker.com/engine/reference/builder/#/add) nel file copia le risorse dell'applicazione dalla cartella **publish** alla cartella radice del contenitore. Infine, impostando il valore [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#/entrypoint) dell'immagine si indica che questo è il comando o l'applicazione che verrà eseguita all'avvio del contenitore. 

## <a name="creating-the-image"></a>Creazione dell'immagine
Per creare l'immagine Docker, viene aggiunto il codice seguente allo script *build.ps1*. Quando lo script viene eseguito, viene creata l'immagine `console-random-answer-generator` tramite l'uso delle risorse compilate da MSBuild definite nella sezione [Compilazione dell'applicazione](#building-the-application).

```
$ImageName="console-random-answer-generator"

function Invoke-Docker-Build ([string]$ImageName, [string]$ImagePath, [string]$DockerBuildArgs = "") {
    echo "docker build -t $ImageName $ImagePath $DockerBuildArgs"
    Invoke-Expression "docker build -t $ImageName $ImagePath $DockerBuildArgs"
}

Invoke-Docker-Build -ImageName $ImageName -ImagePath "."
```

Eseguire lo script usando `.\build.ps1` al prompt dei comandi di PowerShell.

Una volta completata la compilazione, usare il comando `docker images` da una riga di comando o al prompt dei comandi di PowerShell. Si noterà che l'immagine è stata creata ed è pronta per essere eseguita.

```
REPOSITORY                        TAG                 IMAGE ID            CREATED             SIZE
console-random-answer-generator   latest              8f7c807db1b5        8 seconds ago       7.33 GB
```

## <a name="running-the-container"></a>Esecuzione del contenitore
È possibile avviare il contenitore dalla riga di comando tramite i comandi di Docker.

```
docker run console-random-answer-generator "Are you a square container?"
```

L'output è

```
The answer to your question: 'Are you a square container?' is Concentrate and ask again on (70C3D48F4343)
```

Se si esegue il comando `docker ps -a` da PowerShell, è possibile vedere che il contenitore è ancora presente.

```
CONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS                          
70c3d48f4343        console-random-answer-generator   "cmd /S /C ConsoleRan"   2 minutes ago       Exited (0) About a minute ago      
```

Nella colonna STATUS viene indicato che "About a minute ago" (circa un minuto fa) l'applicazione è stata completata ed è possibile arrestarla. Se il comando fosse stato eseguito un centinaio di volte, vi sarebbero cento contenitori statici, lasciati senza alcuna operazione da eseguire. Nello scenario iniziale l'operazione ideale è stata quella di eseguire le operazioni e quindi chiudere o eseguire la pulizia. Per completare il flusso di lavoro, aggiungere l'opzione `--rm` al comando `docker run` per rimuovere il contenitore non appena viene ricevuto il segnale `Exited`.

```
docker run --rm console-random-answer-generator "Are you a square container?"
```

Se si esegue il comando con questa opzione e quindi si esamina l'output del comando `docker ps -a`, si noterà che l'id del contenitore (`Environment.MachineName`) non è presente nell'elenco.

### <a name="running-the-container-using-powershell"></a>Esecuzione del contenitore tramite PowerShell
Nei file di progetto di esempio è anche disponibile un'istruzione *run.ps1* che è un esempio di come usare PowerShell per eseguire l'applicazione accettando gli argomenti.

Per l'esecuzione, aprire PowerShell e usare il comando seguente:

```
.\run.ps1 "Is this easy or what?"
```

## <a name="summary"></a>Riepilogo
È sufficiente aggiungere un documento Dockerfile e pubblicare l'applicazione per eseguire le applicazioni console .NET Framework in un contenitore e poter sfruttare tutti i vantaggi dell'esecuzione di più istanze, avvio e arresto corretti e altre funzionalità di Windows Server 2016 senza apportare modifiche al codice dell'applicazione.

