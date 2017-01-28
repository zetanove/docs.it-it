---
title: Versionamento di .NET Core
description: Versionamento di .NET Core
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: f6f684b1-1d2c-4105-8376-7c1959e23803
translationtype: Human Translation
ms.sourcegitcommit: bb15293c569fa92f1acf6315c5fe7f2cd9cb6f68
ms.openlocfilehash: 1f4f580a8287f371ff5cdc37b78e73b7329dca02

---

# <a name="net-core-versioning"></a>Versionamento di .NET Core

.NET Core è una piattaforma di framework e [pacchetti NuGet](../packages.md) ed è distribuito come unità. È possibile definire una versione separata per ciascuno di questi livelli di piattaforma per assicurare flessibilità al prodotto e descrivere in modo accurato le modifiche apportate a quest'ultimo. Anche se esiste una notevole flessibilità nel versionamento, è tuttavia presente la tendenza a definire una versione della piattaforma come unità per rendere il prodotto più facile da comprendere.

Il prodotto è per certi versi univoco, dal momento che viene descritto e fornito sotto forma di pacchetti da un sistema di gestione pacchetti (NuGet). Anche se in genere si acquisisce .NET Core come SDK autonomo, quest'ultimo è prevalentemente un'esperienza utile sui pacchetti NuGet e di conseguenza non è distinto dai pacchetti stessi. Come risultato, la definizione delle versioni avviene innanzitutto e principalmente in termini di pacchetti. Altre esperienze di versionamento sono successive e conseguenti a questa prima definizione.

## <a name="semantic-versioning"></a>Versionamento Semantico

