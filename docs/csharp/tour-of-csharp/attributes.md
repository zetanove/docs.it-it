---
title: Attributi C# | Panoramica del linguaggio C#
description: Informazioni sulla programmazione dichiarativa con attributi in C#
keywords: .NET, csharp
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 753bcfe2-7ddd-4487-9513-ba70937fc8e9
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5ef8b93bf0a2cf98c5251b888b61db9ab12d9a71
ms.lasthandoff: 03/13/2017

---

# <a name="attributes"></a>Attributi

Tipi, membri e altre entità di un programma C# supportano modificatori che controllano alcuni aspetti del loro comportamento. L'accessibilità di un metodo, ad esempio, è controllata con i modificatori `public`, `protected`, `internal` e `private`. Il linguaggio C# generalizza questa funzionalità in modo che i tipi di informazioni dichiarative definiti dall'utente possano essere associati a entità di programma e recuperati in fase di esecuzione. I programmi specificano queste informazioni dichiarative aggiuntive definendo e usando ***attributi***.

Nell'esempio seguente viene dichiarato un attributo `HelpAttribute` che può essere inserito in entità di programma per fornire collegamenti alla documentazione correlata.

[!code-csharp[AttributeDefined](../../../samples/snippets/csharp/tour/attributes/Program.cs#L3-L20)]

Tutte le classi di attributo derivano dalla classe di base @System.Attribute fornita dalla libreria standard. Gli attributi possono essere applicati specificandone il nome (con eventuali argomenti) tra parentesi quadre appena prima della dichiarazione associata. Se il nome dell'attributo termina con `Attribute`, questa parte del nome può essere omessa quando si fa riferimento all'attributo. L'attributo `HelpAttribute`, ad esempio, può essere usato come illustrato di seguito.

[!code-csharp[AttributeApplied](../../../samples/snippets/csharp/tour/attributes/Program.cs#L22-L28)]

In questo esempio viene associato un attributo `HelpAttribute` alla classe `Widget` e viene aggiunto un altro attributo `HelpAttribute` al metodo `Display` nella classe. I costruttori pubblici di una classe di attributo controllano le informazioni che devono essere specificate quando l'attributo è associato a un'entità di programma. È possibile specificare informazioni aggiuntive facendo riferimento a proprietà di lettura/scrittura pubbliche della classe di attributo, ad esempio il riferimento alla proprietà `Topic` precedente.

Se un attributo viene richiesto tramite reflection, il costruttore della classe di attributo viene richiamato con le informazioni specificate nell'origine del programma e viene restituita l'istanza dell'attributo risultante. Se sono state fornite informazioni aggiuntive tramite proprietà, queste vengono impostate sui valori specificati prima che venga restituita l'istanza dell'attributo.

>[!div class="step-by-step"]
[Precedente](delegates.md)

