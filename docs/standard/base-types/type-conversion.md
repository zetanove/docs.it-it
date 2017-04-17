---
title: "Conversione di tipi in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "v"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conversioni verso un tipo di dati più grande"
  - "conversioni esplicite"
  - "conversioni verso un tipo di dati più piccolo"
  - "conversione di tipo, sulla conversione dei tipi"
  - "tipo (conversione)"
  - "conversione di tipi"
  - "coercizione di restrizione"
  - "Explicit (operatore)"
  - "IConvertible (interfaccia)"
  - "tipi di base, conversione"
  - "op_Implicit (metodo)"
  - "coercizione di ampliamento"
  - "op_Explicit (metodo)"
  - "Convert (classe)"
  - "conversioni implicite"
  - "Implicit (operatore)"
  - "tipi di dati [.NET Framework], conversione"
ms.assetid: ba36154f-064c-47d3-9f05-72f93a7ca96d
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Conversione di tipi in .NET Framework
<a name="top"></a> A ogni valore è associato un tipo che definisce attributi quali la quantità di spazio allocato per il valore, l'intervallo di valori possibili supportati e i membri resi disponibili. Numerosi valori possono essere espressi mediante tipi diversi. Il valore 4, ad esempio, può essere espresso come intero o come valore a virgola mobile. Mediante la conversione di tipi viene creato un valore in un nuovo tipo equivalente al valore del tipo precedente, ma non viene necessariamente mantenuta l'identità, o il valore esatto, dell'oggetto originale.  
  
 .NET Framework supporta automaticamente le conversioni seguenti:  
  
-   Conversione da una classe derivata a una classe di base. Ciò significa, ad esempio, che un'istanza di qualsiasi classe o struttura può essere convertita in un'istanza <xref:System.Object>.  Questa conversione non richiede un operatore di conversione o di cast.  
  
-   Conversione da una classe di base a classe derivata originale. In C\#, questa conversione richiede un operatore di cast. In Visual Basic, è necessario l'operatore [CType](assetId:///CType?qualifyHint=False&amp;autoUpgrade=True) se `Option Strict` è attivo.  
  
-   Conversione da un tipo che implementa un'interfaccia a un oggetto di interfaccia che rappresenta tale interfaccia. Questa conversione non richiede un operatore di conversione o di cast.  
  
-   Conversione da un oggetto di interfaccia al tipo originale che implementa l'interfaccia.  In C\#, questa conversione richiede un operatore di cast. In Visual Basic, è necessario l'operatore assetId:///CType?qualifyHint=False&amp;autoUpgrade=True se `Option Strict` è attivo.  
  
 Oltre a queste conversioni automatiche, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] offre diverse funzionalità che supportano la conversione di tipo personalizzato. tra cui:  
  
