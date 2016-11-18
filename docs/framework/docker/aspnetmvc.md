---
title: Migrazione di applicazioni ASP.NET MVC ai contenitori di Windows
description: Informazioni su come eseguire un&quot;applicazione ASP.NET MVC esistente in un contenitore Docker di Windows
keywords: Contenitori di Windows, Docker, ASP.NET MVC
author: BillWagner
manager: wpickett
ms.date: 09/28/2016
ms.topic: article
ms.prod: .net-framework-4.6
ms.technology: dotnet-mvc
ms.devlang: dotnet
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
translationtype: Human Translation
ms.sourcegitcommit: 15c55a87beb64f265a164db918c7721c7690fadf
ms.openlocfilehash: 3e8a8a953cbb3dde6ddf386f8c3b3a1fd4c549f1

---

# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>Migrazione di applicazioni ASP.NET MVC ai contenitori di Windows

L'esecuzione di un'applicazione esistente basata su .NET Framework in un contenitore di Windows richiede la creazione dell'immagine Docker che contiene l'applicazione e l'avvio di uno o più contenitori per eseguire l'immagine. In questo argomento vengono illustrate le operazioni da eseguire per distribuire un'[applicazione ASP.NET MVC](http://www.asp.net/mvc) esistente in un contenitore di Windows.

Si inizia con un'applicazione ASP.NET MVC già esistente. In seguito si compilano le risorse pubblicate usando Visual Studio. Viene quindi creata con Docker l'immagine che contiene l'applicazione e la esegue quando viene avviata. Al termine, è possibile connettere un browser al sito eseguito in un contenitore di Windows e verificare se l'applicazione è in esecuzione.