.NET Core usa [Versionamento Semantico (SemVer)](http://semver.org/), adottando la convenzione "major.minor.patch" e usando le diverse parti del numero di versione per descrivere il grado e il tipo di modifica.

A .NET Core viene in genere applicato il modello di versionamento seguente. Esistono casi in cui questo modello è stato adattato in base alle versioni esistenti. Tali casi vengono descritti più avanti in questo documento. I framework, ad esempio, hanno lo scopo di rappresentare la piattaforma e le funzionalità dell'API, in conformità alla definizione della versione major/minor.

### <a name="versioning-form"></a>Forma del versionamento

MAJOR.MINOR.PATCH[-PRERELEASE-BUILDNUMBER]

### <a name="decision-tree"></a>Albero delle decisioni

MAJOR nei casi seguenti:
  - Viene eliminato il supporto per una piattaforma
  - Viene adottata una versione MAJOR più recente di una dipendenza esistente 
  - Per impostazione predefinita, viene disabilitato un dettaglio di compatibilità

MINOR nei casi seguenti:
  - Viene aggiunta la superficie di attacco dell'API pubblica 
  - Viene aggiunto un nuovo comportamento
  - Viene adottata una versione MINOR più recente di una dipendenza esistente
  - Viene introdotta una nuova dipendenza 
  
PATCH nei casi seguenti:
  - Vengono eseguite correzioni dei bug
  - Viene aggiunto il supporto per una piattaforma più recente
  - Viene adottata una versione PATCH più recente di una dipendenza esistente
  - Viene apportata una qualsiasi altra modifica (non acquisita in altro modo)

Quando si stabiliscono gli elementi da incrementare nel caso in cui siano presenti più modifiche, scegliere il tipo di modifica più elevato.

## <a name="versioning-scheme"></a>Schema di versionamento

Di seguito sono descritti la definizione e il versionamento di .NET Core:

- Implementazione di runtime e framework distribuita sotto forma di pacchetti. La definizione delle versioni avviene in modo indipendente per ciascun pacchetto, in particolare per quanto riguarda le versioni patch.
- Set di metapacchetti che fa riferimento a pacchetti con granularità fine come unità di cui vengono definite diverse versioni. Le versioni dei metapacchetti vengono definite separatamente da quelle dei pacchetti.
- Set di framework, ad esempio `netstandard`, che rappresenta un set di API di dimensioni progressivamente maggiori, descritto in un set di snapshot di cui vengono definite diverse versioni.

### <a name="packages"></a>Pacchetti

I pacchetti di libreria hanno un'evoluzione indipendente e anche le relative versioni vengono definite in modo separato. I pacchetti che si sovrappongono ad assembly .NET Framework System\* usano in genere versioni 4.x, in linea con il versionamento di .NET Framework 4.x. Si tratta di una scelta storica. I pacchetti che non si sovrappongono a librerie di .NET Framework, ad esempio [System.Reflection.Metadata](https://www.nuget.org/packages/System.Reflection.Metadata), partono in genere da 1.0 e incrementano da quest'ultimo il numero di versione.

I pacchetti descritti dalla [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) vengono trattati in modo speciale in quanto costituiscono la base della piattaforma.

- Le versioni dei pacchetti della NETStandard.Library verranno definite sotto forma di set, dal momento che tra tali pacchetti sono presenti dipendenze a livello di implementazione.
- Le API verranno aggiunte ai pacchetti della NETStandard.Library come parti di versioni .NET Core principali o secondarie: tale operazione, infatti, richiederebbe l'aggiunta di una nuova versione `netstandard`. Quanto affermato sopra si aggiunge ai requisiti di SemVer.

### <a name="metapackages"></a>Metapacchetti

Il versionamento dei metapacchetti .NET Core è basato sul framework a cui tali metapacchetti vengono mappati. I metapacchetti adottano il numero di versione più alto, ad esempio netstandard1.6, del framework a cui vengono mappati nella chiusura pacchetto. 

La versione patch del metapacchetto viene usata per rappresentare gli aggiornamenti del metapacchetto stesso per fare riferimento a pacchetti aggiornati. Le versioni patch non includeranno mai una versione aggiornata del framework. Di conseguenza, i metapacchetti non sono strettamente conformi a SemVer perché il loro schema di versionamento non rappresenta il grado di cambiamento nei pacchetti sottostanti, ma principalmente il livello API. 

Per .NET Core sono presenti due metapacchetti principali.

**NETStandard.Library**

- Versione 1.6 a partire da .NET Core 1.0 (queste versioni non corrispondono né tipicamente né intenzionalmente).
- Viene mappato al framework `netstandard`. 
- Descrive i pacchetti considerati necessari per lo sviluppo di app moderne e che le piattaforme .NET devono implementare per essere considerate piattaforme [.NET Standard](../../standard/library.md).

**Microsoft.NETCore.App**

- Versione 1.0 a partire da .NET Core 1.0 (queste versioni corrispondono).
- Viene mappato al framework `netcoreapp`.
- Descrive i pacchetti presenti nella distribuzione .NET Core.

Nota: [`Microsoft.NETCore.Portable.Compatibility`](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) è un altro metapacchetto .NET. Non viene mappato a un framework particolare, motivo per cui le relative versioni vengono definite come quelle di un pacchetto.

### <a name="frameworks"></a>Framework

Le versioni del framework vengono aggiornate quando si aggiungono nuove API. Non includono alcun concetto della versione patch, poiché rappresentano la forma dell'API e non problemi di implementazione. La definizione delle versioni major e minor seguirà le regole SemVer specificate in precedenza.

Il framework `netcoreapp` è legato alla distribuzione di .NET Core e seguirà il numero di versione usato da quest'ultimo. Ad esempio, quando viene rilasciata la versione .NET Core 2.0, avrà come destinazione `netcoreapp2.0`. Il framework `netstandard` non corrisponderà allo schema di versionamento di alcun runtime .NET, poiché è ugualmente applicabile a tutti questi runtime.

## <a name="versioning-in-practice"></a>Versionamento in pratica

Ogni giorno in GitHub vengono inseriti commit e PR nei repository relativi a .NET Core, con la conseguente generazione di nuove build di diverse librerie. Non è pratico creare nuove versioni pubbliche di .NET Core per ogni modifica. Le modifiche vengono invece aggregate nel corso di un determinato periodo di tempo, ad esempio mesi o settimane, prima di creare una nuova versione pubblica stabile di .NET Core.

Una nuova versione di .NET Core può implicare quanto segue:

- Nuove versioni dei pacchetti e dei metapacchetti.
- Nuove versioni di diversi framework, presupponendo l'aggiunta di nuove API.
- Nuova versione della distribuzione .NET Core.

### <a name="shipping-a-patch-release"></a>Rilascio di una versione patch

Dopo il rilascio di una versione .NET Core 1.0.0 stabile, alle librerie .NET Core vengono apportate modifiche a livello di patch (senza l'aggiunta di nuove API) per correggere i bug e migliorare le prestazioni e l'affidabilità. I diversi metapacchetti vengono aggiornati in modo che facciano riferimento ai pacchetti della libreria .NET Core aggiornati. Le versioni dei metapacchetti vengono definite come aggiornamenti patch (x.y.z). I framework non vengono aggiornati. Viene rilasciata una nuova distribuzione di .NET Core con un numero di versione corrispondente al metapacchetto `Microsoft.NETCore.App`.

Gli esempi di file project.json riportati di seguito mostrano gli aggiornamenti della versione patch.

```
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.1"
  },
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

### <a name="shipping-a-minor-release"></a>Rilascio di una versione secondaria

Dopo il rilascio di una versione .NET Core 1.0.0 stabile, alle librerie .NET Core vengono aggiunte nuove API per abilitare nuovi scenari. I diversi metapacchetti vengono aggiornati in modo che facciano riferimento ai pacchetti della libreria .NET Core aggiornati. Le versioni dei metapacchetti vengono definite come aggiornamenti patch (x.y), in modo che corrispondano alla versione più recente del framework. I diversi framework vengono aggiornati per descrivere le nuove API. Viene rilasciata una nuova distribuzione di .NET Core con un numero di versione corrispondente al metapacchetto `Microsoft.NETCore.App`.

Gli esempi di file project.json riportati di seguito mostrano gli aggiornamenti della versione secondaria.

```
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.1.0"
  },
  "frameworks": {
    "netcoreapp1.1": {}
  }
}
```

### <a name="shipping-a-major-release"></a>Rilascio di una versione principale

Data una versione .NET Core 1.0.0 stabile, alle librerie .NET Core vengono aggiunte nuove API per abilitare nuovi scenari per tale versione principale. È possibile che venga eliminato il supporto per una piattaforma. I diversi metapacchetti vengono aggiornati in modo che facciano riferimento ai pacchetti della libreria .NET Core aggiornati. Le versioni dei metapacchetti `Microsoft.NETCore.App` e del framework `netcore` vengono definite come aggiornamento principale (x.). È possibile che le versioni del metapacchetto `NETStandard.Library` vengano definite come aggiornamento secondario (x.y) perché tale metapacchetto si applica a più implementazioni .NET. Verrà rilasciata una nuova distribuzione .NET Core con un numero di versione corrispondente al metapacchetto `Microsoft.NETCore.App`.

Il riferimento al metapacchetto project.json riportato nell'esempio seguente mostra gli aggiornamenti della versione principale.

```
{
  "dependencies": {
    "Microsoft.NETCore.App": "2.0.0"
  },
  "frameworks": {
    "netcoreapp2.0": {}
  }
}
```



<!--HONumber=Nov16_HO3-->


