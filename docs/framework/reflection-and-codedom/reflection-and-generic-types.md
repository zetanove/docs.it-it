---
title: "Reflection and Generic Types | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "generics [.NET Framework], reflection emit"
  - "reflection emit, generic types"
  - "reflection, generic types"
  - "type arguments"
  - "generics [.NET Framework], reflection"
  - "viewing type information"
  - "type information, viewing"
  - "types, generic"
  - "type parameters"
ms.assetid: f7180fc5-dd41-42d4-8a8e-1b34288e06de
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Reflection and Generic Types
<a name="top"></a> Dal punto di vista della reflection, un tipo ordinario si differenzia da un tipo generico perché quest'ultimo è associato a un insieme di parametri di tipo, se è una definizione di tipo generico, o a un insieme di argomenti di tipo, se è un tipo costruito. Un metodo generico si differenzia da un metodo ordinario esattamente nello stesso modo.  
  
 Per comprendere come i tipi e i metodi generici vengono gestiti dalla reflection, è opportuno considerare due fattori fondamentali:  
  
-   I parametri di tipo delle definizioni di tipo e di metodo generico sono rappresentati da istanze della classe <xref:System.Type>.  
  
    > [!NOTE]
    >  Numerosi metodi e proprietà di <xref:System.Type> hanno un comportamento diverso quando un oggetto <xref:System.Type> rappresenta un parametro di tipo generico. Queste differenze sono illustrate negli argomenti relativi alle proprietà e ai metodi in questione. Vedere ad esempio <xref:System.Type.IsAutoClass%2A> e <xref:System.Type.DeclaringType%2A>.  Inoltre, alcuni membri sono validi solo quando un oggetto <xref:System.Type> rappresenta un parametro di tipo generico. Ad esempio, vedere <xref:System.Type.GetGenericTypeDefinition%2A>.  
  
-   Se un'istanza di <xref:System.Type> rappresenta un tipo generico, includerà una matrice di tipi che rappresentano i parametri di tipo \(per le definizioni di tipo generico\) o gli argomenti di tipo \(per i tipi costruiti\). Questo è vero anche per un'istanza della classe <xref:System.Reflection.MethodInfo> che rappresenta un metodo generico.  
  
 La reflection fornisce metodi di <xref:System.Type> e <xref:System.Reflection.MethodInfo> che consentono di accedere alla matrice di parametri di tipo e stabilire se un'istanza di <xref:System.Type> rappresenta un parametro di tipo o un tipo effettivo.  
  
 Per un codice di esempio che illustra i metodi descritti in questo argomento, vedere [How to: Examine and Instantiate Generic Types with Reflection](../../../docs/framework/reflection-and-codedom/how-to-examine-and-instantiate-generic-types-with-reflection.md).  
  
 Nelle considerazioni che seguono si presuppone la conoscenza della terminologia relativa ai generics, ad esempio la differenza tra argomenti e parametri di tipo e quella tra tipi costruiti aperti o chiusi. Per altre informazioni, vedere [Generics](../../../docs/standard/generics/index.md).  
  
 Questa panoramica include le sezioni seguenti:  
  
