---
title: Microservizi ospitati in Docker | C#
description: Informazioni su come creare servizi ASP.NET Core in esecuzione in contenitori Docker
keywords: .NET, .NET Core, Docker, C#, ASP.NET, microservizio
author: BillWagner
ms.author: wiwagn
ms.date: 02/03/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-docker
ms.devlang: csharp
ms.assetid: 87e93838-a363-4813-b859-7356023d98ed
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 57c49b555d7989a27fb4a2943b72cd2c4849694b
ms.lasthandoff: 03/13/2017

---

# <a name="microservices-hosted-in-docker"></a>Microservizi ospitati in Docker

##<a name="introduction"></a>Introduzione

Questa esercitazione descrive nel dettaglio la procedura per creare e distribuire un microservizio ASP.NET Core in un contenitore Docker. Nel corso di questa esercitazione verranno illustrate le attività seguenti:

* Generazione di un'applicazione ASP.NET Core mediante Yeoman
* Creazione di un ambiente di sviluppo Docker
* Creazione di un'immagine Docker basata su un'immagine esistente
* Distribuzione del servizio in un ambiente Docker

Verranno inoltre illustrate alcune funzionalità del linguaggio C#:

* Conversione di oggetti C# in payload JSON
* Creazione di oggetti di trasferimento dati non modificabili
* Elaborazione delle richieste HTTP in ingresso e generazione della risposta HTTP
* Uso dei tipi valore nullable

È possibile recuperare il codice dall'[archivio GitHub](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/WeatherMicroservice).

### <a name="why-docker"></a>Vantaggi offerti dall'uso di Docker

Docker semplifica la creazione di immagini delle macchine standard per ospitare i servizi in un data center o nel cloud pubblico. Docker consente di configurare l'immagine e di eseguirne la replica in base alle necessità per scalare l'installazione dell'applicazione.

Tutto il codice riportato in questa esercitazione può essere eseguito in qualsiasi ambiente .NET Core.
Le attività aggiuntive per un'installazione Docker funzioneranno per un'applicazione ASP.NET Core. 

## <a name="prerequisites"></a>Prerequisiti
È necessario configurare il computer per l'esecuzione di .NET Core. Le istruzioni di installazione sono disponibili nella pagina [.NET Core](https://www.microsoft.com/net/core).
Questa applicazione può essere eseguita in Windows, Ubuntu Linux, macOS o in un contenitore Docker. È necessario installare l'editor di codice preferito. Nelle descrizioni seguenti viene usato [Visual Studio Code](https://code.visualstudio.com/), un editor open source multipiattaforma, ma è possibile usare gli strumenti con cui si ha maggiore familiarità.

