---
title: Dati numerici in .NET Framework | Documentazione Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SIMD
- System.Numerics.Vectors
- vectors
- scientific computing
- Complex
- numerics
- BigInteger
ms.assetid: dfebc18e-acde-4510-9fa7-9a0f4aa3bd11
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 19006cc5f24ffc66b92e53e8174c6bd33c249679
ms.openlocfilehash: 9b62cffb136abde67ab6952e7849e5681ec99a24
ms.contentlocale: it-it
ms.lasthandoff: 05/11/2017

---
# <a name="numerics-in-the-net-framework"></a>Dati numerici in .NET Framework
.NET Framework supporta le primitive numeriche integrali e a virgola mobile standard oltre a <xref:System.Numerics.BigInteger>, un tipo integrale senza limite teorico superiore o inferiore, <xref:System.Numerics.Complex>, un tipo che rappresenta numeri complessi, e un set di tipi di vettore abilitati per SIMD nello spazio dei nomi <xref:System.Numerics>.  
  
 System.Numerics.Vectors, la libreria dei tipi di vettore abilitata per SIMD è stata anche rilasciata come pacchetto NuGet.  
  
## <a name="integral-types"></a>Tipi integrali  
 .NET Framework supporta interi con e senza segno di lunghezza da 1 a 8 byte. La tabella seguente contiene un elenco dei tipi integrali e delle relative dimensioni, indica se sono con o senza segno e il specifica relativo intervallo. Tutti gli Integer sono tipi di valori.  
  
|Tipo|Con segno/Senza segno|Dimensioni (byte)|Valore minimo|Valore massimo|  
|----------|----------------------|--------------------|-------------------|-------------------|  
|<xref:System.Byte?displayProperty=fullName>|Senza segno|1|0|255|  
|<xref:System.Int16?displayProperty=fullName>|Firmato|2|-32,768|32,767|  
|<xref:System.Int32?displayProperty=fullName>|Firmato|4|-2,147,483,648|2,147,483,647|  
|<xref:System.Int64?displayProperty=fullName>|Firmato|8|-9,223,372,036,854,775,808|9,223,372,036,854,775,807|  
|<xref:System.SByte?displayProperty=fullName>|Firmato|1|-128|127|  
|<xref:System.UInt16?displayProperty=fullName>|Senza segno|2|0|65,535|  
|<xref:System.UInt32?displayProperty=fullName>|Senza segno|4|0|4,294,967,295|  
|<xref:System.UInt64?displayProperty=fullName>|Senza segno|8|0|18,446,744,073,709,551,615|  
  
 Ogni tipo integrale supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita. Ogni Integer include anche metodi per eseguire confronti di uguaglianza e confronti relativi, per convertire la rappresentazione di stringa di un numero in tale Integer e per convertire un Integer nella relativa rappresentazione di stringa. Altre operazioni matematiche oltre a quelle gestite dagli operatori standard, ad esempio arrotondamento e identificazione del valore più grande o più piccolo tra due Integer, sono disponibili nella classe <xref:System.Math>. È anche possibile operare sui singoli bit di un valore Integer usando la <xref:System.BitConverter> classe.  
  
 Si noti che i tipi integrali senza segno non sono conformi a CLS. Per altre informazioni, vedere [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../docs/standard/language-independence-and-language-independent-components.md).  
  
## <a name="floating-point-types"></a>Tipi a virgola mobile  
 .NET Framework include tre tipi primitivi a virgola mobile, elencati nella tabella seguente.  
  
