---
title: Compilazione e uso ripetitivo nelle espressioni regolari
description: Compilazione e uso ripetitivo nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 3adea434-e2ed-4023-b4f5-b0608b4cf53f
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 7b3acb4571cddc19520f8534828d94844c9d59e6
ms.lasthandoff: 03/02/2017

---

# <a name="compilation-and-reuse-in-regular-expressions"></a>Compilazione e uso ripetitivo nelle espressioni regolari

Se si comprendono le modalità con cui le espressioni regolari vengono compilate dal motore e vengono memorizzate nella cache, è possibile ottimizzare le prestazioni delle applicazioni che fanno ampio uso di espressioni regolari. In questo argomento vengono descritte sia la compilazione che la memorizzazione nella cache.

## <a name="compiled-regular-expressions"></a>Espressioni regolari compilate

Per impostazione predefinita, il motore delle espressioni regolari compila un'espressione regolare in una sequenza di istruzioni interne. Si tratta di codici di alto livello che sono diversi da Microsoft intermediate language, o MSIL. Quando il motore esegue un'espressione regolare, interpreta i codici interni.

Se un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) viene costruito con l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled), compila l'espressione regolare in codice MSIL esplicito anziché in istruzioni interne di espressione regolare di alto livello. In questo modo il compilatore JIT di.NET può convertire l'espressione in codice macchina nativo per ottimizzare le prestazioni.

Tuttavia, il codice MSIL generato non può essere scaricato. L'unico modo per scaricare il codice è scaricare un dominio dell'applicazione intero, ovvero, tutto il codice dell'applicazione. In effetti, una volta che un'espressione regolare viene compilata con l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled), .NET non rilascia mai le risorse usate dall'espressione compilata, anche se l'espressione regolare è stata creata da un oggetto [Regex](xref:System.Text.RegularExpressions.Regex), a sua volta rilasciato in Garbage Collection.

È necessario prestare attenzione quando si sceglie il numero di espressioni regolari da compilare con l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled), in quanto si rischia un uso eccessivo di risorse. Se un'applicazione deve usare un numero elevato o illimitato di espressioni regolari, ogni espressione deve essere interpretata, non compilata. Tuttavia, se un numero ridotto di espressioni regolari viene usato ripetutamente, sarà preferibile compilare tali espressioni con [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) per ottenere prestazioni migliori. 

## <a name="the-regular-expressions-cache"></a>La cache delle espressioni regolari

Per migliorare le prestazioni, il motore delle espressioni regolari gestisce una cache a livello di applicazione delle espressioni regolari compilate. La cache memorizza i modelli di espressione regolare che vengono usati solo nelle chiamate di metodo statico. I modelli di espressione regolare specificati per i metodi di istanza non vengono memorizzati. Questo evita la necessità di analizzare nuovamente un'espressione nel codice di alto livello ogni volta che viene usata.

Il numero massimo di espressioni regolari memorizzate nella cache è determinato dal valore della proprietà `static` (`Shared` in Visual Basic) [Regex.CacheSize](xref:System.Text.RegularExpressions.Regex.CacheSize). Per impostazione predefinita, il motore delle espressioni regolari memorizza nella cache fino a 15 espressioni regolari compilate. Se il numero di espressioni regolari compilate supera la dimensione della cache, l'espressione regolare usata meno di recente viene eliminata e viene memorizzata nella cache la nuova espressione regolare. 

L'applicazione dell'utente può trarre vantaggio delle espressioni regolari precompilate in uno dei due modi seguenti:

* Usando un metodo statico dell'oggetto [Regex](xref:System.Text.RegularExpressions.Regex) per definire l'espressione regolare. Se si usa un modello di espressione regolare che è già stato definito in un'altra chiamata di metodo statico, il motore delle espressioni regolari lo recupera dalla cache. In caso contrario il motore compila l'espressione regolare e la aggiunge alla cache.

* Usando ripetutamente un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) esistente finché il modello di espressione regolare relativo è necessario.


A causa del sovraccarico di creazione di istanze di oggetti e di compilazione di espressioni regolari, la creazione e l'eliminazione rapide di numerosi oggetti [Regex](xref:System.Text.RegularExpressions.Regex) è un processo molto costoso. Per le applicazioni che usano un numero elevato di espressioni regolari, è possibile ottimizzare le prestazioni mediante chiamate di metodi statici [Regex](xref:System.Text.RegularExpressions.Regex) e aumentando eventualmente la dimensione della cache delle espressioni regolari.

## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)