È inoltre necessario installare il motore di Docker. Per le istruzioni di installazione relative alla piattaforma in uso, vedere la pagina [Docker Installation](http://www.docker.com/products/docker) (Installazione di Docker).
È possibile installare Docker in diverse distribuzioni di Linux, macOS o Windows. La pagina citata sopra contiene sezioni per ciascuna delle installazioni disponibili.

La maggior parte dei componenti da installare viene eseguita da uno strumento di gestione pacchetti. Se è già installato lo strumento di gestione pacchetti `npm` di Node.js, ignorare questo passaggio. In caso contrario, installare la versione più recente di Node.js, scaricabile da [nodejs.org](https://nodejs.org), che installerà lo strumento di gestione pacchetti npm. 

A questo punto è necessario installare alcuni strumenti da riga di comando che supportano lo sviluppo di ASP.NET Core. I modelli di riga di comando usano Yeoman, Bower, Grunt e Gulp. Se tali strumenti sono già installati, è positivo. In caso contrario, digitare quanto segue nella shell preferita:

`npm install -g yo bower grunt-cli gulp`

L'opzione `-g` indica che si tratta di un'installazione globale e che gli strumenti sono disponibili nell'intero sistema. Un'installazione locale limita l'ambito del pacchetto a un singolo progetto. Dopo avere installato gli strumenti di base, è necessario installare i generatori di modelli yeoman ASP.NET:

`npm install -g generator-aspnet`

## <a name="create-the-application"></a>Creare l'applicazione

Dopo avere installato tutti gli strumenti, creare una nuova applicazione ASP.NET Core. Per usare il generatore da riga di comando, eseguire il comando yeoman seguente nella shell preferita:

`yo aspnet`

Questo comando richiede di selezionare il tipo di applicazione che si vuole creare. Per questo microservizio, è consigliabile selezionare l'applicazione Web più semplice e leggera possibile. A questo scopo, selezionare Applicazione Web ASP.NET vuota. Il modello richiederà di specificare un nome. Selezionare WeatherMicroservice. 

Il modello crea automaticamente otto file:

* Un file con estensione gitignore, personalizzato per le applicazioni ASP.NET Core.
* Un file Startup.cs, contenente la base dell'applicazione.
* Un file Program.cs, contenente il punto di ingresso dell'applicazione.
* Un file WeatherMicroservice.csproj, ovvero il file di compilazione dell'applicazione.
* Un file Docker. Questo script crea un'immagine Docker per l'applicazione.
* Un file README.md, contenente collegamenti ad altre risorse ASP.NET Core.
* Un file web.config, contenente informazioni di configurazione di base.
* Un file runtimeconfig.template.json, contenente le impostazioni di debug degli IDE.

È ora possibile eseguire l'applicazione generata dal modello. A questo scopo è possibile usare una serie di strumenti da riga di comando. Il comando `dotnet` esegue gli strumenti necessari per lo sviluppo di .NET. Ogni verbo esegue un comando differente

Il primo passaggio riguarda il ripristino di tutte le dipendenze:

```console
dotnet restore
```

Il comando dotnet restore usa lo strumento di gestione pacchetti di NuGet per installare tutti i pacchetti necessari nella directory dell'applicazione. Genera inoltre un file project.json.lock. Questo file contiene informazioni su ciascun pacchetto a cui si fa riferimento. Dopo aver ripristinato tutte le dipendenze, compilare l'applicazione:

```console
dotnet build
```

Dopo aver compilato l'applicazione, eseguirla dalla riga di comando:

```console
dotnet run
```

La configurazione predefinita è in ascolto su http://localhost:5000. È possibile aprire un browser e passare a tale pagina, dove viene visualizzato un messaggio "Hello World!" .

### <a name="anatomy-of-an-aspnet-core-application"></a>Composizione di un'applicazione ASP.NET Core

Dopo aver compilato l'applicazione, è ora opportuno analizzare il modo in cui questa funzionalità viene implementata. A questo punto risultano particolarmente interessanti due dei file generati: project.json e Startup.cs. 

Project.json contiene informazioni sul progetto. I due nodi che verranno usati di frequente sono 'dependencies' e 'frameworks'. Nel nodo 'dependencies' sono elencati tutti i pacchetti necessari per l'applicazione.
Al momento, poiché sono necessario soltanto i pacchetti che eseguono un server Web, si tratta di un nodo di piccole dimensioni.

Il nodo 'frameworks' specifica le versioni e le configurazioni del framework .NET che eseguirà l'applicazione.

L'applicazione viene implementata nel file Startup.cs, contenente la classe startup.

I due metodi vengono chiamati dall'infrastruttura ASP.NET Core per configurare ed eseguire l'applicazione. Il metodo `ConfigureServices` descrive i servizi necessari per l'applicazione. Poiché si sta creando un microservizio semplificato, non è necessario configurare alcuna dipendenza. Il metodo `Configure` consente di configurare i gestori per le richieste HTTP in ingresso. Il modello genera un semplice gestore che risponde a qualsiasi richiesta con il testo "Hello World!".

## <a name="build-a-microservice"></a>Creare un microservizio

Il servizio che si intende creare distribuirà report meteo da qualsiasi località. In un ambiente di produzione, per recuperare i dati meteo sarebbe necessario chiamare un qualche servizio. Ai fini di questo esempio, verrà generata una previsione meteo casuale. 

Per implementare il servizio meteo casuale, è necessario eseguire diverse attività:

* Analizzare la richiesta in ingresso per leggere la latitudine e la longitudine.
* Generare alcuni dati di previsione casuali.
* Convertire i dati di previsione casuali da oggetti C# in pacchetti JSON.
* Impostare l'intestazione della risposta per indicare che il servizio reinvia JSON.
* Scrivere la risposta.

Ciascuno di questi passaggi è descritto nelle sezioni seguenti.

### <a name="parsing-the-query-string"></a>Analizzare la stringa di query

Per iniziare, viene eseguita l'analisi della stringa di query. Nella stringa di query il servizio accetterà argomenti 'lat' e 'long' nel formato seguente:

`http://localhost:5000/?lat=-35.55&long=-12.35`  

Tutte le modifiche che è necessario apportare sono presenti nell'espressione lambda definita come argomento per `app.Run` nella classe startup.

L'argomento presente nell'espressione lambda è l'`HttpContext` della richiesta. Una delle sue proprietà è l'oggetto `Request`. L'oggetto `Request` ha una proprietà `Query` contenente un dizionario di tutti i valori presenti nella stringa di query per la richiesta. La prima operazione consiste nell'individuare i valori relativi alla latitudine e alla longitudine:

[!code-csharp[ReadQueryString](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#ReadQueryString "leggere le variabili dalla stringa di query")]

Il valori del dizionario Query sono di tipo `StringValue`. Questo tipo può contenere una raccolta di stringhe. Ai fini di questo servizio meteo, ogni valore è una singola stringa. Per questo motivo nel codice sopra riportato è presente una chiamata a `FirstOrDefault()`. 

Come passaggio successivo, è necessario convertire le stringhe in valori double. Per convertire una stringa in un valore double verrà usato il metodo `double.TryParse()`:

```cs
bool TryParse(string s, out double result);
```

Questo metodo utilizza parametri C# per indicare se la stringa di input può essere convertita in un valore double. Se la stringa costituisce una rappresentazione valida per un valore double, il metodo restituisce true e l'argomento `result` contiene il valore. Se la stringa non rappresenta un valore double valido, il metodo restituisce false.

È possibile adattare tale API mediante l'uso di un *metodo di estensione* che restituisce un *valore double nullable*. Un *tipo valore nullable* rappresenta alcuni tipi valore e può includere anche un valore mancante o null. Per rappresentare un tipo nullable, aggiungere il carattere `?` alla dichiarazione del tipo. 

I metodi di estensione sono definiti come metodi statici. Se tuttavia si aggiunge il modificatore `this` al primo parametro di tali metodi, è possibile chiamarli come se fossero membri della classe. I metodi di estensione possono essere definiti soltanto in classi statiche. Di seguito è riportata la definizione della classe contenente il metodo di estensione per l'analisi:

[!code-csharp[TryParseExtension](../../../samples/csharp/getting-started/WeatherMicroservice/Extensions.cs#TryParseExtension "Tentare l'analisi per un valore nullable")]

L'espressione `default(double?)` restituisce il valore predefinito per il tipo `double?`. Il valore predefinito è il valore null (o mancante).

È possibile usare questo metodo di estensione per convertire gli argomenti della stringa di query in un tipo double:

[!code-csharp[UseTryParse](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#UseTryParse "Usare il metodo di estensione TryParse")]

Per testare facilmente il codice di analisi, aggiornare la risposta in modo che includa i valori degli argomenti seguenti:

[!code-csharp[WriteResponse](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#WriteResponse "Scrivere la risposta di output")]

A questo punto, è possibile eseguire l'applicazione Web e verificare se il codice di analisi funziona correttamente. Aggiungere valori alla richiesta Web in un browser. Verranno visualizzati i risultati aggiornati.

### <a name="build-a-random-weather-forecast"></a>Creare una previsione meteo casuale

L'attività successiva consiste nella creazione di una previsione meteo casuale. Come prima operazione, creare un contenitore dati in cui siano presenti i valori necessari per una previsione meteo:

```cs
public class WeatherReport
{
    private static readonly string[] PossibleConditions = new string[]
    {
        "Sunny",
        "Mostly Sunny",
        "Partly Sunny",
        "Partly Cloudy",
        "Mostly Cloudy",
        "Rain"
    };

    public int HiTemperature { get; }
    public int LoTemperature { get; }
    public int AverageWindSpeed { get; }
    public string Conditions { get; }
}
```

Come passaggio successivo, aggiungere un costruttore che imposti tali valori in modo casuale. Il costruttore usa i valori relativi a latitudine e longitudine per inizializzare il generatore di numeri Random. Questo significa che la previsione per la stessa località è la stessa. Se si modificano gli argomenti relativi alla latitudine e alla longitudine, si otterrà una previsione diversa, poiché si parte con un valore di inizializzazione differente.

[!code-csharp[WeatherReportConstructor](../../../samples/csharp/getting-started/WeatherMicroservice/WeatherReport.cs#WeatherReportConstructor "Costruttore report meteo")]

Nel metodo di risposta è ora possibile generare una previsione a 5 giorni:

[!code-csharp[GenerateRandomReport](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#GenerateRandomReport "Generare un report meteo casuale")]

### <a name="build-the-json-response"></a>Generare la risposta JSON

L'attività finale del codice sul server consiste nel convertire la matrice WeatherReport in un pacchetto JSON e di rinviarlo al client. Come prima operazione, creare il pacchetto JSON. All'elenco delle dipendenze verrà aggiunto il serializzatore NewtonSoft JSON. È possibile eseguire questa operazione usando l'interfaccia della riga di comando di `dotnet`:

```
dotnet add package Newtonsoft.Json
```

È quindi possibile usare la classe `JsonConvert` per scrivere l'oggetto in una stringa:

[!code-csharp[ConvertToJson](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#ConvertToJSON "Convertire gli oggetti in JSON")]

Il codice sopra riportato converte l'oggetto forecast (un elenco di oggetti `WeatherForecast`) in un pacchetto JSON. Dopo aver costruito il pacchetto di risposta, impostare il tipo di contenuto su `application/json` e scrivere la stringa.

L'applicazione viene eseguita e restituisce previsioni casuali.

## <a name="build-a-docker-image"></a>Creare un'immagine Docker

L'attività finale consiste nell'esecuzione dell'applicazione in Docker. Verrà creato un contenitore Docker per eseguire un'immagine Docker che rappresenta l'applicazione.

Un'***immagine Docker*** è un file che definisce l'ambiente per l'esecuzione dell'applicazione.

Un ***contenitore Docker*** rappresenta un'istanza in esecuzione di un'immagine Docker.

Per analogia, è possibile assimilare l'*immagine Docker* a una *classe* e il *contenitore Docker* a un oggetto o a un'istanza di tale classe.  

Ai fini di questa esercitazione, verrà usato il file Docker creato dal modello di ASP.NET. Di seguito viene descritto il contenuto di tale file.

La prima riga specifica l'immagine di origine:

```
FROM microsoft/dotnet:1.1-sdk-msbuild
```

Docker consente di configurare un'immagine del computer basata su un modello di origine. Questo significa che, per iniziare, non è necessario specificare tutti i parametri del computer, ma soltanto le eventuali modifiche. Tali modifiche dovranno includere l'applicazione.

Nel primo esempio verrà usata la versione `1.1-sdk-msbuild` dell'immagine dotnet. Questo è il modo più semplice per creare un ambiente Docker funzionante. L'immagine include il runtime principale di dotnet e dotnet SDK. Questo semplifica le operazioni iniziali e la compilazione, ma crea un'immagine di maggiori dimensioni.

Le cinque righe successive consentono di installare e compilare l'applicazione:

```
WORKDIR /app

# copy csproj and restore as distinct layers

COPY WeatherMicroservice.csproj .
RUN dotnet restore

# copy and build everything else

COPY . .

# RUN dotnet restore
RUN dotnet publish -c Release -o out
```

Il codice sopra riportato copia il file di progetto dalla directory corrente alla macchina virtuale Docker e ripristina tutti i pacchetti. Se si usa l'interfaccia della riga di comando, l'immagine Docker deve includere .NET Core SDK. In seguito la rimanente parte dell'applicazione viene copiata e il comando publish di dotnet compila l'applicazione e ne crea un pacchetto.

L'ultima riga del file esegue l'applicazione:

```
ENTRYPOINT ["dotnet", "out/WeatherMicroservice.dll", "--server.urls", "http://0.0.0.0:5000"]
```

Viene fatto riferimento a questa porta configurata nell'ultima riga del file Docker, nell'argomento `--server.urls` di `dotnet`. Il comando `ENTRYPOINT` comunica a Docker quale comando e quali opzioni della riga di comando avviano il servizio. 

## <a name="building-and-running-the-image-in-a-container"></a>Compilare ed eseguire l'immagine in un contenitore

In questa sezione si eseguirà la compilazione di un'immagine e l'esecuzione di un servizio all'interno di un contenitore Docker. Non si vuole che tutti i file della directory locale vengano copiati nell'immagine. L'applicazione verrà invece compilata nel contenitore. Verrà creato un file `.dockerignore` per specificare le directory non copiate nell'immagine. Si vuole che non venga copiata alcuna risorsa di compilazione. Specificare le directory di compilazione e pubblicazione nel file `.dockerignore`:

```
bin/*
obj/*
out/*
```

L'immagine viene compilata usando il comando build di Docker. Eseguire il comando seguente dalla directory contenente il codice.

```console
docker build -t weather-microservice .
```

Questo comando compila l'immagine del contenitore sulla base di tutte le informazioni presenti nel file Docker. L'argomento `-t` specifica un tag, o un nome, per questa immagine del contenitore. Nella riga di comando precedente il tag usato per il contenitore Docker è `weather-microservice`. Dopo l'esecuzione di questo comando, è disponibile un contenitore pronto per l'esecuzione del nuovo servizio. 

> [!Note]
> Il comando copy copierà tutte le risorse compilate, nonché l'origine dell'applicazione.
> Prima di compilare l'immagine Docker, rimuovere le directory `obj`, `bin` e `out` dal computer locale.

Eseguire il comando seguente per avviare il contenitore e il servizio:

```console
docker run -d -p 80:5000 --name hello-docker weather-microservice
```

L'opzione `-d` consente di eseguire il contenitore scollegato dal terminale corrente. Questo significa che nel terminale non verrà visualizzato l'output del comando. L'opzione `-p` indica il mapping delle porte tra il servizio e l'host. In base al codice sopra riportato, qualsiasi richiesta in ingresso sulla porta 80 verrà inoltrata alla porta 5000 del contenitore. La porta 5000 è la porta su cui è in ascolto il servizio secondo gli argomenti della riga di comando specificati nel file Docker sopra riportato. L'argomento `--name` indica il nome del contenitore in esecuzione. È un nome appropriato, che è possibile specificare per usare il contenitore. 

Per vedere se l'immagine è in esecuzione, usare il comando seguente:

```console
docker ps
```

Se il contenitore è in esecuzione, viene visualizzata una riga in cui sono elencati i processi in esecuzione. Questa riga potrebbe essere l'unica.

Per testare il servizio, è possibile aprire un browser, passare a localhost e specificare valori per la latitudine e la longitudine:

```
http://localhost/?lat=35.5&long=40.75
```

## <a name="attaching-to-a-running-container"></a>Collegarsi a un contenitore in esecuzione

Quando si esegue il servizio in una finestra di comando, è possibile osservare le informazioni di diagnostica stampate per ogni richiesta. Quando il contenitore è in esecuzione senza collegamento, tali informazioni non vengono visualizzate. Il comando attach di Docker consente di collegarsi a un contenitore in esecuzione in modo da visualizzare le informazioni di log.  Eseguire questo comando da una finestra di comando:

```console
docker attach --sig-proxy=false hello-docker
```

L'argomento `--sig-proxy=false` indica che i comandi `Ctrl-C` non vengono inviati al processo del contenitore, ma che arrestano il comando `docker attach`. L'argomento finale è il nome assegnato al contenitore nel comando `docker run`. 

> [!NOTE]
> È anche possibile usare l'ID del contenitore assegnato da Docker per fare riferimento a qualsiasi altro contenitore. Se in `docker run` non è stato specificato un nome per il contenitore, è necessario usare l'ID del contenitore.

Aprire un browser e passare al servizio. Nelle finestre di comando verranno visualizzati messaggi di diagnostica provenienti dal contenitore collegato in esecuzione.

Premere `Ctrl-C` per arrestare il processo di collegamento.

Quando si è finito di usare il contenitore, è possibile arrestarlo:

```console
docker stop hello-docker
```

Il contenitore e l'immagine sono ancora disponibili per il riavvio.  Per rimuovere il contenitore dal computer, usare il comando seguente:

```console
docker rm hello-docker
```

Per rimuovere dal computer le immagini non utilizzate, usare il comando seguente:

```console
docker rmi hello-docker
```

## <a name="conclusion"></a>Conclusione 

In questa esercitazione è stato creato un microservizio ASP.NET Core e sono state aggiunte alcune semplici funzionalità.

È stata compilata un'immagine Docker del contenitore e quest'ultimo è stato eseguito sul computer. È stata collegata una finestra del terminale al servizio e sono stati visualizzati i messaggi di diagnostica provenienti dal servizio stesso.

Nel corso dell'esercitazione è stato possibile osservare diverse funzionalità del linguaggio C# in azione.