-   Operatore `Implicit` che definisce le conversioni tra tipi verso un tipo di dati più grande. Per ulteriori informazioni, vedere la sezione [Conversione implicita con l'operatore Implicit](#implicit_conversion_with_the_implicit_operator).  
  
-   Operatore `Explicit` che definisce le conversioni tra tipi verso un tipo di dati più piccolo. Per ulteriori informazioni, vedere la sezione [Conversione esplicita con l'operatore Explicit](#explicit_conversion_with_the_explicit_operator).  
  
-   Interfaccia <xref:System.IConvertible> che definisce le conversioni in ognuno dei tipi di dati .NET Framework di base. Per ulteriori informazioni, vedere la sezione [Interfaccia IConvertible](#the_iconvertible_interface).  
  
-   Classe <xref:System.Convert> che fornisce un set di metodi che implementano i metodi nell'interfaccia <xref:System.IConvertible>. Per altre informazioni, vedere la sezione [Classe Convert](#Convert).  
  
-   Classe <xref:System.ComponentModel.TypeConverter>, una classe di base che può essere estesa per supportare la conversione di un tipo specifico in qualsiasi altro tipo. Per ulteriori informazioni, vedere la sezione [Classe TypeConverter](#the_typeconverter_class).  
  
<a name="implicit_conversion_with_the_implicit_operator"></a>   
## Conversione implicita con l'operatore Implicit  
 Le conversioni verso un tipo di dati più grande comportano la creazione di un nuovo valore dal valore di un tipo esistente che dispone di un intervallo più restrittivo o di un elenco di membri più limitato rispetto al tipo di destinazione. Le conversioni verso un tipo di dati più grande non possono comportare perdita di dati, ma è possibile che comportino una perdita di precisione. Poiché i dati non possono venire persi, i compilatori possono gestire la conversione in modo implicito o trasparente, senza la necessità di utilizzare un metodo di conversione esplicito o un operatore di cast.  
  
> [!NOTE]
>  Sebbene il codice che esegue una conversione esplicita sia in grado di chiamare un metodo di conversione o di utilizzare un operatore di cast, l'utilizzo di tali elementi non è richiesto dai compilatori che supportano le conversioni implicite.  
  
 Il tipo <xref:System.Decimal> supporta ad esempio le conversioni implicite da valori <xref:System.Byte>, <xref:System.Char>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.UInt16>, <xref:System.UInt32> e <xref:System.UInt64>. Nell'esempio seguente vengono illustrate alcune conversioni implicite nell'assegnazione di valori a una variabile <xref:System.Decimal>.  
  
 [!code-csharp[Conceptual.Conversion#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#1)]
 [!code-vb[Conceptual.Conversion#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#1)]  
  
 Se un determinato compilatore di linguaggio supporta gli operatori personalizzati, è anche possibile definire le conversioni implicite nei tipi personalizzati. Nell'esempio seguente viene fornita un'implementazione parziale di un tipo di dati Signed Byte denominato `ByteWithSign` che utilizza la rappresentazione di segno e grandezza. Il tipo supporta la conversione implicita di valori <xref:System.Byte> e <xref:System.SByte> in valori `ByteWithSign`.  
  
 [!code-csharp[Conceptual.Conversion#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#2)]
 [!code-vb[Conceptual.Conversion#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#2)]  
  
 Il codice client può quindi dichiarare una variabile `ByteWithSign` e assegnare a essa valori <xref:System.Byte> e <xref:System.SByte> senza eseguire alcuna conversione esplicita né utilizzare operatori di cast, come illustrato nell'esempio seguente.  
  
 [!code-csharp[Conceptual.Conversion#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/implicit1.cs#3)]
 [!code-vb[Conceptual.Conversion#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/implicit1.vb#3)]  
  
 [Torna all'inizio](#top)  
  
<a name="explicit_conversion_with_the_explicit_operator"></a>   
## Conversione esplicita con l'operatore Explicit  
 Le conversioni verso un tipo di dati più piccolo comportano la creazione di un nuovo valore dal valore di un tipo esistente che dispone di un intervallo più ampio o di un elenco di membri più grande rispetto al tipo di destinazione. Poiché una conversione verso un tipo di dati più piccolo può comportare una perdita di dati, i compilatori spesso richiedono che tale conversione sia resa esplicita tramite una chiamata a un metodo di conversione o a un operatore di cast. È quindi necessario gestire la conversione in modo esplicito nel codice dello sviluppatore.  
  
> [!NOTE]
>  Lo scopo principale della richiesta di un metodo di conversione o di un operatore di cast per le conversioni verso un tipo di dati più piccolo è quello di rendere lo sviluppatore consapevole della possibilità di perdita dei dati o del verificarsi di un'eccezione <xref:System.OverflowException>, in modo che tale eventualità venga gestita nel codice. In alcuni compilatori tuttavia questo requisito non è sempre rispettato. In Visual Basic, ad esempio, se l'opzione `Option Strict` è disattivata \(impostazione predefinita\), il compilatore tenta di eseguire le conversioni verso un tipo di dati più piccolo in modo implicito.  
  
 I tipi di dati <xref:System.UInt32>, <xref:System.Int64> e <xref:System.UInt64> hanno intervalli più ampi del tipo di dati <xref:System.Int32>, come illustrato nella tabella seguente.  
  
|Tipo|Confronto con intervallo di Int32|  
|----------|---------------------------------------|  
|<xref:System.Int64>|<xref:System.Int64.MaxValue?displayProperty=fullName> è maggiore di <xref:System.Int32.MaxValue?displayProperty=fullName> e <xref:System.Int64.MinValue?displayProperty=fullName> è minore di <xref:System.Int32.MinValue?displayProperty=fullName> \(ha un intervallo negativo più ampio\).|  
|<xref:System.UInt32>|<xref:System.UInt32.MaxValue?displayProperty=fullName> è maggiore di <xref:System.Int32.MaxValue?displayProperty=fullName>.|  
|<xref:System.UInt64>|<xref:System.UInt64.MaxValue?displayProperty=fullName> è maggiore di <xref:System.Int32.MaxValue?displayProperty=fullName>.|  
  
 Per gestire le conversioni verso un tipo di dati più piccolo, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] consente ai tipi di definire un operatore `Explicit`. I singoli compilatori di linguaggio possono implementare quindi questo operatore utilizzando la propria sintassi oppure è possibile chiamare un membro della classe <xref:System.Convert> per eseguire la conversione. Per altre informazioni sulla classe <xref:System.Convert>, vedere la sezione [Classe Convert](#Convert) più avanti in questo argomento. L'esempio seguente illustra l'uso delle funzionalità del linguaggio per gestire la conversione esplicita di questi valori Integer potenzialmente esterni all'intervallo in valori <xref:System.Int32>.  
  
 [!code-csharp[Conceptual.Conversion#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#4)]
 [!code-vb[Conceptual.Conversion#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#4)]  
  
 Le conversioni esplicite possono produrre risultati diversi in linguaggi diversi e tali risultati possono differire dal valore restituito dal metodo <xref:System.Convert> corrispondente. Se, ad esempio, il valore <xref:System.Double> 12.63251 viene convertito in un tipo <xref:System.Int32>, sia il metodo `CInt` Visual Basic che il metodo <xref:System.Convert.ToInt32%28System.Double%29?displayProperty=fullName> .NET Framework arrotondano il valore <xref:System.Double> per restituire un valore di 13, mentre l'operatore `(int)` C\# tronca il valore <xref:System.Double> per restituire un valore di 12. Analogamente, l'operatore `(int)` C\# non supporta la conversione da valore booleano a valore intero, mentre il metodo `CInt` Visual Basic consente di convertire un valore `true` in \-1. Per contro, il metodo <xref:System.Convert.ToInt32%28System.Boolean%29?displayProperty=fullName> consente di convertire un valore `true` in 1.  
  
 La maggior parte dei compilatori consente l'esecuzione di conversioni esplicite in modalità controllata o non controllata. Quando viene eseguita una conversione controllata, viene generato un evento <xref:System.OverflowException> se il valore del tipo da convertire non rientra nell'intervallo del tipo di destinazione. Quando viene eseguita una conversione non controllata nelle stesse condizioni, potrebbe non venire generata un'eccezione, ma il comportamento esatto della conversione risulterà non definito e potrebbe venire restituito un valore non corretto.  
  
> [!NOTE]
>  In C\# è possibile eseguire conversioni controllate utilizzando la parola chiave `checked` con l'operatore di cast o specificando l'opzione del compilatore `/checked+`. Viceversa, le conversioni in modalità non controllata possono essere eseguite utilizzando la parola chiave `unchecked` con l'operatore di cast o specificando l'opzione del compilatore `/checked-`. Per impostazione predefinita, le conversioni esplicite vengono eseguite in modalità non controllata. In Visual Basic è possibile eseguire conversioni in modalità controllata deselezionando la casella di controllo **Rimuovi controllo dell'overflow di Integer** nella finestra di dialogo **Impostazioni del compilatore avanzate** del progetto o specificando l'opzione del compilatore `/removeintchecks-`. Viceversa, le conversioni non controllate possono essere eseguite selezionando la casella di controllo **Rimuovi controllo dell'overflow di Integer** nella finestra di dialogo **Impostazioni del compilatore avanzate** del progetto o specificando l'opzione del compilatore `/removeintchecks+`. Per impostazione predefinita, le conversioni esplicite vengono eseguite in modalità controllata.  
  
 Nell'esempio C\# seguente vengono utilizzate le parole chiave `checked` e `unchecked` per illustrare la differenza nel comportamento quando un valore al di fuori dell'intervallo di un tipo <xref:System.Byte> viene convertito in <xref:System.Byte>. La conversione controllata genera un'eccezione, mentre la conversione non controllata assegna <xref:System.Byte.MaxValue?displayProperty=fullName> alla variabile <xref:System.Byte>.  
  
 [!code-csharp[Conceptual.Conversion#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#12)]  
  
 Se un determinato compilatore di linguaggio supporta gli operatori di overload personalizzati, è anche possibile definire conversioni esplicite nei tipi personalizzati. Nell'esempio seguente viene fornita un'implementazione parziale di un tipo di dati Signed Byte denominato `ByteWithSign` che utilizza la rappresentazione di segno e grandezza. Il tipo supporta la conversione esplicita di valori <xref:System.Int32> e <xref:System.UInt32> in valori `ByteWithSign`.  
  
 [!code-csharp[Conceptual.Conversion#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#5)]
 [!code-vb[Conceptual.Conversion#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#5)]  
  
 Il codice client può quindi dichiarare una variabile `ByteWithSign` e assegnare a essa valori <xref:System.Int32> e <xref:System.UInt32> se le assegnazioni includono un operatore di cast o un metodo di conversione, come illustrato nell'esempio seguente.  
  
 [!code-csharp[Conceptual.Conversion#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/explicit1.cs#6)]
 [!code-vb[Conceptual.Conversion#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/explicit1.vb#6)]  
  
 [Torna all'inizio](#top)  
  
<a name="the_iconvertible_interface"></a>   
## Interfaccia IConvertible  
 Per supportare la conversione di un tipo qualsiasi in un tipo di base Common Language Runtime, in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] è disponibile l'interfaccia <xref:System.IConvertible>. È necessario che il tipo di implementazione fornisca gli elementi seguenti:  
  
-   Un metodo che restituisce l'oggetto <xref:System.TypeCode> del tipo di implementazione.  
  
-   Metodi per convertire il tipo di implementazione in ognuno dei tipi di base di Common Language Runtime \(<xref:System.Boolean>, <xref:System.Byte>, <xref:System.DateTime><xref:System.Decimal>, <xref:System.Double> e così via\).  
  
-   Un metodo di conversione generalizzato per convertire un'istanza del tipo di implementazione in un altro tipo specificato. Le conversioni non supportate devono generare un evento <xref:System.InvalidCastException>.  
  
 Ogni tipo di base di Common Language Runtime \(ovvero <xref:System.Boolean>, <xref:System.Byte>, <xref:System.Char>, <xref:System.DateTime>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.String>, <xref:System.UInt16>, <xref:System.UInt32> e <xref:System.UInt64>\) nonché i tipi <xref:System.DBNull> e <xref:System.Enum>, implementano l'interfaccia <xref:System.IConvertible>. Si tratta tuttavia di implementazioni esplicite dell'interfaccia. Il metodo di conversione può essere chiamato solo tramite una variabile dell'interfaccia <xref:System.IConvertible>, come illustrato nell'esempio seguente. In questo esempio viene convertito un valore <xref:System.Int32> nel valore <xref:System.Char> equivalente.  
  
 [!code-csharp[Conceptual.Conversion#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible1.cs#7)]
 [!code-vb[Conceptual.Conversion#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible1.vb#7)]  
  
 Il requisito che il metodo di conversione venga chiamato sull'interfaccia anziché sul tipo di implementazione rende relativamente costose le implementazioni esplicite dell'interfaccia. È invece consigliabile chiamare il membro appropriato della classe <xref:System.Convert> per eseguire la conversione tra tipi di base di Common Language Runtime. Per ulteriori informazioni, vedere la sezione successiva, [Classe Convert](#Convert).  
  
> [!NOTE]
>  Oltre all'interfaccia <xref:System.IConvertible> e alla classe <xref:System.Convert> fornite da [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], nei singoli linguaggi possono essere disponibili altre modalità per eseguire le conversioni. In C\# vengono ad esempio utilizzati gli operatori di cast mentre in Visual Basic vengono utilizzate funzioni di conversione implementate dal compilatore quali `CType`, `CInt` e `DirectCast`.  
  
 L'interfaccia <xref:System.IConvertible> è principalmente progettata per supportare la conversione tra tipi di base in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. L'interfaccia può tuttavia anche essere implementata da un tipo personalizzato per supportare la conversione di tale tipo in altri tipi personalizzati. Per ulteriori informazioni, vedere la sezione [Conversioni personalizzate con il metodo ChangeType](#ChangeType) più avanti in questo argomento.  
  
 [Torna all'inizio](#top)  
  
<a name="Convert"></a>   
## Classe Convert  
 Benché sia possibile chiamare l'implementazione dell'interfaccia <xref:System.IConvertible> di ogni tipo di base per eseguire una conversione di tipi, il modo indipendente dal linguaggio consigliato per convertire un tipo di base in un altro consiste nel chiamare i metodi della classe <xref:System.Convert?displayProperty=fullName>. È inoltre possibile utilizzare il metodo <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=fullName> per eseguire la conversione da un tipo personalizzato specificato a un altro.  
  
### Conversioni tra tipi di base  
 La classe <xref:System.Convert> consente di eseguire conversioni indipendenti dal linguaggio tra tipi di base ed è disponibile in tutti i linguaggi destinati a Common Language Runtime. Questa classe fornisce un set completo di metodi per le conversioni verso un tipo di dati più piccolo e per le conversioni verso un tipo di dati più grande e genera un evento <xref:System.InvalidCastException> per le conversioni non supportate \(ad esempio la conversione di un valore <xref:System.DateTime> in un valore intero\). Le conversioni verso un tipo di dati più piccolo vengono eseguite in un contesto controllato \(checked\) e, se la conversione ha esito negativo, viene generato un evento <xref:System.OverflowException>.  
  
> [!IMPORTANT]
>  Poiché la classe <xref:System.Convert> include metodi per la conversione in e da ogni tipo di base, non occorre chiamare l'implementazione esplicita dell'interfaccia <xref:System.IConvertible> di ogni tipo di base.  
  
 Nell'esempio seguente viene illustrato l'utilizzo della classe <xref:System.Convert?displayProperty=fullName> per eseguire diverse conversioni verso un tipo di dati più grande e più piccolo tra tipi di base .NET Framework.  
  
 [!code-csharp[Conceptual.Conversion#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/convert1.cs#8)]
 [!code-vb[Conceptual.Conversion#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/convert1.vb#8)]  
  
 Talvolta, in particolare nel caso di conversione verso e da valori a virgola mobile, una conversione può comportare una perdita di precisione, anche se non viene generato un evento <xref:System.OverflowException>. Nell'esempio seguente viene illustrata questa perdita di precisione. Nel primo caso, un valore <xref:System.Decimal> è meno preciso \(meno cifre significative\) quando viene convertito in <xref:System.Double>. Nel secondo caso, un valore <xref:System.Double> viene arrotondato da 42,72 a 43 per completare la conversione.  
  
 [!code-csharp[Conceptual.Conversion#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/convert1.cs#9)]
 [!code-vb[Conceptual.Conversion#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/convert1.vb#9)]  
  
 Per consultare una tabella in cui sono elencate le conversioni verso un tipo di dati più piccolo e più grande supportate dalla classe <xref:System.Convert>, vedere [Tabelle di conversione di tipi](../../../docs/standard/base-types/conversion-tables.md).  
  
<a name="ChangeType"></a>   
### Conversioni personalizzate con il metodo ChangeType  
 Oltre a supportare le conversioni in ognuno dei tipi di base, la classe <xref:System.Convert> può essere utilizzata per convertire un tipo personalizzato in uno o più tipi predefiniti. Questa conversione viene eseguita dal metodo <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=fullName> che a sua volta esegue il wrapping di una chiamata al metodo <xref:System.IConvertible.ToType%2A?displayProperty=fullName> del parametro `value`. Questo significa che l'oggetto rappresentato dal parametro `value` deve fornire un'implementazione dell'interfaccia <xref:System.IConvertible>.  
  
> [!NOTE]
>  Poiché i metodi <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%29?displayProperty=fullName> e di <xref:System.Convert.ChangeType%28System.Object%2CSystem.Type%2CSystem.IFormatProvider%29?displayProperty=fullName> utilizzano un oggetto <xref:System.Type> per specificare il tipo di destinazione in cui `value` viene convertito, possono essere utilizzati per eseguire una conversione dinamica a un oggetto il cui tipo non è noto in fase di compilazione. Tuttavia, si noti che l'implementazione <xref:System.IConvertible> di `value` deve comunque supportare questa conversione.  
  
 Nell'esempio seguente viene illustrata una possibile implementazione dell'interfaccia <xref:System.IConvertible> che consente la conversione di un oggetto `TemperatureCelsius` in un oggetto `TemperatureFahrenheit` e viceversa. Nell'esempio viene definita una classe di base, `Temperature`, che implementa l'interfaccia <xref:System.IConvertible> ed esegue l'override del metodo <xref:System.Object.ToString%2A?displayProperty=fullName>. Le classi `TemperatureCelsius` e `TemperatureFahrenheit` derivate eseguono ognuna l'override dei metodi `ToType` e `ToString` della classe di base.  
  
 [!code-csharp[Conceptual.Conversion#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible2.cs#10)]
 [!code-vb[Conceptual.Conversion#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible2.vb#10)]  
  
 Nell'esempio seguente vengono illustrate diverse chiamate a queste implementazioni di <xref:System.IConvertible> per convertire oggetti `TemperatureCelsius` in oggetti `TemperatureFahrenheit` e viceversa.  
  
 [!code-csharp[Conceptual.Conversion#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.conversion/cs/iconvertible2.cs#11)]
 [!code-vb[Conceptual.Conversion#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.conversion/vb/iconvertible2.vb#11)]  
  
 [Torna all'inizio](#top)  
  
<a name="the_typeconverter_class"></a>   
## Classe TypeConverter  
 In .NET Framework è anche possibile definire un convertitore di tipi per un tipo personalizzato mediante l'estensione della classe <xref:System.ComponentModel.TypeConverter?displayProperty=fullName> e l'associazione del convertitore di tipi al tipo tramite un attributo <xref:System.ComponentModel.TypeConverterAttribute?displayProperty=fullName>. Nella tabella seguente sono evidenziate le differenze tra questo approccio e l'implementazione dell'interfaccia <xref:System.IConvertible> per un tipo personalizzato.  
  
> [!NOTE]
>  È possibile fornire supporto per un tipo personalizzato in fase di progettazione solo se per tale tipo è stato definito un convertitore di tipi.  
  
|Conversione mediante TypeConverter|Conversione mediante IConvertible|  
|----------------------------------------|---------------------------------------|  
|Implementata per un tipo personalizzato derivando una classe separata da <xref:System.ComponentModel.TypeConverter>. Questa classe derivata viene associata al tipo personalizzato applicando un attributo <xref:System.ComponentModel.TypeConverterAttribute>.|Implementata da un tipo personalizzato per eseguire la conversione. È necessario che un utente di tale tipo richiami sul tipo stesso un metodo di conversione <xref:System.IConvertible>.|  
|Utilizzabile sia in fase di progettazione che in fase di esecuzione.|Utilizzabile solo in fase di esecuzione.|  
|Utilizza la reflection ed è quindi più lenta della conversione consentita da <xref:System.IConvertible>.|Non utilizza la reflection.|  
|Consente di eseguire conversioni bidirezionali, dal tipo personalizzato ad altri tipi di dati e da altri tipi di dati al tipo personalizzato. Un oggetto <xref:System.ComponentModel.TypeConverter> definito per `MyType` consente ad esempio le conversioni da `MyType` a <xref:System.String> e da <xref:System.String> a `MyType`.|Consente la conversione da un tipo personalizzato ad altri tipi di dati, ma non da altri tipi di dati al tipo personalizzato.|  
  
 Per ulteriori informazioni sull'utilizzo di convertitori di tipi per l'esecuzione di conversioni, vedere <xref:System.ComponentModel.TypeConverter?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Convert?displayProperty=fullName>   
 <xref:System.IConvertible>   
 [Tabelle di conversione dei tipi](../../../docs/standard/base-types/conversion-tables.md)