---
title: Compilazione di immagini Docker per .NET Core
description: Informazioni sulle immagini Docker e su .NET Core
keywords: .NET, .NET Core, Docker
author: spboyer
ms.author: shboyer
ms.date: 08/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-docker
ms.devlang: dotnet
ms.assetid: 03c28597-7e73-46d6-a9c3-f9cb55642739
ms.translationtype: Human Translation
ms.sourcegitcommit: 890c058bd09893c2adb185e1d8107246eef2e20a
ms.openlocfilehash: 007d96cf7d174e7849a2b9c8439cfac893c7aa5c
ms.contentlocale: it-it
ms.lasthandoff: 04/12/2017

---
 

#<a name="building-docker-images-for-net-core-applications"></a>Compilazione di immagini Docker per applicazioni .NET Core

Per comprendere in che modo usare insieme .NET Core e Docker, è necessario prima conoscere le diverse immagini Docker disponibili e i casi in cui è opportuno usarle. Di seguito verranno illustrate in modo dettagliato le variazioni offerte, verrà creata un'API Web ASP.NET Core, verranno usati gli strumenti Yeoman Docker per creare un contenitore sottoponibile a debug e verrà mostrato in che modo è possibile usare Visual Studio Code per l'esecuzione del processo. 

## <a name="docker-image-optimizations"></a>Ottimizzazioni delle immagini Docker

Quando si creano immagini Docker per gli sviluppatori, è opportuno concentrare l'attenzione su tre scenari principali:

- Immagini usate per sviluppare app .NET Core
- Immagini usate per compilare app .NET Core
- Immagini usate per eseguire app .NET Core

Perché tre immagini?
Durante lo sviluppo, la compilazione e l'esecuzione di applicazioni nei contenitori, è necessario tenere conto di diverse priorità.
- **Sviluppo:** qual è la velocità di iterazione delle modifiche? È possibile eseguirne il debug? Le dimensioni dell'immagine non sono essenziali, mentre è importante la possibilità di apportare modifiche al codice e visualizzare rapidamente tali modifiche. Alcuni degli strumenti Microsoft, ad esempio [yo docker](https://aka.ms/yodocker), da usare nel codice Visual Studio utilizzano questa immagine durante la fase di sviluppo. 
- **Compilazione:** quali sono gli elementi necessari per compilare l'app? Questi elementi includono il compilatore e qualsiasi altra dipendenza necessaria per ottimizzare i file binari. Questa immagine non è quella che verrà distribuita, ma piuttosto un'immagine usata per compilare il contenuto inserito in un'immagine di produzione. Questa immagine verrà usata nell'integrazione continuativa o nell'ambiente di compilazione. Ad esempio, anziché installare le dipendenze direttamente in un agente di compilazione, quest'ultimo creerà un'istanza dell'immagine di compilazione per compilare l'applicazione contenuta nell'immagine stessa con tutte le dipendenze necessarie. Per l'agente di compilazione è necessario soltanto sapere come eseguire questa immagine Docker. 
- **Produzione:** con quale velocità è possibile distribuire e avviare l'immagine? Questa immagine ha dimensioni ridotte, motivo per cui può passare rapidamente attraverso la rete dal registro Docker agli host Docker. Il contenuto è pronto per l'esecuzione, rendendo minimo l'intervallo tra l'esecuzione Docker e l'elaborazione dei risultati. Nel modello Docker non modificabile non è necessaria la compilazione dinamica del codice. Il contenuto inserito in questa immagine sarà limitato ai file binari e al contenuto necessario per eseguire l'applicazione, ad esempio l'output pubblicato usando `dotnet publish` e contenente i file binari, le immagini e i file con estensione js e css compilati. Nel corso del tempo si vedranno immagini contenenti pacchetti PreJit.  

Anche se sono presenti più versioni dell'immagine .NET Core, tutte queste versioni condividono uno o più layer. La quantità di spazio su disco necessaria per l'archiviazione o per il delta per effettuare il pull dal Registro di sistema è molto minore dell'insieme delle immagini, perché tutte le immagini condividono lo stesso layer di base e potenzialmente altri layer.  

## <a name="docker-image-variations"></a>Variazioni delle immagini Docker

Per raggiungere gli obiettivi sopra descritti, in [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/) sono disponibili varianti delle immagini.

