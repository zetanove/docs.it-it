---
title: Common Type System e Common Language Specification
description: Common Type System e Common Language Specification
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 3b1f5725-ac94-4f17-8e5f-244442438a4d
translationtype: Human Translation
ms.sourcegitcommit: b967d8e55347f44a012e4ad8e916440ae228c8ec
ms.openlocfilehash: 1680934b40c3055d2c33ed7457d8734dccbd0a8c
ms.lasthandoff: 03/10/2017

---

# <a name="common-type-system--common-language-specification"></a>Common Type System e Common Language Specification

Siamo di fronte ancora una volta a due termini molto usati nel mondo di .NET e che sono effettivamente fondamentali per capire in che modo la piattaforma .NET consente lo sviluppo multi-linguaggio e per comprenderne il funzionamento.

## <a name="common-type-system"></a>Common Type System

Per partire dall'inizio, tenere presente che la piattaforma .NET è _indipendente dal linguaggio_. Ciò non significa semplicemente che un programmatore può scrivere codice in qualsiasi linguaggio che possa essere compilato in linguaggio intermedio. Significa anche che il programmatore deve poter interagire con il codice scritto in altri linguaggi che possano essere usati nella piattaforma .NET.

Per poter far ciò in modo trasparente, deve esistere una modalità comune per descrivere tutti i tipi supportati. Questo è il compito di Common Type System (CTS). È stato realizzato per eseguire diverse operazioni:

*   Stabilire un framework per l'esecuzione di diversi linguaggi.
*   Offrire un modello orientato a oggetti per supportare l'implementazione di vari linguaggi sulla piattaforma .NET.
*   Definire un set di regole che tutti i linguaggi devono seguire quando si tratta di uso dei tipi.
*   Specificare una libreria che contenga i tipi di dati primitivi di base, ad esempio `Boolean`, `Byte`, `Char` e così via, usati nello sviluppo delle applicazioni.

CTS definisce due tipologie principali di tipi che devono essere supportati: riferimento e valore. I rispettivi nomi ne indicano la definizione.

Gli oggetti dei tipi riferimento sono rappresentati da un riferimento al valore effettivo dell'oggetto. In questo contesto un riferimento è simile a un puntatore in C/C++. Fa semplicemente riferimento a una posizione di memoria in cui si trovano i valori degli oggetti. Questo ha un impatto notevole sull'uso di questi tipi. Se si assegna un tipo riferimento a una variabile e quindi si passa tale variabile in un metodo, ad esempio, qualsiasi modifica all'oggetto si rifletterà sull'oggetto principale. Non si tratta di eseguire una copia.

I tipi valore sono l'opposto, in quanto gli oggetti sono rappresentati dai propri valori. Se si assegna un tipo valore a una variabile, si sta essenzialmente copiando un valore dell'oggetto.

CTS definisce diverse categorie di tipi, ognuna con una semantica e un uso specifici:

*   Classi
*   Strutture
*   Enumerazioni
*   Interfacce
*   Delegati

CTS definisce anche tutte le altre proprietà dei tipi, ad esempio i modificatori di accesso, quali sono i membri di tipo valido, come funzionano ereditarietà e overload e così via. Sfortunatamente, un'analisi approfondita di tali aspetti va oltre l'ambito di un articolo introduttivo come questo, ma è possibile accedere alla sezione [Altre risorse](#more-resources) alla fine per collegamenti a contenuti più dettagliati su questi argomenti.

## <a name="common-language-specification"></a>Common Language Specification

Per abilitare scenari di interoperabilità completa, tutti gli oggetti creati nel codice devono basarsi su un aspetto comune ai linguaggi che li usano, definito _chiamante_. Poiché sono presenti numerosi linguaggi diversi, la piattaforma .NET ha specificato tali aspetti comuni in **Common Language Specification** (Specifiche CLS). CLS definisce un set di funzionalità necessarie per molte applicazioni comuni. Offre anche una sorta di "ricetta" per qualsiasi linguaggio che viene implementato sulla piattaforma .NET, specificando cosa debba supportare.

CLS è un subset di CTS. Ciò significa che tutte le regole in CTS si applicano anche a CLS, a meno che le regole di CLS siano più restrittive. Se un componente viene compilato usando solo le regole in CLS, in altre parole espone solo le funzionalità di CLS nelle proprie API, viene definito come **conforme a CLS**. Ad esempio, le `<framework-librares>` sono conformi a CLS proprio per il fatto che devono funzionare per tutti i linguaggi supportati nella piattaforma .NET.

È possibile vedere i documenti nella sezione [Altre risorse](#more-resources) qui sotto per una panoramica di tutte le funzionalità in CLS.

## <a name="more-resources"></a>Altre risorse

*   [Common Type System](https://msdn.microsoft.com/library/zcx1eb1e.aspx)
*   [Common Language Specification](https://msdn.microsoft.com/library/12a7a7h3.aspx)

