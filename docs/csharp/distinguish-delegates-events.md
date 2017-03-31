---
title: Distinzione di delegati ed eventi
description: Distinzione di delegati ed eventi
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 0fdc8629-2fdb-4a7c-a433-5b9d04eaf911
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4020df1a63cbcdeb7e7b5d9d49cfe6444a43655e
ms.lasthandoff: 03/13/2017

---

# <a name="distinguising-delegates-and-events"></a>Distinzione di delegati ed eventi

[Precedente](modern-events.md)

Gli sviluppatori che non hanno familiarità con la piattaforma .NET Core spesso sono in difficoltà quando devono scegliere tra due tipi di progettazione, uno basato su `delegates` e l'altro su `events`. Questo è un concetto difficile, poiché le due funzionalità del linguaggio sono molto simili. È persino possibile creare eventi usando il supporto del linguaggio per i delegati. 

Entrambi i tipi di progettazione consentono di usare scenari di associazione tardiva, in altre parole scenari in cui un componente comunica chiamando un metodo noto solo in runtime. Entrambi supportano metodi per sottoscrittori singoli e multipli. Questa funzionalità è nota anche come supporto singlecast e multicast. Entrambi i tipi di progettazione usano una sintassi simile per l'aggiunta e la rimozione di gestori. Per la chiamata dei metodi di generazione di eventi e di chiamata di delegati, infine, entrambi i tipi di progettazione usano esattamente la stessa sintassi. Supportano persino la stessa sintassi del metodo `Invoke()` con l'operatore `?.`.

Con tutte queste analogie, è comprensibile avere difficoltà nel determinare quando usare ognuno dei due tipi di progettazione.

## <a name="listening-to-events-is-optional"></a>L'ascolto di eventi è facoltativo

La considerazione più importante per determinare quale funzionalità del linguaggio usare è la necessità di un sottoscrittore associato. Se il codice deve chiamare il codice fornito dal sottoscrittore, è necessario usare una progettazione basata su delegati. Se il codice è in grado di eseguire tutte le operazioni contenute senza chiamare alcun sottoscrittore, è necessario usare una progettazione basata su eventi. 

Si considerino gli esempi compilati nel corso di questa sezione. Perché il codice con `List.Sort()` compilato sia in grado di ordinare correttamente gli elementi, deve essere dotato di una funzione di confronto. Perché le query LINQ siano in grado di determinare quali elementi restituire, devono essere dotate di delegati. In entrambi i casi è stata usata una progettazione compilata con delegati.

Si consideri l'evento `Progress`, che segnala lo stato di un'attività.
L'attività continua indipendentemente dal fatto che siano presenti listener o meno.
Un altro esempio è rappresentato da `FileSearcher`, che continua a cercare e trovare tutti i file specificati anche senza sottoscrittori di eventi associati.
I controlli UX continuano a funzionare correttamente, anche se non sono presenti sottoscrittori in ascolto degli eventi. Entrambi gli esempi usano progettazioni basate su eventi.

## <a name="return-values-require-delegates"></a>Per la restituzione di valori sono necessari delegati

Un'altra considerazione riguarda il prototipo che si vuole usare per il metodo del delegato. Come si è visto, per i delegati usati per gli eventi il tipo restituito è void. Si è visto anche che alcuni termini per la creazione di gestori eventi, invece, restituiscono informazioni alle origini eventi tramite la modifica di proprietà dell'oggetto argomento dell'evento. Questi termini sono efficaci, ma non sono altrettanto naturali della restituzione di un valore da parte di un metodo.

Si tenga presente che spesso questi due tipi di euristica sono presenti entrambi: se il metodo del delegato restituisce un valore, è probabile che in qualche modo influisca sull'algoritmo.

## <a name="event-listeners-often-have-longer-lifetimes"></a>I listener di eventi hanno spesso una durata maggiore 

Questa è una giustificazione leggermente più debole. È tuttavia possibile che le progettazioni basate su eventi siano più naturali se l'origine degli eventi genera eventi per un periodo di tempo duraturo. Esempi di ciò sono riscontrabili per controlli UX presenti in molti sistemi. Dopo la sottoscrizione di un evento, l'origine di questo può generare eventi per tutta la durata del programma.
È possibile annullare la sottoscrizione di eventi quando questi non sono più necessari.

Ciò contrasta con molte progettazioni basate su delegati, in cui un delegato viene usato come argomento per un metodo e non viene più usato dopo che il metodo ritorna.

## <a name="evaluate-carefully"></a>Valutare con attenzione

Le considerazioni precedenti non rappresentano regole ferree ma informazioni aggiuntive che consentono di stabilire la scelta più appropriata per il proprio caso specifico. Date le analogie, è anche possibile eseguire un prototipo per entrambi i tipi di progettazione, per verificare quale risulterebbe più naturale usare. Entrambi consentono di gestire in modo efficiente gli scenari di associazione tardiva. Usare quello che comunica meglio con il proprio progetto.

