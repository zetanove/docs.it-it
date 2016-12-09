---
title: Pulizia delle risorse non gestite
description: Pulizia delle risorse non gestite
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/18/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 8c97c3e2-8619-47ce-ae29-d6a3140bfa83
translationtype: Human Translation
ms.sourcegitcommit: 213ce098bcc2b5e31c55e759d895254d5ca33caa
ms.openlocfilehash: c0600eb27c27261f6496fb45310514f7f716b3b3

---

# <a name="cleaning-up-unmanaged-resources"></a>Pulizia delle risorse non gestite

Le attività di gestione della memoria vengono effettuate dal Garbage Collector di .NET per la maggior parte degli oggetti creati dall'app. Se però si creano oggetti che includono risorse non gestite, sarà necessario rilasciare esplicitamente queste ultime quando si smette di utilizzarle. Il tipo più comune di risorsa non gestita è rappresentato dagli oggetti che eseguono il wrapping di risorse del sistema operativo, quali file, finestre, connessioni di rete o connessioni di database. Benché il Garbage Collector sia in grado di tenere traccia della durata di un oggetto in cui è incapsulata una risorsa non gestita, non dispone di dati sufficienti per effettuare il rilascio e la pulizia della risorsa non gestita. 

Se i tipi utilizzano risorse non gestite, è necessario effettuare le operazioni seguenti: 

* Implementare il modello Dispose. A tale scopo è necessario specificare un'implementazione [IDisposable.Dispose](xref:System.IDisposable.Dispose) per abilitare il rilascio deterministico delle risorse non gestite. Un consumer del tipo in uso chiama [Dispose](xref:System.IDisposable.Dispose) quando l'oggetto e le risorse che usa non sono più necessari. Il metodo [Dispose](xref:System.IDisposable.Dispose) rilascia immediatamente le risorse non gestite. 

* Impostare il rilascio delle risorse non gestite nel caso in cui un consumer del tipo in uso ometta di chiamare [Dispose](xref:System.IDisposable.Dispose). Questo risultato può essere raggiunto in due modi: 

    * Utilizzare un handle sicuro per eseguire il wrapping della risorsa non gestita. Questa è la tecnica consigliata. Gli handle sicuri derivano dalla classe [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) e includono un potente metodo [Finalize](xref:System.Object.Finalize). L'uso di un handle sicuro richiede semplicemente l'implementazione dell'interfaccia [IDisposable](xref:System.IDisposable) e la chiamata del metodo [Dispose](xref:System.IDisposable.Dispose) dell'handle sicuro nell'implementazione [IDisposable.Dispose](xref:System.IDisposable.Dispose). Il finalizzatore dell'handle sicuro viene chiamato automaticamente dal Garbage Collector se non viene chiamato il metodo [Dispose](xref:System.IDisposable.Dispose). 

      -oppure-

    * Eseguire l'override del metodo [Object.Finalize](xref:System.Object.Finalize). La finalizzazione abilita il rilascio non deterministico delle risorse non gestite quando il consumer di un tipo non riesce a chiamare [IDisposable.Dispose](xref:System.IDisposable.Dispose) per l'eliminazione deterministica. Tuttavia, poiché la finalizzazione dell'oggetto può essere un'operazione complessa e soggetta a errori, è consigliabile utilizzare un handle sicuro anziché fornire il proprio finalizzatore. 

I consumer del tipo in uso possono quindi chiamare l'implementazione [IDisposable.Dispose](xref:System.IDisposable.Dispose) direttamente per liberare la memoria usata dalle risorse non gestite. Quando si implementa correttamente un metodo [Dispose](xref:System.IDisposable.Dispose), il metodo [Finalize](xref:System.Object.Finalize) o il proprio override del metodo [Object.Finalize](xref:System.Object.Finalize) diventa una misura di protezione per la pulizia delle risorse nel caso in cui il metodo [Dispose](xref:System.IDisposable.Dispose) non venga chiamato. 

## <a name="in-this-section"></a>Contenuto della sezione

[Implementazione di un metodo Dispose](implementing-dispose.md): descrive come implementare il modello Dispose per il rilascio delle risorse non gestite.

[Uso di oggetti che implementano IDisposable](using-objects.md): descrive come i consumer di un determinato tipo garantiscono che venga chiamata l'implementazione Dispose corrispondente. A tale scopo, è consigliabile usare l'istruzione using in C# o l'istruzione Using in Visual Basic.

## <a name="reference"></a>Riferimento

[System.IDisposable](xref:System.IDisposable): definisce il metodo `Dispose` per il rilascio delle risorse non gestite.

[Object.Finalize](xref:System.Object.Finalize): provvede alla finalizzazione dell'oggetto se le risorse non gestite non vengono rilasciate dal metodo `Dispose`. 

[GC.SuppressFinalize](xref:System.GC#System_GC_SuppressFinalize_System_Object_): elimina la finalizzazione. Questo metodo viene abitualmente chiamato da un metodo `Dispose` per impedire l'esecuzione di un finalizzatore. 



<!--HONumber=Nov16_HO3-->