|Tipo|Dimensioni (in byte)|Minimo|Massimo|  
|----------|-----------------------|-------------|-------------|  
|<xref:System.Double?displayProperty=fullName>|8|-1.79769313486232e308|1.79769313486232e308|  
|<xref:System.Single?displayProperty=fullName>|4|-3.402823e38|3.402823e38|  
|<xref:System.Decimal?displayProperty=fullName>|16|-79,228,162,514,264,337,593,543,950,335|79,228,162,514,264,337,593,543,950,335|  
  
 Ogni tipo a virgola mobile supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita. Include inoltre metodi per eseguire confronti di uguaglianza e confronti relativi, per convertire la rappresentazione di stringa di un numero a virgola mobile e per convertire un numero a virgola mobile nella relativa rappresentazione di stringa. Altre operazioni matematiche, algebriche e trigonometriche sono disponibili nella classe <xref:System.Math>. È anche possibile operare sui singoli bit dei valori <xref:System.Double> e <xref:System.Single> usando la classe <xref:System.BitConverter>. La struttura <xref:System.Decimal?displayProperty=fullName> dispone di metodi specifici, <xref:System.Decimal.GetBits%2A?displayProperty=fullName> e <xref:System.Decimal.%23ctor%28System.Int32%5B%5D%29?displayProperty=fullName>, che consentono di operare sui singoli bit di un valore decimale, nonché di un set di metodi specifici per l'esecuzione di altre operazioni matematiche.  
  
 I tipi <xref:System.Double> e <xref:System.Single> sono destinati all'uso con valori imprecisi per natura (ad esempio la distanza tra due stelle nel sistema solare) e per applicazioni che non richiedono un livello elevato di precisione e un errore di arrotondamento di entità ridotta. Per i casi in cui è necessaria una maggiore precisione e gli errori di arrotondamento non sono desiderabili, è consigliabile usare il tipo <xref:System.Decimal?displayProperty=fullName>.  
  
## <a name="biginteger"></a>BigInteger  
 <xref:System.Numerics.BigInteger?displayProperty=fullName> è un tipo immutabile che rappresenta un Integer arbitrariamente grande il cui valore in teoria non dispone di limiti inferiori o superiori. I metodi del tipo <xref:System.Numerics.BigInteger> sono strettamente paralleli a quelli di altri tipi integrali.  
  
## <a name="complex"></a>Complex  
 Il tipo <xref:System.Numerics.Complex> rappresenta un numero complesso, ovvero composto da una parte numerica reale e da una parte numerica immaginaria. Supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita, oltre che metodi matematici, algebrici e trigonometrici.  
  
## <a name="simd-enabled-vector-types"></a>Tipi di vettore abilitati per SIMD  
 Lo spazio dei nomi <xref:System.Numerics> include un set di tipi di vettore abilitati per SIMD per .NET Framework. SIMD (Single Instruction Multiple Data) consente di parallelizzare alcune operazioni a livello hardware, con un notevole miglioramento delle prestazioni nelle app matematiche, scientifiche e di grafica che eseguono calcoli su vettori.  
  
 I tipi di vettore abilitati per SIMD in .NET Framework sono elencati di seguito.  System.Numerics.Vectors include inoltre un tipo Plane e un tipo Quaternion.  
  
-   Tipi <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3> e <xref:System.Numerics.Vector4>, che sono vettori a due, tre e quattro dimensioni di tipo <xref:System.Single>.  
  
-   Due tipi di matrici: <xref:System.Numerics.Matrix3x2>, che rappresenta una matrice 3x2, e <xref:System.Numerics.Matrix4x4>, che rappresenta una matrice 4x4.  
  
-   Tipi <xref:System.Numerics.Plane> e <xref:System.Numerics.Quaternion>.  
  
 I tipi di vettore abilitati per SIMD sono implementati in IL, dunque è possibile usarli su hardware e compilatori JIT non abilitati per SIMD. Per sfruttare le istruzioni SIMD, le app a 64 bit devono essere compilate con il nuovo compilatore JIT a 64 bit per codice gestito, incluso con .NET Framework 4.6, che aggiunge il supporto SIMD quando le app sono destinate a processori x64.  
  
 È anche possibile scaricare SIMD come [pacchetto NuGet](http://www.nuget.org/packages/System.Numerics.Vectors).  Il pacchetto NuGet include anche una struttura <xref:System.Numerics.Vector%601> generica che consente di creare un vettore di qualsiasi tipo numerico primitivo. I tipi numerici primitivi includono tutti i tipi numerici dello spazio dei nomi <xref:System> ad eccezione di <xref:System.Decimal>. La struttura <xref:System.Numerics.Vector%601> fornisce anche una libreria di metodi utili che è possibile chiamare quando si usano i vettori.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti di base sulle applicazioni](../../docs/standard/application-essentials.md)
