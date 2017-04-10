---
title: Catalogo dei RID (Runtime IDentifier) di .NET Core
description: Catalogo dei RID (Runtime IDentifier) di .NET Core
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 08/22/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: b2032f5d-771f-48d9-917c-587d9509035c
translationtype: Human Translation
ms.sourcegitcommit: 811b9539019b7cc2817b5742760ae52fbc2f95dd
ms.openlocfilehash: fc59a9f3333f01caf9622dd500a5de6e2ae5132b
ms.lasthandoff: 03/02/2017

---

# <a name="net-core-runtime-identifier-rid-catalog"></a>Catalogo dei RID (Runtime IDentifier) di .NET Core

## <a name="what-are-rids"></a>Caratteristiche dei RID
RID è l'acronimo di *Runtime IDentifier*. I RID vengono usati per identificare i sistemi operativi di destinazione in cui verrà eseguita un'applicazione o una risorsa, ad esempio un assembly. I RID hanno l'aspetto seguente: "ubuntu.14.04-x64", "win7-x64", "osx.10.11-x64". Per i pacchetti con dipendenze native, il RID specifica le piattaforme su cui verrà ripristinato il pacchetto. 

È importante sottolineare che i RID sono stringhe molto opache. Questo significa che, per funzionare, devono corrispondere esattamente alle operazioni che li usano. Si consideri ad esempio il caso di [Elementary OS](https://elementary.io/), che è un clone diretto di Ubuntu 14.04. Anche se .NET Core e l'interfaccia della riga di comando funzionano correttamente in questa versione di Ubuntu, se si tenta di usarli in Elementary OS senza alcuna modifica, il ripristino di un qualsiasi pacchetto avrà esito negativo. Questo problema si verifica perché attualmente non è disponibile un RID che designi Elementary OS come piattaforma. 

I RID che rappresentano un sistema operativo reale seguono in genere il modello seguente: `[os].[version]-[arch]` dove:
- `[os]` è il sistema operativo moniker, ad esempio `ubuntu`.
- `[version]` è la versione del sistema operativo indicata da un numero separato da punti (`.`), ad esempio `15.10`, e sufficientemente accurata da consentire ragionevolmente alle risorse di avere come destinazione le API della piattaforma del sistema operativo rappresentate dalla versione in oggetto.
  - **Non deve** trattarsi di versioni di marketing, poiché tali versioni rappresentano spesso più versioni discrete del sistema operativo con una superficie di attacco delle API della piattaforma differente.
- `[arch]` è l'architettura del processore, ad esempio `x86`, `x64`, `arm`, `arm64` e così via.

Il grafico RID viene definito in un pacchetto denominato `Microsoft.NETCore.Platforms` in un file denominato `runtime.json`, che è possibile vedere l'[archivio CoreFX](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json). Se si usa questo file, si noterà che alcuni dei RID contengono un'istruzione `"#import"`. Si tratta di istruzioni di compatibilità. Questo significa che un RID contenente un RID importato può rappresentare una destinazione per il ripristino di pacchetti per tale RID. L'affermazione precedente è poco chiara. Per questo motivo, di seguito è riportato un esempio riguardante MacOS:

```json
"osx.10.11-x64": {
    "#import": [ "osx.10.11", "osx.10.10-x64" ]
}
```
Il RID sopra riportato specifica che `osx.10.11-x64` importa `osx.10.10-x64`. Questo significa che, durante il ripristino di pacchetti, NuGet sarà in grado di ripristinare quelli che specificano di richiedere `osx.10.10-x64` su `osx.10.11-x64`.

Di seguito è riportato un grafico RID di esempio di dimensioni leggermente maggiori:  

- `win10-arm`
  - `win10`
  - `win81-arm`
    - `win81`
    - `win8-arm`
      - `win8`
        - `win7`
          - `win`
            - `any`

Tutti i RID finiscono per mappare nuovamente al RID `any` radice.

Anche se i RID sembrano semplici da usare, è necessario tenere presenti alcuni aspetti importanti:

* Sono **stringhe opache** e devono essere trattati come black box
    * Non si devono creare RID a livello di codice
* È necessario usare i RID già definiti nella piattaforma in uso, come mostrato in questo documento
* Non è necessario che i RID siano specifici, motivo per cui non bisogna presupporre nulla in base al valore effettivo del RID. Consultare questo documento per stabilire quali RID sono necessari per una determinata piattaforma

## <a name="using-rids"></a>Uso dei RID
Per usare i RID, è necessario sapere quali sono quelli disponibili. Alla piattaforma vengono regolarmente aggiunti nuovi RID. Per la versione più recente, verificare il file [runtime.json](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json) nell'archivio CoreFX.

> [!NOTE]
> Microsoft sta lavorando per rendere disponibili queste informazioni in forma più interattiva. Quando tale risultato sarà raggiunto, questa pagina verrà aggiornata in modo da puntare allo strumento in questione e/o alla documentazione sull'utilizzo dello stesso. 

## <a name="windows-rids"></a>RID Windows

* Windows 7/Windows Server 2008 R2
    * `win7-x64`
    * `win7-x86`
* Windows 8/Windows Server 2012
    * `win8-x64`
    * `win8-x86`
    * `win8-arm`
* Windows 8.1/Windows Server 2012 R2
    * `win81-x64`
    * `win81-x86`
    * `win81-arm`
* Windows 10/Windows Server 2016
    * `win10-x64`
    * `win10-x86`
    * `win10-arm`
    * `win10-arm64`

## <a name="linux-rids"></a>RID Linux

* Red Hat Enterprise Linux
    * `rhel.7-x64`
* Ubuntu
    * `ubuntu.14.04-x64`
    * `ubuntu.14.10-x64`
    * `ubuntu.15.04-x64`
    * `ubuntu.15.10-x64`
    * `ubuntu.16.04-x64`
    * `ubuntu.16.10-x64`
* CentOS
    * `centos.7-x64`
* Debian
    * `debian.8-x64`
* Fedora
    * `fedora.23-x64`
    * `fedora.24-x64`
* OpenSUSE
    * `opensuse.13.2-x64`
    * `opensuse.42.1-x64`
* Oracle Linux
    * `ol.7-x64`
    * `ol.7.0-x64`
    * `ol.7.1-x64`
    * `ol.7.2-x64`
* Derivati Ubuntu attualmente supportati 
    * `linuxmint.17-x64`
    * `linuxmint.17.1-x64`
    * `linuxmint.17.2-x64`
    * `linuxmint.17.3-x64`
    * `linuxmint.18-x64`

## <a name="os-x-rids"></a>RID OS X

* `osx.10.10-x64`
* `osx.10.11-x64`
* `osx.10.12-x64`

