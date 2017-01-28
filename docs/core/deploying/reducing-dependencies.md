---
title: Riduzione delle dipendenze dei pacchetti con project.json
description: Riduzione delle dipendenze dei pacchetti con project.json
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 916251e3-87f9-4eee-81ec-94076215e6fa
translationtype: Human Translation
ms.sourcegitcommit: 62fdb3e60b206728d86220076867eb8fd68af82e
ms.openlocfilehash: 77d49a1df361823c3f8f676923960d4bef2eeb08

---

# <a name="reducing-package-dependencies-with-projectjson"></a>Riduzione delle dipendenze dei pacchetti con project.json

Questo articolo descrive cosa è necessario conoscere sulla riduzione delle dipendenze dei pacchetti durante la creazione di librerie `project.json`. Al termine dell'articolo, si apprenderà come creare la libreria in modo che usi solo le dipendenze necessarie. 

## <a name="why-its-important"></a>Perché è importante?

.NET Core è un prodotto costituito da pacchetti NuGet.  Un pacchetto fondamentale è il [metapacchetto della libreria .NET Standard](https://www.nuget.org/packages/NETStandard.Library), che è un pacchetto NuGet composto da altri pacchetti.  Fornisce il set di pacchetti in grado di funzionare su più implementazioni di .NET, ad esempio .NET Framework, .NET Core e Xamarin/Mono.

È tuttavia probabile che la libreria non usi tutti i pacchetti che contiene.  Quando si crea una libreria e la si distribuisce tramite NuGet, è opportuno ridurre il numero delle dipendenze ai soli pacchetti che vengono effettivamente usati.  In questo modo, si otterrà un impatto minore per i pacchetti NuGet.

## <a name="how-to-do-it"></a>Come procedere?

Attualmente non è disponibile un comando `dotnet` ufficiale che consenta di ridurre il numero di riferimenti nel pacchetto.  È tuttavia possibile eseguire questa operazione manualmente.  Il processo generale è simile al seguente:

1. Fare riferimento a `NETStandard.Library` versione `1.6.0` in una sezione `dependencies` di `project.json`.
2. Ripristinare i pacchetti con `dotnet restore` dalla riga di comando.
3. Esaminare il file `project.lock.json` e trovare la sezione `NETSTandard.Library`  in genere all'inizio del file.
4. Copiare tutti i pacchetti elencati in `dependencies`.
5. Rimuovere il riferimento `.NETStandard.Library` e sostituirlo con i pacchetti copiati.
6. Rimuovere i riferimenti ai pacchetti non necessari.

È possibile individuare i pacchetti non necessari in uno dei modi seguenti:

1. Tentativi ed errori.  Questo metodo fa riferimento alla rimozione di un pacchetto, al relativo ripristino, se la libreria continua a eseguire la compilazione, e alla ripetizione del processo.
2. Tramite uno strumento come [ILSpy](http://ilspy.net) o [.NET Reflector](http://www.red-gate.com/products/dotnet-development/reflector) per la selezione dei riferimenti in modo da visualizzare quali vengono effettivamente usati dal codice.  A questo punto, è possibile rimuovere i pacchetti che non corrispondono ai tipi in uso.

## <a name="example"></a>Esempio 

Si supponga di aver scritto una libreria che offre funzionalità aggiuntive per tipi di raccolte generiche.  Tale libreria deve dipendere da pacchetti come `System.Collections`, ma può non dipendere da pacchetti come `System.Net.Http`.  Di conseguenza, può essere opportuno ridurre le dipendenze dei pacchetti alla quantità necessaria per la libreria.

Per ridurre questa libreria, iniziare con il file `project.json` e aggiungere un riferimento a `NETStandard.Library` versione `1.6.0`.

```json
{
    "version":"1.0.0",
    "dependencies":{
        "NETStandard.Library":"1.6.0"
    },
    "frameworks": {
        "netstandard1.0": {}
     }
}
```

Successivamente, si ripristinano i pacchetti con `dotnet restore`, si analizza il file `project.lock.json` e si trovano tutti i pacchetti ripristinati per `NETSTandard.Library`.

Di seguito è presentata la specifica sezione del file `project.lock.json` quando punta a `netstandard1.0`:

```json
"NETStandard.Library/1.6.0":{
    "type": "package",
    "dependencies": {
        "Microsoft.NETCore.Platforms": "1.0.1",
        "Microsoft.NETCore.Runtime": "1.0.2",
        "System.Collections": "4.0.11",
        "System.Diagnostics.Debug": "4.0.11",
        "System.Diagnostics.Tools": "4.0.1",
        "System.Globalization": "4.0.11",
        "System.IO": "4.1.0",
        "System.Linq": "4.1.0",
        "System.Net.Primitives": "4.0.11",
        "System.ObjectModel": "4.0.12",
        "System.Reflection": "4.1.0",
        "System.Reflection.Extensions": "4.0.1",
        "System.Reflection.Primitives": "4.0.1",
        "System.Resources.ResourceManager": "4.0.1",
        "System.Runtime": "4.1.0",
        "System.Runtime.Extensions": "4.1.0",
        "System.Text.Encoding": "4.0.11",
        "System.Text.Encoding.Extensions": "4.0.11",
        "System.Text.RegularExpressions": "4.1.0",
        "System.Threading": "4.0.11",
        "System.Threading.Tasks": "4.0.11",
        "System.Xml.ReaderWriter": "4.0.11",
        "System.Xml.XDocument": "4.0.11"
    }
}
```

Successivamente, sovrascrivere i riferimenti dei pacchetti nella sezione `dependencies` del file della libreria `project.json`, sostituendo il riferimento `NETStandard.Library`:

```json
{
    "version":"1.0.0",
    "dependencies":{
        "Microsoft.NETCore.Platforms": "1.0.1",
        "Microsoft.NETCore.Runtime": "1.0.2",
        "System.Collections": "4.0.11",
        "System.Diagnostics.Debug": "4.0.11",
        "System.Diagnostics.Tools": "4.0.1",
        "System.Globalization": "4.0.11",
        "System.IO": "4.1.0",
        "System.Linq": "4.1.0",
        "System.Net.Primitives": "4.0.11",
        "System.ObjectModel": "4.0.12",
        "System.Reflection": "4.1.0",
        "System.Reflection.Extensions": "4.0.1",
        "System.Reflection.Primitives": "4.0.1",
        "System.Resources.ResourceManager": "4.0.1",
        "System.Runtime": "4.1.0",
        "System.Runtime.Extensions": "4.1.0",
        "System.Text.Encoding": "4.0.11",
        "System.Text.Encoding.Extensions": "4.0.11",
        "System.Text.RegularExpressions": "4.1.0",
        "System.Threading": "4.0.11",
        "System.Threading.Tasks": "4.0.11",
        "System.Xml.ReaderWriter": "4.0.11",
        "System.Xml.XDocument": "4.0.11"
    },
    "frameworks":{
        "netstandard1.0": {}
    }
}
```

Si tratta di numerosi pacchetti, molti dei quali certamente non necessari per l'estensione dei tipi di raccolta.  È possibile rimuovere manualmente i pacchetti o usare uno strumento come [ILSpy](http://ilspy.net) o [.NET Reflector](http://www.red-gate.com/products/dotnet-development/reflector) per identificare i pacchetti effettivamente usati dal codice.

Di seguito un esempio di pacchetto dopo la riduzione delle dipendenze:

```json
{
    "dependencies":{
        "Microsoft.NETCore.Platforms": "1.0.1",
        "Microsoft.NETCore.Runtime": "1.0.2",
        "System.Collections": "4.0.11",
        "System.Linq": "4.1.0",
        "System.Runtime": "4.1.0",
        "System.Runtime.Extensions": "4.1.0",
        "System.Runtime.Handles": "4.0.1",
        "System.Runtime.InteropServices": "4.1.0",
        "System.Runtime.InteropServices.RuntimeInformation": "4.0.0",
        "System.Threading.Tasks": "4.0.11"
    },
    "frameworks":{
        "netstandard1.0": {}
     }
}
```

A questo punto, l'impatto è ridotto rispetto a quello che avrebbe se dipendesse dal metapacchetto `NETStandard.Library`.



<!--HONumber=Nov16_HO3-->


