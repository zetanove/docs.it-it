---
title: Librerie del framework
description: Librerie del framework
keywords: .NET, .NET Core
author: richlander
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 7b77b6c1-8367-4602-bff3-91e4c05ac643
translationtype: Human Translation
ms.sourcegitcommit: 9df468c7225dbf1e3317ea34bd8b2285361a69f4
ms.openlocfilehash: f14e6552b2f59694f5cf877ee8ab76ffa026f18f
ms.lasthandoff: 01/18/2017

---

# <a name="framework-libraries"></a>Librerie del framework

.NET ha un ampio set standard di librerie di classi, definite librerie di classi di base (set di base) o librerie di classi di framework (set completo). Le librerie offrono implementazioni per molti tipi generali e specifici dell'app, algoritmi e funzionalità di utilità. Le librerie commerciali e delle community sono basati sulle librerie di classi di framework e offrono librerie disponibili sul mercato facili da usare per un ampio set di attività di elaborazione.

Con ogni implementazione di .NET viene offerto un sottoinsieme di queste librerie. Le API delle librerie di classi base sono incluse in qualsiasi implementazione di .NET, poiché sono richieste dagli sviluppatori e necessarie all'esecuzione delle librerie comunemente diffuse. Le librerie specifiche delle app di livello superiore alle librerie di classi base, ad esempio ASP.NET, non saranno disponibili in tutte le implementazioni .NET.

## <a name="base-class-libraries"></a>Librerie di classi base

Le librerie di classi base offrono i tipi fondamentali e le funzionalità di utilità e sono la base per tutte le altre librerie di classi .NET. Hanno lo scopo di offrire implementazioni molto generali senza eccezioni ai carichi di lavoro. Le prestazioni sono sempre un fattore importante, poiché le app potrebbero preferire criteri specifici, ad esempio bassa latenza o velocità elevata oppure memoria minima o basso utilizzo della CPU. Queste librerie in genere sono destinate ad alte prestazioni e rappresentano un compromesso operativo tra i vari livelli di esecuzione. Per la maggior parte delle app, la loro implementazione ha dato risultati abbastanza positivi.

## <a name="primitive-types"></a>Tipi primitivi

.NET include un set di tipi primitivi, che vengono usati in tutti i programmi (a diversi livelli). Questi tipi contengono dati, ad esempio numeri, stringhe, byte e oggetti arbitrari. Il linguaggio C# include parole chiave per questi tipi. Un set di esempio di questi tipi è elencato di seguito, con le parole chiave del linguaggio C# corrispondenti.

* [System.Object](https://msdn.microsoft.com/library/system.object.aspx) ([object](https://msdn.microsoft.com/library/9kkx3h3c.aspx)): classe base principale nel sistema di tipo CLR. È la radice della gerarchia dei tipi.
* [System.Int16](https://msdn.microsoft.com/library/system.int16.aspx) ([short](https://msdn.microsoft.com/library/ybs77ex4.aspx)): tipo intero con segno a 16 bit. È anche disponibile il tipo [UInt16](https://msdn.microsoft.com/library/system.uint16.aspx) senza segno.
* [System.Int32](https://msdn.microsoft.com/library/system.int32.aspx) ([int](https://msdn.microsoft.com/library/5kzh1b5w.aspx)): tipo intero con segno a 32 bit. È anche disponibile il tipo [UInt32](https://msdn.microsoft.com/library/x0sksh43.aspx) senza segno.
* [System.Single](https://msdn.microsoft.com/library/system.single.aspx) ([float](https://msdn.microsoft.com/library/b1e65aza.aspx)): tipo a virgola mobile a 32 bit.
* [System.Decimal](https://msdn.microsoft.com/library/system.decimal.aspx) ([decimal](https://msdn.microsoft.com/library/364x0z75.aspx)): tipo decimale a 128 bit.
* [System.Byte](https://msdn.microsoft.com/library/system.byte.aspx) ([byte](https://msdn.microsoft.com/library/5bdb6693.aspx)): tipo intero senza segno a 8 bit che rappresenta un byte di memoria.
* [System.Boolean](https://msdn.microsoft.com/library/system.boolean.aspx) ([bool](https://msdn.microsoft.com/library/c8f5xwh7.aspx)): tipo booleano che rappresenta 'true' o 'false'.
* [System.Char](https://msdn.microsoft.com/library/system.char.aspx) ([char](https://msdn.microsoft.com/library/x9h8tsay.aspx)): tipo numerico a 16 bit che rappresenta un carattere Unicode.
* [System.String](https://msdn.microsoft.com/library/system.string.aspx) ([string](https://msdn.microsoft.com/library/362314fe.aspx)): rappresenta una serie di caratteri. Diverso dal tipo `char[]`, ma consente l'indicizzazione in ogni singolo `char` di `string`.

## <a name="data-structures"></a>Strutture di dati

.NET include un insieme di strutture di dati che sono alla base di quasi tutte le applicazioni .NET. Si tratta principalmente di raccolte, ma sono inclusi anche altri tipi.

*   [Array](https://msdn.microsoft.com/library/system.array.aspx): rappresenta una matrice di oggetti fortemente tipizzati accessibile con l'indice. Per struttura, ha una dimensione fissa.
*   [List](https://msdn.microsoft.com/library/6sh2ey19.aspx): rappresenta un elenco di oggetti fortemente tipizzati accessibili con l'indice. Viene ridimensionato automaticamente secondo le necessità.
*   [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx): rappresenta una raccolta di valori indicizzati da una chiave. I valori sono accessibili tramite chiave. Viene ridimensionato automaticamente secondo le necessità.
*   [Uri](https://msdn.microsoft.com/library/system.uri.aspx): offre una rappresentazione in forma di oggetto di un identificatore URI (Uniform Resource Identifier) e accesso facile alle parti dell'URI.
*   [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx): rappresenta un istante di tempo, in genere espresso come data e ora del giorno.

## <a name="utility-apis"></a>API di utilità

.NET include un set di API di utilità che offre funzionalità per molte attività importanti.

*   [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient.aspx): un'API per inviare richieste HTTP e ricevere risposte HTTP da una risorsa identificata da un URI.
*   [XDocument](https://msdn.microsoft.com/library/system.xml.linq.xdocument.aspx): un'API per il caricamento e l'esecuzione di query su documenti XML con LINQ.
*   [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader.aspx): un'API per leggere file ([StreamWriter](https://msdn.microsoft.com/library/system.io.stringwriter.aspx)). Può essere usata anche per scrivere file.

## <a name="app-model-apis"></a>API dei modelli per App

Ci sono molti modelli per app, offerti da diverse società, che possono essere usati con .NET.

*   [ASP.NET](http://asp.net): offre un framework Web per la creazione di siti Web e servizi. Supportato in Windows, Linux e macOS (dipende dalla versione ASP.NET).