-   [Come stabilire se un tipo o un metodo è generico](#is_this_a_generic_type_or_method)  
  
-   [Generazione di tipi generici chiusi](#generating_closed_generic_types)  
  
-   [Analisi degli argomenti e dei parametri di tipo](#examining_type_arguments)  
  
-   [Invarianti](#invariants)  
  
-   [Argomenti correlati](#related_topics)  
  
<a name="is_this_a_generic_type_or_method"></a>   
## Come stabilire se un tipo o un metodo è generico  
 Quando si esamina un tipo sconosciuto rappresentato da un'istanza di <xref:System.Type> tramite la reflection, usare la proprietà <xref:System.Type.IsGenericType%2A> per stabilire se il tipo sconosciuto è generico. Se il tipo è generico, restituisce `true`. In modo analogo, quando si esamina un metodo sconosciuto rappresentato da un'istanza della classe <xref:System.Reflection.MethodInfo>, usare la proprietà <xref:System.Reflection.MethodInfo.IsGenericMethod%2A> per stabilire se il metodo è generico.  
  
### Come stabilire se un oggetto rappresenta una definizione di metodo o di tipo generico  
 Usare la proprietà <xref:System.Type.IsGenericTypeDefinition%2A> per stabilire se un oggetto <xref:System.Type> rappresenta una definizione di tipo generico e il metodo <xref:System.Reflection.MethodInfo.IsGenericMethodDefinition%2A> per determinare se un oggetto <xref:System.Reflection.MethodInfo> rappresenta una definizione di metodo generico.  
  
 Le definizioni di metodo e di tipo generico costituiscono i modelli a partire dai quali vengono creati i tipi istanziabili. I tipi generici nella libreria di classi .NET Framework, ad esempio <xref:System.Collections.Generic.Dictionary%602>, sono definizioni di tipo generico.  
  
### Come stabilire se un tipo o un metodo è aperto o chiuso  
 Un tipo o un metodo generico è chiuso se tutti i relativi parametri di tipo, inclusi tutti i parametri di tipo di tutti i tipi di inclusione, sono stati sostituiti da tipi istanziabili. È possibile creare un'istanza di un tipo generico solo se è chiuso. Se un tipo è aperto, la proprietà <xref:System.Type.ContainsGenericParameters%2A?displayProperty=fullName> restituisce `true`. Per i metodi, la stessa funzione viene eseguita dal metodo <xref:System.Reflection.MethodInfo.ContainsGenericParameters%2A?displayProperty=fullName>.  
  
 [Torna all'inizio](#top)  
  
<a name="generating_closed_generic_types"></a>   
## Generazione di tipi generici chiusi  
 Dopo avere ottenuto una definizione di metodo o di tipo generico, usare il metodo <xref:System.Type.MakeGenericType%2A> per creare un tipo generico chiuso oppure il metodo <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A> per creare un oggetto <xref:System.Reflection.MethodInfo> relativo a un metodo generico chiuso.  
  
### Recupero della definizione di tipo o di metodo generico  
 Se è disponibile un tipo o di un metodo generico aperto che non è una definizione di tipo o di metodo generico, non è possibile crearne istanze né specificare i parametri di tipo mancanti. A questo scopo è necessario avere una definizione di tipo o di metodo generico. Usare il metodo <xref:System.Type.GetGenericTypeDefinition%2A> per ottenere la definizione di tipo generico o il metodo <xref:System.Reflection.MethodInfo.GetGenericMethodDefinition%2A> per ottenere la definizione di metodo generico.  
  
 Ad esempio, se si ha un oggetto <xref:System.Type> che rappresenta `Dictionary<int, string>` \(`Dictionary(Of Integer, String)` in Visual Basic\) e si vuole creare il tipo `Dictionary<string, MyClass>`, è possibile usare il metodo <xref:System.Type.GetGenericTypeDefinition%2A> per ottenere un oggetto <xref:System.Type> che rappresenta `Dictionary<TKey, TValue>` e quindi il metodo <xref:System.Type.MakeGenericType%2A> per generare un oggetto <xref:System.Type> che rappresenta `Dictionary<int, MyClass>`.  
  
 Per un esempio di tipo generico aperto che non è un tipo generico, vedere la sezione "Parametro di tipo o argomento di tipo" più avanti in questo argomento.  
  
 [Torna all'inizio](#top)  
  
<a name="examining_type_arguments"></a>   
## Analisi degli argomenti e dei parametri di tipo  
 Usare il metodo <xref:System.Type.GetGenericArguments%2A?displayProperty=fullName> per ottenere una matrice di oggetti <xref:System.Type> che rappresentano i parametri o gli argomenti di tipo di un tipo generico e il metodo <xref:System.Reflection.MethodInfo.GetGenericArguments%2A?displayProperty=fullName> per eseguire la stessa operazione per un metodo generico.  
  
 Dopo avere stabilito che l'oggetto <xref:System.Type> rappresenta un parametro di tipo, la reflection consentirà di ottenere altre informazioni al riguardo. È possibile determinare l'origine, la posizione e i vincoli del parametro di tipo.  
  
### Parametro di tipo o argomento di tipo  
 Per stabilire se un determinato elemento della matrice è un parametro di tipo oppure un argomento di tipo, usare la proprietà <xref:System.Type.IsGenericParameter%2A>. Se l'elemento è un parametro di tipo, la proprietà <xref:System.Type.IsGenericParameter%2A> restituisce `true`.  
  
 Un tipo generico può essere aperto senza essere una definizione di tipo generico, nel qual caso presenterà sia argomenti di tipo che parametri di tipo. Ad esempio, nel codice seguente la classe `D` deriva da un tipo creato sostituendo il primo parametro di tipo `D` al secondo parametro di tipo `B`.  
  
```csharp  
class B<T, U> {} class D<V, W> : B<int, V> {}  
```  
  
```vb  
Class B(Of T, U) End Class Class D(Of V, W) Inherits B(Of Integer, V) End Class  
```  
  
```cpp#  
generic<typename T, typename U> ref class B {}; generic<typename V, typename W> ref class D : B<int, V> {};  
```  
  
 Se si ottiene un oggetto <xref:System.Type> che rappresenta `D<V, W>` e si usa la proprietà <xref:System.Type.BaseType%2A> per recuperarne il tipo di base, il `type B<int, V>` risultante sarà aperto, ma non sarà una definizione di tipo generico.  
  
### Origine di un parametro generico  
 Un parametro di tipo generico può provenire dal tipo in esame, da un tipo di inclusione o da un metodo generico.  È possibile determinarne l'origine nel modo seguente:  
  
-   Prima di tutto, usare la proprietà <xref:System.Type.DeclaringMethod%2A> per determinare se il parametro di tipo proviene da un metodo generico. Se il valore della proprietà non è un riferimento Null \(`Nothing` in Visual Basic\), l'origine è un metodo generico.  
  
-   Se l'origine non è un metodo generico, usare la proprietà <xref:System.Type.DeclaringType%2A> per determinare il tipo generico a cui appartiene il parametro di tipo generico.  
  
 Se il parametro di tipo appartiene a un metodo generico, la proprietà <xref:System.Type.DeclaringType%2A> restituisce il tipo che ha dichiarato tale metodo, che non è un'informazione rilevante.  
  
### Posizione di un parametro generico  
 In rare situazioni è necessario stabilire la posizione di un parametro di tipo nell'elenco dei parametri di tipo della classe dichiarante. Si supponga ad esempio di avere un oggetto <xref:System.Type> che rappresenta il tipo `B<int, V>` dell'esempio precedente. Il metodo <xref:System.Type.GetGenericArguments%2A> fornisce un elenco di argomenti di tipo ed è possibile determinare l'origine del parametro `V` in esame usando le proprietà <xref:System.Type.DeclaringMethod%2A> e <xref:System.Type.DeclaringType%2A>. È quindi possibile usare la proprietà <xref:System.Type.GenericParameterPosition%2A> per determinare la posizione del parametro nell'elenco dei parametri del tipo in cui il parametro è stato definito. In questo esempio, `V` si trova nella posizione 0 \(zero\) dell'elenco di parametri di tipo in cui è stato definito.  
  
### Vincoli di interfaccia e del tipo di base  
 Usare il metodo <xref:System.Type.GetGenericParameterConstraints%2A> per ottenere il vincolo del tipo di base e i vincoli di interfaccia di un parametro di tipo. L'ordine degli elementi della matrice non è significativo. Un elemento rappresenta un vincolo di interfaccia se è un tipo di interfaccia.  
  
### Attributi di parametri generici:  
 La proprietà <xref:System.Type.GenericParameterAttributes%2A> ottiene un valore <xref:System.Reflection.GenericParameterAttributes> che indica la varianza \(covarianza o controvarianza\) e i vincoli speciali di un parametro di tipo.  
  
#### Covarianza e controvarianza  
 Per determinare se un parametro di tipo sia covariante o controvariante, applicare la maschera <xref:System.Reflection.GenericParameterAttributes?displayProperty=fullName> al valore <xref:System.Reflection.GenericParameterAttributes> restituito dalla proprietà <xref:System.Type.GenericParameterAttributes%2A>. Se il risultato è <xref:System.Reflection.GenericParameterAttributes?displayProperty=fullName>, il parametro di tipo è invariante. Vedere [Covarianza e controvarianza](../../../docs/standard/generics/covariance-and-contravariance.md).  
  
#### Vincoli speciali  
 Per stabilire i vincoli speciali di un parametro di tipo, applicare la maschera <xref:System.Reflection.GenericParameterAttributes?displayProperty=fullName> al valore <xref:System.Reflection.GenericParameterAttributes> restituito dalla proprietà <xref:System.Type.GenericParameterAttributes%2A>. Se il risultato è <xref:System.Reflection.GenericParameterAttributes?displayProperty=fullName>, non sono presenti vincoli speciali. Un parametro di tipo può essere vincolato per essere un tipo di riferimento, un tipo di valore non nullable e per avere un costruttore predefinito.  
  
 [Torna all'inizio](#top)  
  
<a name="invariants"></a>   
## Invarianti  
 Per una tabella di condizioni non variabili associate a termini comuni nella reflection per tipi generici, vedere <xref:System.Type.IsGenericType%2A?displayProperty=fullName>. Per altri termini correlati ai metodi generici, vedere <xref:System.Reflection.MethodInfo.IsGenericMethod%2A?displayProperty=fullName>.  
  
 [Torna all'inizio](#top)  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[How to: Examine and Instantiate Generic Types with Reflection](../../../docs/framework/reflection-and-codedom/how-to-examine-and-instantiate-generic-types-with-reflection.md)|Mostra come usare le proprietà e i metodi di <xref:System.Type> e <xref:System.Reflection.MethodInfo> per esaminare i tipi generici.|  
|[Generics](../../../docs/standard/generics/index.md)|Descrive la funzionalità generics con la relativa modalità di supporto in .NET Framework.|  
|[How to: Define a Generic Type with Reflection Emit](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)|Mostra come usare la reflection emit per generate tipi generici in assembly dinamici.|  
|[Viewing Type Information](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)|Descrive la classe <xref:System.Type> e vengono forniti esempi di codice in cui viene descritto l'uso di <xref:System.Type> con diverse classi di reflection per ottenere informazioni su costruttori, metodi, campi, proprietà ed eventi.|