- `microsoft/dotnet:<version>-sdk` : ovvero **microsoft/dotnet:1.0.0-preview2-sdk**. Questa immagine contiene .NET Core SDK che include gli strumenti .NET Core e quelli dell'interfaccia della riga di comando. Questa immagine è mappata allo **scenario di sviluppo**. Usare questa immagine per operazioni locali di sviluppo, debug e testing unità, ad esempio tutte le attività di sviluppo eseguite prima dell'archiviazione del codice. Questa immagine può essere usata anche per gli scenari di **compilazione**.

- `microsoft/dotnet:<version>-core` : ovvero **microsoft/dotnet:1.0.0-core**. Questa immagine esegue [applicazioni .NET Core portabili](../deploying/index.md) ed è ottimizzata per l'esecuzione dell'applicazione nella fase di **produzione**. Non contiene l'SDK ed è finalizzata all'acquisizione dell'output ottimizzato di `dotnet publish`. Il runtime portabile è adatto agli scenari Docker di contenitore poiché l'esecuzione di più contenitori trae vantaggio dai layer di immagine condivisi.  

## <a name="alternative-images"></a>Immagini alternative

Oltre agli scenari ottimizzati di sviluppo, compilazione e produzione, Microsoft fornisce immagini aggiuntive:

- `microsoft/dotnet:<version>-onbuild` : ovvero **microsoft/dotnet:1.0.0-preview2-onbuild**. Contiene trigger [ONBUILD](https://docs.docker.com/engine/reference/builder/#/onbuild). La compilazione eseguirà il comando [COPY](https://docs.docker.com/engine/reference/builder/#/copy) sull'applicazione, eseguirà `dotnet restore` e creerà un'istruzione [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint) `dotnet run` per eseguire l'applicazione al momento dell'esecuzione dell'immagine Docker. Anche se non si tratta di un'immagine ottimizzata per la produzione, alcuni utenti possono trovarla utile per copiare semplicemente il codice sorgente in un'immagine ed eseguirlo. 

- `microsoft/dotnet:<version>-core-deps` : ovvero **microsoft/dotnet:1.0.0-core-deps**. Usare questa immagine, se si vogliono eseguire applicazioni autonome. Questa immagine contiene il sistema operativo con tutte le dipendenze native richieste da .NET Core. Può essere usata anche come immagine di base per compilazioni CoreFX o CoreCLR personalizzate. Mentre la variante **onbuild** è ottimizzata per inserire semplicemente il codice in un'immagine ed eseguirlo, questa immagine è ottimizzata per contenere soltanto le dipendenze del sistema operativo necessarie per l'esecuzione di app .NET Core per cui viene fornito anche il runtime di .NET. Questa immagine non è in genere ottimizzata per l'esecuzione di più contenitori .NET Core nello stesso host. Ciascuna immagine infatti include il runtime di .NET Core e di conseguenza la struttura multi-layer delle immagini non offrirà alcun vantaggio.   

Versioni più recenti di ciascuna variante:

- `microsoft/dotnet` o `microsoft/dotnet:latest` (include l'SDK)
- `microsoft/dotnet:onbuild`
- `microsoft/dotnet:core`
- `microsoft/dotnet:core-deps`

Di seguito è riportato un elenco delle immagini dopo un'operazione `docker pull <imagename>` in un computer di sviluppo per mostrare le diverse dimensioni. Si noti che la variante di sviluppo/compilazione, `microsoft/dotnet:1.0.0-preview2-sdk`, ha dimensioni maggiori in quanto contiene l'SDK per lo sviluppo e la compilazione dell'applicazione. La variante di produzione, `microsoft/dotnet:core`, ha dimensioni minori, in quanto contiene soltanto il runtime di NET Core. L'immagine minima utilizzabile in Linux, `core-deps`, ha dimensioni abbastanza ridotte. L'applicazione, tuttavia, dovrà eseguire una copia privata del runtime di .NET con tale immagine. Dal momento che i contenitori sono già barriere private per l'isolamento, quando si eseguono più contenitori basati su .NET tale ottimizzazione andrà perduta. 

```
REPOSITORY          TAG                     IMAGE ID            SIZE
microsoft/dotnet    1.0.0-preview2-onbuild  19b6a6c4b1db        540.4 MB
microsoft/dotnet    onbuild                 19b6a6c4b1db        540.4 MB
microsoft/dotnet    1.0.0-preview2-sdk      a92c3d9ad0e7        540.4 MB
microsoft/dotnet    core                    5224a9f2a2aa        253.2 MB
microsoft/dotnet    1.0.0-core-deps         c981a2eebe0e        166.2 MB
microsoft/dotnet    core-deps               c981a2eebe0e        166.2 MB
microsoft/dotnet    latest                  03c10abbd08a        540.4 MB
microsoft/dotnet    1.0.0-core              b8da4a1fd280        253.2 MB
```

## <a name="prerequisites"></a>Prerequisiti

Per la compilazione e l'esecuzione è necessario che nel computer siano installati gli elementi seguenti:

- [.NET Core](http://dot.net)
- [Docker](https://www.docker.com/products/docker), per eseguire localmente i contenitori Docker 
- [Generatore Yeoman per ASP.NET](https://github.com/omnisharp/generator-aspnet), per creare l'applicazione API Web
- [Generatore Yeoman per Docker](http://aka.ms/yodocker), fornito da Microsoft

Installare i generatori Yeoman per ASP.NET Core e Docker usando npm 

```
npm install -g yo generator-aspnet generator-docker
```

> [!NOTE]
> Questo esempio userà [Visual Studio Code](http://code.visualstudio.com) per l'editor.

## <a name="creating-the-web-api-application"></a>Creazione dell'applicazione API Web

Come punto di riferimento, prima di inserire l'applicazione nei contenitori, eseguirla localmente. 

L'applicazione completata si trova nel repository [dotnet/docs su GitHub](https://github.com/dotnet/docs/tree/master/samples/core/docker/building-net-docker-images). Per istruzioni sul download, vedere [Esempi ed esercitazioni](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

Creare una directory per l'applicazione.

Aprire una sessione della riga di comando o terminal in tale directory e usare il generatore Yeoman ASP.NET digitando quanto segue:
```
yo aspnet
```

Selezionare l'**applicazione API Web**, digitare **api** come nome dell'app, quindi premere INVIO.  Dopo che è stato eseguito lo scaffolding dell'applicazione, passare alla directory `/api` e ripristinare le dipendenze NuGet usando `dotnet restore`.

```
cd api
dotnet restore
```

Testare l'applicazione usando `dotnet run` e i valori disponibili in **http://localhost:5000/api/values**

```javascript
[
    "value1",
    "value2"
]
```

Usare `Ctrl+C` per arrestare l'applicazione.

## <a name="adding-docker-support"></a>Aggiunta del supporto per Docker

Per aggiungere al progetto il supporto per Docker usare il generatore Yeoman fornito da Microsoft. Questo generatore attualmente supporta progetti .NET Core, Node.js e Go mediante la creazione di un documento Dockerfile e di script che consentono di compilare ed eseguire progetti all'interno dei contenitori. Vengono aggiunti anche specifici file Visual Studio Code (launch.json, tasks.json) per il debug dell'editor e il supporto del riquadro comandi.

```console
$ yo docker

     _-----_     ╭──────────────────────────╮
    |       |    │   Welcome to the Docker  │
    |--(o)--|    │        generator!        │
   `---------´   │     Let's add Docker     │
    ( _´U`_ )    │  container magic to your │
    /___A___\   /│           app!           │
     |  ~  |     ╰──────────────────────────╯
   __'.___.'__
 ´   `  |° ´ Y `

? What language is your project using? (Use arrow keys)
❯ .NET Core
  Golang
  Node.js
```

- Selezionare `.NET Core` come tipo di progetto
- `rtm` per la versione di .NET Core
- `Y` il progetto usa un server Web
- `5000` la porta su cui l'applicazione API Web è in ascolto (http://localhost:5000)
- `api` per il nome dell'immagine
- `api` per il nome del servizio
- `api` per il progetto di composizione 
- `Y` per sovrascrivere il documento Dockerfile corrente

Quando il generatore è completo, al progetto vengono aggiunti i file seguenti:

- .vscode/launch.json
- Dockerfile.debug
- Dockerfile
- docker-compose.debug.yml
- docker-compose.yml
- dockerTask.ps1
- dockerTask.sh
- .vscode/tasks.json

Il generatore crea due documenti Dockerfile.

**Dockerfile.debug**: questo file è basato sull'immagine **microsoft/dotnet:1.0.0-preview2-sdk** che, come si nota dall'elenco delle varianti di immagine, include SDK, interfaccia della riga di comando e .NET Core. Tale immagine sarà quella usata per lo sviluppo e il debug (F5). L'inclusione di tutti questi componenti crea un'immagine più grande, di dimensioni pari a circa 540 MB.

**Dockerfile**: si tratta dell'immagine della versione basata su **microsoft/dotnet:1.0.0-core** e deve essere usata per la produzione. Quando eseguita, questa immagine è pari a circa 253 MB.

### <a name="creating-the-docker-images"></a>Creazione di immagini Docker
Usando lo script `dockerTask.sh` o `dockerTask.ps1` è possibile compilare o comporre l'immagine e il contenitore dell'applicazione **api** per un ambiente specifico. Compilare l'immagine di **debug** eseguendo il comando seguente.

```bash
./dockerTask.sh build debug
```

L'immagine compilerà l'applicazione ASP.NET, eseguirà `dotnet restore`, aggiungerà il debugger all'immagine, imposterà un `ENTRYPOINT` e al termine copierà l'app nell'immagine. Il risultato è un'immagine Docker denominata *api* con un `TAG` di *debug*.  Vedere le immagini sul computer usando `docker images`.

```bash
docker images

REPOSITORY          TAG                  IMAGE ID            CREATED             SIZE
api                 debug                70e89fbc5dbe        a few seconds ago   779.8 MB
```

Un altro modo per generare l'immagine ed eseguire l'applicazione all'interno del contenitore Docker consiste nell'aprire l'applicazione in Visual Studio Code e usare gli strumenti di debug. 

Selezionare l'icona per il debug nella barra di sinistra di Visual Studio Code.

![icona per il debug di Visual Studio Code](./media/building-net-docker-images/debugging_debugicon.png)

Fare quindi clic sull'icona per la riproduzione o premere F5 per generare l'immagine e avviare l'applicazione all'interno del contenitore. L'applicazione API Web verrà avviata usando il Web browser predefinito in http://localhost:5000.

![Visual Studio Code - Strumenti di debug Docker](./media/building-net-docker-images/docker-tools-vscode-f5.png)

Nell'applicazione è possibile impostare punti di interruzione, passaggi e così via come se l'applicazione stessa fosse in esecuzione in locale sul computer di sviluppo e non all'interno del contenitore. Il vantaggio di eseguire il debug all'interno del contenitore consiste nel fatto che questa è la stessa immagine che verrà distribuita in un ambiente di produzione.

Per la creazione dell'immagine della versione o di produzione è sufficiente eseguire questo comando dal terminale passando il nome di ambiente `release`.

```bash
./dockerTask build release
```

Il comando crea l'immagine basandosi sull'immagine di base **microsoft/dotnet:core** più piccola, esegue un [EXPOSE](https://docs.docker.com/engine/reference/builder/#/expose) sulla porta 5000, imposta l'[ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint) per `dotnet api.dll` e lo copia nella directory `/app`. Non è presente alcun debugger, SDK o `dotnet restore` risultante in un'immagine molto più piccola. L'immagine è denominata **api** e ha un `TAG` di tipo **latest**.

```
REPOSITORY          TAG                  IMAGE ID            CREATED             SIZE
api                 debug                70e89fbc5dbe        1 hour ago        779.8 MB
api                 latest               ef17184c8de6        1 hour ago        260.7 MB
```

## <a name="summary"></a>Riepilogo

L'uso del generatore Docker per aggiungere i file necessari all'applicazione API Web semplifica il processo di creazione delle versioni di sviluppo e produzione delle immagini.  Gli strumenti sono multipiattaforma e forniscono anche uno script PowerShell per ottenere gli stessi risultati riguardo all'integrazione di Windows e Visual Studio Code, con procedure per il debug dell'applicazione all'interno del contenitore. La comprensione delle varianti delle immagini e degli scenari di destinazione consente di ottimizzare i processi di sviluppo a ciclo interno, ottenendo al tempo stesso immagini ottimizzate per le distribuzioni di produzione.  