In questo articolo si presuppone che l'utente abbia una conoscenza di base di Docker. Se questi concetti sono nuovi, altre informazioni sull'architettura Docker sono disponibili in [Panoramica Docker](https://docs.docker.com/engine/understanding-docker/) nel sito di Docker.

L'applicazione che verrà eseguita in un contenitore è un semplice sito Web che risponde alle domande in modo casuale. Questa applicazione è un'applicazione MVC di base senza supporto per l'autenticazione né archiviazione nel database, che consente di concentrarsi sullo spostamento del livello Web in un contenitore. Gli argomenti successivi spiegheranno come spostare e gestire l'archiviazione permanente nelle applicazioni eseguite nei contenitori.

Per spostare l'applicazione sono necessari i passaggi seguenti:

1. [Creazione di un'attività di pubblicazione per compilare le risorse necessarie per un'immagine.](#publish-script)
2. [Creazione di un'immagine Docker che eseguirà l'applicazione.](#build-the-image)
3. [Avvio di un contenitore Docker che esegue l'immagine.](#start-a-container)
4. [Verifica dell'applicazione con il browser.](#verify-in-the-browser)

L'applicazione completata si trova nel [repository dotnet/core-docs su GitHub](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator).

## <a name="prerequisites"></a>Prerequisiti

Come minimo, il computer di sviluppo deve eseguire l'[Aggiornamento dell'anniversario di Windows 10](https://www.microsoft.com/en-us/software-download/windows10/) o [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server). 

Prima di iniziare, è necessario installare [Docker per Windows](https://docs.docker.com/docker-for-windows/) versione 1.12 Beta 26 o versione successiva. Il supporto per i contenitori di Windows per il momento è disponibile solo nel canale Beta.

> [!IMPORTANT]
> Se si usa Windows Server 2016, è necessario seguire le istruzioni riportate in [Distribuzione di host contenitore - Windows Server](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/deployment/deployment) prima di eseguire i contenitori Docker.

Dopo aver installato e avviato Docker, è necessario fare clic con il pulsante destro del mouse sull'icona della barra delle applicazioni e selezionare l'opzione che consente di **passare ai contenitori di Windows** per eseguire le immagini Docker basate su Windows. L'esecuzione del comando richiede alcuni secondi:

![Contenitore di Windows][windows-container]

## <a name="publish-script"></a>Pubblicare lo script

Il primo passaggio consiste nel riunire in un'unica posizione tutti gli asset da caricare in un'immagine Docker. Fortunatamente è possibile usare il comando **Pubblica** di Visual Studio per creare un profilo di pubblicazione per l'applicazione. Tale profilo consente di inserire tutti gli asset in un'unica struttura di directory che verrà copiata nell'immagine di destinazione più avanti in questa esercitazione.

**Procedura di pubblicazione**

1. Fare clic con il pulsante destro del mouse sul progetto Web in Visual Studio e selezionare **Pubblica**.
2. Fare clic sul **pulsante del profilo personalizzato e quindi selezionare **File system** come metodo.
3. Scegliere la directory. Per convenzione, l'esempio scaricato usa `bin/PublishOutput`.

![Connessione di pubblicazione][publish-connection]

Aprire quindi la sezione **Opzioni pubblicazione file** della scheda **Impostazioni**. Selezionare **Precompila durante la pubblicazione**. Questa ottimizzazione significa che compilando le viste nel contenitore Docker, si stanno copiando le viste precompilate.

![Impostazioni di pubblicazione][publish-settings]

Fare clic su **Pubblica** in modo che Visual Studio copi tutti gli asset necessari nella cartella di destinazione. 

## <a name="build-the-image"></a>Creare l'immagine

L'immagine Docker viene definita in un documento Dockerfile che contiene le istruzioni per l'immagine di base, eventuali componenti aggiuntivi, l'applicazione da eseguire e altre immagini di configurazione.  Il Dockerfile costituisce l'input per il comando `docker build` che crea l'immagine.

Verrà creata un'immagine basata sull'immagine `microsft/aspnet` situata nell'[hub Docker](https://hub.docker.com/r/microsoft/aspnet/).
L'immagine di base, `microsoft/aspnet`, è un'immagine di Windows Server. Oltre a Windows Server Core, sono installati e abilitati IIS e ASP.NET 4.6.2. Quando si esegue questa immagine in un contenitore, viene automaticamente avviato IIS e tutti i siti Web installati diventano attivi.

Il documento Dockerfile che crea l'immagine è simile al seguente:

```
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# Next, this Dockerfile creates a directory for your application
RUN mkdir C:\randomanswers

# configure the new site in IIS.
RUN powershell -NoProfile -Command \
    Import-module IISAdministration; \
    New-IISSite -Name "ASPNET" -PhysicalPath C:\randomanswers -BindingInformation "*:8000:"

# This instruction tells the container to listen on port 8000. 
EXPOSE 8000

# The final instruction copies the site you published earlier into the container.
ADD containerImage/ /randomanswers
```

Non esiste alcun comando `ENTRYPOINT` in questo Dockerfile. Non è necessario.
L'immagine di base assicura che IIS venga avviato all'avvio del contenitore. 

Successivamente sarà necessario eseguire un comando di compilazione di Docker per creare l'immagine che eseguirà l'applicazione ASP.NET. A tale scopo, aprire una finestra di PowerShell e digitare il comando seguente nella directory soluzione:

```
docker build -t mvcrandomanswers .
```

Questo comando consente di creare la nuova immagine seguendo le istruzioni nel documento Dockerfile. Può essere necessario estrarre l'immagine di base dall'[hub Docker](http://hub.docker.com) per aggiungere l'applicazione a tale immagine.

Dopo aver completato il comando è possibile eseguire il comando `docker images` per visualizzare informazioni sulla nuova immagine:

```
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       8.104 GB
```

L'ID immagine sarà diverso nel computer in uso. A questo punto è possibile eseguire l'applicazione.

## <a name="start-a-container"></a>Avviare un contenitore

Per avviare un contenitore eseguire il comando `docker run` seguente:

```
docker run -d -p 8000:8000 --name randomanswers mvcrandomanswers
```

L'argomento `-d` indica a Docker di avviare l'immagine senza collegamento. Ciò significa che l'immagine Docker viene eseguita scollegata dalla shell corrente.

L'argomento `-p 8000:8000` indica a Docker in che modo devono essere mappate le porte in ingresso. In questo esempio viene usata la porta 8000 sia per l'host che per il contenitore.

Il valore `--name randomanswers` assegna un nome al contenitore in esecuzione. È possibile usare questo nome anziché l'ID del contenitore nella maggior parte dei comandi.

Il valore `mvcrandomanswers` è il nome dell'immagine da avviare.

## <a name="verify-in-the-browser"></a>Verificare nel browser

> [!NOTE]
> Con la versione corrente non è possibile usare `http://localhost` per passare al sito. La causa è un comportamento noto in WinNAT, che verrà risolto in futuro. Fino a quel momento sarà necessario usare l'indirizzo IP del contenitore.

Dopo l'avvio del contenitore è necessario trovarne l'indirizzo IP in modo da consentire la connessione al contenitore in esecuzione da un browser:

```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" randomanswers
172.31.194.61
```

È possibile connettersi al contenitore in esecuzione usando l'indirizzo IPv4 e la porta configurata (8000), `http://172.31.194.61:8000` nell'esempio illustrato. Digitando l'URL nel browser viene visualizzato il sito in esecuzione.

> [!NOTE]
> Alcuni software VPN o proxy possono impedire la navigazione nel sito.
> È possibile disabilitarli temporaneamente per verificare che il contenitore funzioni.

La directory di esempio su GitHub contiene un [script di PowerShell](https://github.com/dotnet/docs/tree/master/samples/framework/docker/MVCRandomAnswerGenerator/run.ps1) che esegue automaticamente questi comandi. Aprire una finestra di PowerShell, passare alla directory soluzione e digitare:

```
./run.ps1
```

Il comando crea l'immagine, visualizza l'elenco di immagini presenti nel computer, avvia un contenitore e visualizza l'indirizzo IP per tale contenitore. 

Al termine, per arrestare il contenitore, eseguire un comando `docker
stop`:

```
docker stop randomanswers
```

Per rimuovere il contenitore, eseguire un comando `docker rm`:

```
docker rm randomanswers
```

## <a name="summary"></a>Riepilogo

Questo argomento ha illustrato la procedura richiesta per spostare ed eseguire un'applicazione ASP.NET MVC esistente in un contenitore di Windows Server. L'esecuzione di un'applicazione esistente non richiede modifiche all'applicazione. È necessario eseguire le attività richieste per pubblicare l'applicazione, creare un'immagine Docker e avviare tale immagine in un nuovo contenitore. L'uso dei contenitori di Windows Server è il metodo più semplice per eseguire la migrazione delle applicazioni esistenti in questo ambiente.

[windows-container]: media/aspnetmvc/SwitchContainer.png "Passare a un contenitore di Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Pubblicare nel File system"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Impostazioni di pubblicazione"



<!--HONumber=Nov16_HO3-->


