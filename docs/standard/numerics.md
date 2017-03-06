---
title: Dati numerici in .NET Core
description: Dati numerici in .NET Core
keywords: .NET, .NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6b8696be-55f5-4b66-98f3-69ff827c2c49
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 8e2aad830bdaccad6e8184fa462dd0d3157fd6c9
ms.lasthandoff: 03/02/2017

---

# <a name="numerics-in-net-core"></a>Dati numerici in .NET Core

.NET Framework supporta le primitive numeriche integrali e a virgola mobile standard, oltre a [System.Numerics.BigInteger](https://docs.microsoft.com/dotnet/core/api/System.Numerics.BigInteger), un tipo integrale senza limite teorico superiore o inferiore, [System.Numerics.Complex](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Complex), un tipo che rappresenta numeri complessi, e un set di tipi di vettore abilitati per [SIMD](https://en.wikipedia.org/wiki/SIMD) (Single Instruction Multiple Data) nello spazio dei nomi [System.Numerics](https://docs.microsoft.com/dotnet/core/api/System.Numerics). 

## <a name="integral-types"></a>Tipi integrali

.NET Core supporta interi con e senza segno di lunghezza da&1; a&8; byte. La tabella seguente contiene un elenco dei tipi integrali e delle relative dimensioni, indica se sono con o senza segno e il specifica relativo intervallo. Tutti gli Integer sono tipi di valori. 

Tipo | Con segno/Senza segno | Dimensioni (byte) | Valore minimo | Valore massimo
---- | --------------- | ------------ | ------------- | -------------
[System.Byte](https://docs.microsoft.com/dotnet/core/api/System.Byte) | Senza segno | 1 | 0 | 255
[System.Int16](https://docs.microsoft.com/dotnet/core/api/System.Int16) | Firmato | 2 | -32,768 | 32,767
[System.Int32](https://docs.microsoft.com/dotnet/core/api/System.Int32) | Firmato | 4 | -2,147,483,648 | 2,147,483,647
[System.Int64](https://docs.microsoft.com/dotnet/core/api/System.Int64) | Firmato | 8 | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807
[System.SByte](https://docs.microsoft.com/dotnet/core/api/System.SByte) | Firmato | 1 | -128 | 127
[System.UInt16](https://docs.microsoft.com/dotnet/core/api/System.UInt16) | Senza segno | 2 | 0 | 65,535
[System.UInt32](https://docs.microsoft.com/dotnet/core/api/System.UInt32) | Senza segno | 4 | 0 | 4,294,967,295
[System.UInt64](https://docs.microsoft.com/dotnet/core/api/System.UInt64) | Senza segno | 8 | 0 | 18,446,744,073,709,551,615

Ogni tipo integrale supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita. Ogni Integer include anche metodi per eseguire confronti di uguaglianza e confronti relativi, per convertire la rappresentazione di stringa di un numero in tale Integer e per convertire un Integer nella relativa rappresentazione di stringa. Altre operazioni matematiche oltre a quelle gestite dagli operatori standard, ad esempio arrotondamento e identificazione del valore più grande o più piccolo tra due Integer, sono disponibili nella classe [System.Math](https://docs.microsoft.com/dotnet/core/api/System.Math). È anche possibile operare sui singoli bit di un valore Integer usando la classe [System.BitConverter](https://docs.microsoft.com/dotnet/core/api/System.BitConverter). 
     
Si noti che i tipi integrali senza segno non sono conformi a CLS. Per altre informazioni, vedere [.NET Common Type System & Common Language Specification](common-type-system.md) (Common Type System e specifiche CLS).

## <a name="floating-point-types"></a>Tipi a virgola mobile

.NET Core include tre tipi primitivi a virgola mobile, elencati nella tabella seguente. 

Tipo | Dimensioni (byte) | Valore minimo | Valore massimo
---- | ------------ | ------------- | -------------
[System.Double](https://docs.microsoft.com/dotnet/core/api/System.Double) | 8 | -1.79769313486232e308 | 1.79769313486232e308
[System.Single](https://docs.microsoft.com/dotnet/core/api/System.Single) | 4 | -3.402823e38 | 3.402823e38
[System.Decimal](https://docs.microsoft.com/dotnet/core/api/System.Decimal) | 16 | -79,228,162,514,264,337,593,543,950,335 | 79,228,162,514,264,337,593,543,950,335
   
Ogni tipo a virgola mobile supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita. Include inoltre metodi per eseguire confronti di uguaglianza e confronti relativi, per convertire la rappresentazione di stringa di un numero a virgola mobile e per convertire un numero a virgola mobile nella relativa rappresentazione di stringa. Altre operazioni matematiche, algebriche e trigonometriche sono disponibili nella classe `Math`. È anche possibile operare sui singoli bit dei valori `Double` e `Single` usando la classe `BitConverter`. La struttura `Decimal` dispone di metodi specifici, `Decimal.GetBits` e `Decimal.Decimal(Int32())`, che consentono di operare sui singoli bit di un valore decimale, nonché di un set di metodi specifici per l'esecuzione di altre operazioni matematiche. 

I tipi `Double` e `Single` sono destinati all'uso con valori imprecisi per natura (ad esempio la distanza tra due stelle nel sistema solare) e per applicazioni che non richiedono un livello elevato di precisione e un errore di arrotondamento di entità ridotta. Per i casi in cui è necessaria una maggiore precisione e sono da evitare errori di arrotondamento, è consigliabile usare il tipo `Decimal`.

## <a name="biginteger"></a>BigInteger

[System.Numerics.BigInteger](https://docs.microsoft.com/dotnet/core/api/System.Numerics.BigInteger) è un tipo immutabile che rappresenta un Integer di dimensioni arbitrarie il cui valore in teoria non ha limiti inferiori o superiori. I metodi del tipo `BigInteger` sono strettamente paralleli a quelli di altri tipi integrali.  

## <a name="complex"></a>Complex

Il tipo [System.Numerics.Complex](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Complex) rappresenta un numero complesso, ovvero composto da una parte numerica reale e da una parte numerica immaginaria. Supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita, oltre che metodi matematici, algebrici e trigonometrici. 

## <a name="simd-enabled-vector-types"></a>Tipi di vettore abilitati per SIMD

Lo spazio dei nomi `System.Numerics` include un set di tipi di vettore abilitati per SIMD per .NET Core. SIMD consente di parallelizzare alcune operazioni a livello hardware, con un notevole miglioramento delle prestazioni nelle app matematiche, scientifiche e di grafica che eseguono calcoli su vettori. 

I tipi di vettore abilitati per SIMD in .NET Core sono elencati di seguito: 

* I tipi [System.Numerics.Vector2](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector2), [System.Numerics.Vector3](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector3) e [System.Numerics.Vector4](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector4), che sono vettori a 2, 3 e 4 dimensioni di tipo `Single`.

* La struttura[Vector&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Vector-1) consente di creare un vettore di qualsiasi tipo numerico primitivo. I tipi numerici primitivi includono tutti i tipi numerici dello spazio dei nomi System ad eccezione di Decimal.

* Due tipi di matrici: [System.Numerics.Matrix3x2](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Matrix3x2), che rappresenta una matrice 3x2, e [System.Numerics.Matrix4x4](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Matrix4x4), che rappresenta una matrice 4x4. 

* Il tipo [System.Numerics.Plane](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Plane), che rappresenta un piano tridimensionale, e il tipo [System.Numerics.Quaternion](https://docs.microsoft.com/dotnet/core/api/System.Numerics.Quaternion), che rappresenta un vettore usato per codificare le rotazioni fisiche tridimensionali.

