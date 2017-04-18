---
title: Provider di tipi
description: Provider di tipi
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 25697ef6-465e-4248-9de5-1d199d4a8b59
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: e9e67e6531e0c1daad0c0d4a9f778670d5cb2263
ms.lasthandoff: 04/05/2017

---

# <a name="type-providers"></a>Provider di tipi

> [!NOTE]
Questa guida è stata scritta a partire da F# 3.0 e verrà aggiornata.  Per provider di tipo multipiattaforma aggiornati, vedere [FSharp.Data](http://fsharp.github.io/FSharp.Data/).

Un provider di tipi F# è un componente che fornisce tipi, proprietà e metodi da utilizzare in un programma. I provider di tipi sono una parte significativa per il supporto di F# 3.0, per una programmazione con informazioni. La chiave per la programmazione con informazioni è eliminare le barriere per utilizzare le diverse risorse trovate in Internet e negli ambienti aziendali moderni. Una barriera significativa per includere una risorsa di informazioni in un programma è la necessità di rappresentare tali informazioni come tipi, proprietà e metodi da utilizzare nell'ambiente di un linguaggio di programmazione. La scrittura manuale di questi tipi richiede molto tempo ed è difficile da gestire. Un'alternativa comune prevede l'utilizzo di un generatore di codice per aggiungere file al progetto. Tuttavia, i tipi convenzionali per la generazione di codice non si adattano alle modalità esplorative di programmazione supportate da F#, perché il codice generato deve essere sostituito ogni volta che viene modificato un riferimento al servizio.

I tipi forniti dal provider di tipi F# sono in genere basati su origini di informazioni esterne. Ad esempio, un tipo di provider F# per SQL fornirà tipi, proprietà e metodi necessari per utilizzare direttamente le tabelle di ogni database SQL al quale è necessario accedere. Analogamente, un tipo di provider per i servizi Web WSDL fornirà i tipi, proprietà e metodi che è necessario utilizzare direttamente con qualsiasi servizio Web WSDL.

Il set di tipi, proprietà e metodi forniti da un provider di tipi F# possono dipendere dai parametri indicati nel codice del programma. Ad esempio, un provider di tipi può fornire tipi diversi in base a una stringa di connessione o un URL di servizio. In questo modo, lo spazio di informazioni disponibile tramite la stringa di connessione o un URL viene integrato direttamente nel programma. Un provider di tipi può inoltre garantire che i gruppi di tipi siano espandibili solamente su richiesta, ovvero vengono espansi se ai tipi viene effettivamente fatto riferimento dal programma. Questo consente di utilizzare l'integrazione diretta su richiesta di spazi di informazioni su larga scala fortemente tipizzati, come i mercati di dati online.

F# contiene diversi provider di tipi incorporati per servizi dati Internet e aziendali di uso comune. Questi tipi di provider forniscono un accesso semplice e regolare a database relazionali SQL, OData basati sulla rete e servizi WSDL e supportano l'utilizzo di query LINQ F# rispetto a tali origini dati.

Se necessario, è possibile creare provider di tipi personalizzati o fare riferimento a provider di tipi creati da altri. Ad esempio, si supponga che l'organizzazione abbia un servizio dati che fornisce un numero elevato e crescente di set di dati denominati, ciascuno con il proprio schema dati stabile. È possibile scegliere di creare un provider di tipi che legge gli schemi ed elenca gli ultimi set di dati disponibili per il programmatore, in una modalità fortemente tipizzata.


## <a name="related-topics"></a>Argomenti correlati


|Titolo|Descrizione|
|-----|-----------|
|[Walkthrough: Accessing a SQL Database by Using Type Providers](accessing-a-sql-database.md) (Procedura dettagliata: accesso a un database SQL tramite provider di tipi)|Viene illustrato come usare il provider di tipi SqlDataConnection per accedere alle tabelle e alle stored procedure di un database SQL, in base a una stringa di connessione per una connessione diretta a un database. L'accesso utilizza un mapping LINQ to SQL.|
|[Walkthrough: Accessing a SQL Database by Using Type Providers and Entities](accessing-a-sql-database-entities.md) (Procedura dettagliata: accesso a un database SQL tramite entità e provider di tipi)|Illustra come usare il provider di tipi SqlEntityConnection per accedere alle tabelle e alle stored procedure di un database SQL, in base a una stringa di connessione per una connessione diretta a un database. L'accesso usa un mapping LINQ to Entities. Questo metodo può essere usato con qualsiasi database, ma nell'esempio viene illustrato SQL Server.|
|[Walkthrough: Accessing an OData Service by Using Type Providers](accessing-an-odata-service.md) (Procedura dettagliata: accesso a un servizio OData tramite provider di tipi)|Illustra come usare il provider di tipi ODataService per accedere a un servizio OData in una modalità fortemente tipizzata in base all'URL di un servizio.|
|[Walkthrough: Accessing a Web Service by Using Type Providers](accessing-a-web-service.md) (Procedura dettagliata: accesso a un servizio Web tramite provider di tipi)|Illustra come usare il provider di tipi WsdlService per accedere a un servizio web WSDL in una modalità fortemente tipizzata in base a un URL del servizio.|
|[Walkthrough: Generating F&#35; Types from a DBML File](generating-fsharp-types-from-dbml.md) (Procedura dettagliata: generazione di tipi F&#35; da un file DBML)|Illustra come usare il provider di tipi DbmlFile per accedere alle tabelle e alle stored procedure di un database SQL, in base a un file DBML che fornisce una specifica dello schema del database LINQ to SQL.|
|[Walkthrough: Generating F&#35; Types from an EDMX Schema File](generating-fsharp-types-from-edmx.md) (Procedura dettagliata: generazione di tipi F&#35; da un file di schema EDMX)|Viene illustrato come utilizzare il provider di tipi EdmxFile per accedere alle tabelle e alle stored procedure di un database SQL, in base a un file EDMX che fornisce una specifica dello schema Entity Framework.|
|[Tutorial: Creating a Type Provider](creating-a-type-provider.md) (Esercitazione: creazione di un provider di tipi)|Vengono fornite informazioni sulla scrittura di provider di tipi personalizzati.|
|[Type Provider Security](type-provider-security.md) (Sicurezza dei provider di tipi)|Vengono fornite informazioni sulle considerazioni relative alla sicurezza quando si sviluppano provider di tipi.|
|[Risoluzione dei problemi relativi ai provider di tipi](troubleshooting-type-providers.md)|Vengono fornite informazioni sui problemi comuni che possono verificarsi quando si usano provider di tipi e sono inclusi suggerimenti per le soluzioni.|

## <a name="see-also"></a>Vedere anche
[Riferimenti per il linguaggio F#](../../language-reference/index.md)

[Visual F#](../../index.md)
