---
title: "Dati numerici in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SIMD"
  - "System.Numerics.Vectors"
  - "vettori"
  - "calcolo scientifico"
  - "Complex"
  - "dati numerici"
  - "BigInteger"
ms.assetid: dfebc18e-acde-4510-9fa7-9a0f4aa3bd11
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Dati numerici in .NET Framework
.NET Framework supporta le primitive numeriche standard a virgola mobile e integrali, nonché <xref:System.Numerics.BigInteger>, un tipo integrale con nessun limite teorico superiore o inferiore, <xref:System.Numerics.Complex>, un tipo che rappresenta numeri complessi e un set di tipi di vettori abilitati per SIMD il <xref:System.Numerics> dello spazio dei nomi.  
  
 Inoltre, System.Numerics.Vectors, la libreria dei tipi vectory, abilitati per SIMD è stata rilasciata come pacchetto NuGet.  
  
## <a name="integral-types"></a>Tipi integrali  
 .NET Framework supporta interi con e senza segno di lunghezza da&1; a&8; byte. La tabella seguente contiene un elenco dei tipi integrali e delle relative dimensioni, indica se sono con o senza segno e il specifica relativo intervallo. Tutti gli Integer sono tipi di valori.  
  
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
  
 Ogni tipo integrale supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita. Ogni Integer include anche metodi per eseguire confronti di uguaglianza e confronti relativi, per convertire la rappresentazione di stringa di un numero in tale Integer e per convertire un Integer nella relativa rappresentazione di stringa. Altre operazioni matematiche oltre a quelle gestite dagli operatori standard, ad esempio arrotondamento e identificazione del valore minore o maggiore di due interi, sono disponibili le <xref:System.Math> (classe). È anche possibile operare sui singoli bit di un valore integer usando la <xref:System.BitConverter> (classe).  
  
 Si noti che i tipi integrali senza segno non sono conformi a CLS. Per ulteriori informazioni, vedere [indipendenza del linguaggio e componenti indipendenti dal linguaggio](../../docs/standard/language-independence-and-language-independent-components.md).  
  
## <a name="floating-point-types"></a>Tipi a virgola mobile  
 .NET Framework include tre tipi primitivi a virgola mobile, elencati nella tabella seguente.  
  
|Tipo|Dimensioni (in byte)|Minimo|Massimo|  
|----------|-----------------------|-------------|-------------|  
|<xref:System.Double?displayProperty=fullName>|8|-1.79769313486232e308|1.79769313486232e308|  
|<xref:System.Single?displayProperty=fullName>|4|-3.402823e38|3.402823e38|  
|<xref:System.Decimal?displayProperty=fullName>|16|-79,228,162,514,264,337,593,543,950,335|79,228,162,514,264,337,593,543,950,335|  
  
 Ogni tipo a virgola mobile supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita. Include inoltre metodi per eseguire confronti di uguaglianza e confronti relativi, per convertire la rappresentazione di stringa di un numero a virgola mobile e per convertire un numero a virgola mobile nella relativa rappresentazione di stringa. Altre operazioni matematiche, algebriche e trigonometriche sono disponibili le <xref:System.Math> (classe). È inoltre possibile rivolgersi sui singoli bit di <xref:System.Double> e <xref:System.Single> valori utilizzando il <xref:System.BitConverter> (classe). Il <xref:System.Decimal?displayProperty=fullName> struttura dispone di metodi propri <xref:System.Decimal.GetBits%2A?displayProperty=fullName> e [Decimal.Decimal (Int32\<xref:System.Decimal.%23ctor%28System.Int32%5B%5D%29?displayProperty=fullName>, di operare con un valore decimale singoli bit, nonché un proprio set di metodi per l'esecuzione di altre operazioni matematiche.  
  
 Il <xref:System.Double> e <xref:System.Single> tipi sono deve essere utilizzata per i valori per loro natura imprecisi (ad esempio la distanza tra due stelle nel sistema solare) e per le applicazioni in cui non è richiesto un elevato livello di precisione e piccolo errore di arrotondamento. Si consiglia di utilizzare il <xref:System.Decimal?displayProperty=fullName> tipo per i casi in cui maggiore precisione è obbligatorio e gli errori di arrotondamento sono inaccettabile,  
  
## <a name="biginteger"></a>BigInteger  
 <xref:System.Numerics.BigInteger?displayProperty=fullName> è un tipo immutabile che rappresenta un Integer di dimensioni arbitrarie il cui valore in teoria non ha limiti inferiori o superiori. I metodi di <xref:System.Numerics.BigInteger> tipo strettamente paralleli a quelli di altri tipi integrali.  
  
## <a name="complex"></a>Complex  
 Il <xref:System.Numerics.Complex> tipo rappresenta un numero complesso, ovvero un numero con una parte numerica reale e una parte numerica immaginaria. Supporta un set standard di operatori aritmetici, di confronto, uguaglianza, conversione esplicita e conversione implicita, oltre che metodi matematici, algebrici e trigonometrici.  
  
## <a name="simd-enabled-vector-types"></a>Tipi di vettore abilitati per SIMD  
 Il <xref:System.Numerics> dello spazio dei nomi include un set di tipi di vettori abilitati per SIMD per .NET Framework. SIMD (Single Instruction Multiple Data) consente di parallelizzare alcune operazioni a livello hardware, con un notevole miglioramento delle prestazioni nelle app matematiche, scientifiche e di grafica che eseguono calcoli su vettori.  
  
 I tipi di vettore abilitati per SIMD in .NET Framework sono elencati di seguito.  System.Numerics.Vectors include inoltre un tipo Plane e un tipo Quaternion.  
  
-   <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3>, e <xref:System.Numerics.Vector4> tipi, ovvero 2, 3 e 4-dimensionale vettori di tipo <xref:System.Single>.  
  
-   Due tipi di matrice, <xref:System.Numerics.Matrix3x2>, che rappresenta una 3x2 matrice; e <xref:System.Numerics.Matrix4x4>, che rappresenta una 4x4 matrice.  
  
-   Il <xref:System.Numerics.Plane> e <xref:System.Numerics.Quaternion> tipi.  
  
 I tipi di vettore abilitati per SIMD sono implementati in IL, dunque è possibile usarli su hardware e compilatori JIT non abilitati per SIMD. Per sfruttare le istruzioni SIMD, le app a 64 bit devono essere compilate con il nuovo compilatore JIT a 64 bit per codice gestito, incluso con .NET Framework 4.6, che aggiunge il supporto SIMD quando le app sono destinate a processori x64.  
  
 È inoltre possibile scaricare SIMD come un [pacchetto NuGet](http://www.nuget.org/packages/System.Numerics.Vectors).  Il pacchetto NuGET include inoltre un oggetto generico <xref:System.Numerics.Vector%601> struttura che consente di creare un vettore di qualsiasi tipo numerico primitivo. (I tipi numerici primitivi includono tutti i tipi numerici di <xref:System> dello spazio dei nomi, ad eccezione di <xref:System.Decimal>.) Inoltre, il <xref:System.Numerics.Vector%601> struttura fornisce una libreria di metodi utili che è possibile chiamare quando si lavora con i vettori.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazione Essentials](../../docs/standard/application-essentials.md)