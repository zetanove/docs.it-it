---
title: "Serializzazione a tolleranza di versione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "BinaryFormatter (classe), esempi"
  - "serializzazione, attributi"
  - "serializzazione, controllo"
  - "serializzazione, serializzazione personalizzata"
  - "serializzazione, tolleranza di versione"
  - "serializzazione a tolleranza di versione"
  - "versioni e serializzazione"
ms.assetid: bea0ffe3-2708-4a16-ac7d-e586ed6b8e8d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Serializzazione a tolleranza di versione
Nelle versioni 1.0 e 1.1 di .NET Framework la creazione di tipi serializzabili riutilizzabili da una versione di un'applicazione alla versione successiva risulta problematica.Se un tipo veniva modificato aggiungendo campi aggiuntivi, si verificavano i seguenti problemi:  
  
-   Le versioni precedenti di un'applicazione avrebbero generato eccezioni durante la richiesta di deserializzazione delle nuove versioni del tipo obsoleto.  
  
-   Le versioni più recenti di un'applicazione avrebbero generato eccezioni durante la deserializzazione delle versioni precedenti di un tipo con dati mancanti.  
  
 La Serializzazione a tolleranza di versione \(VTS, Version Tolerant Serialization\) è un set di funzionalità introdotto in .NET Framework 2.0 che semplifica, nel tempo, la modifica dei tipi serializzabili.In particolare, le funzionalità VTS vengono abilitate per le classi alle quali è stato applicato l'attributo <xref:System.SerializableAttribute>, inclusi i tipi generici.VTS rende possibile l'aggiunta di nuovi campi a tali classi senza compromettere la compatibilità con le altre versioni del tipo.Per un'applicazione di esempio funzionante, vedere [Esempio di tecnologia di serializzazione indipendente dalla versione](../../../docs/framework/serialization/version-tolerant-serialization-technology-sample.md).  
  
 Le funzionalità VTS vengono abilitate durante l'utilizzo di <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.Inoltre, durante l'utilizzo di <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>, sono abilitate tutte le funzionalità salvo la tolleranza di dati estranei.Per ulteriori informazioni sull'utilizzo di tali classi per la serializzazione, vedere [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md).  
  
## Elenco delle funzionalità  
 Il set di funzionalità comprende quanto segue:  
  
-   Tolleranza di dati estranei o imprevisti.Consente a versioni più recenti del tipo di inviare dati alle versioni precedenti.  
  
-   Tolleranza di dati facoltativi mancanti.Consente a versioni precedenti di inviare dati alle versioni più recenti.  
  
-   Callback di serializzazione.Consente l'impostazione intelligente del valore predefinito nei casi in cui dei dati siano mancanti.  
  
 In aggiunta, è presente una funzionalità che consente di dichiarare l'aggiunta di un nuovo campo facoltativo.Questa è la proprietà <xref:System.Runtime.Serialization.OptionalFieldAttribute.VersionAdded%2A> dell'attributo <xref:System.Runtime.Serialization.OptionalFieldAttribute>.  
  
 Queste funzionalità vengono discusse in dettaglio di seguito.  
  
## Tolleranza di dati estranei o imprevisti  
 In passato, durante la serializzazione, la presenza di dati estranei o imprevisti generava eccezioni.Con VTS, nella stessa situazione, eventuali dati estranei o imprevisti vengono ignorati piuttosto che generare eccezioni.Ciò consente alle applicazioni che utilizzano versioni più recenti di un tipo \(ovvero una versione che include più campi\) di inviare informazioni alle applicazioni che prevedono versioni precedenti dello stesso tipo.  
  
 Nell'esempio riportato di seguito, i dati aggiuntivi contenuti in `CountryField` della versione 2.0 della classe `Address` vengono ignorati nel momento in cui un'applicazione precedente deserializza la versione più recente.  
  
```csharp  
// Version 1 of the Address class.  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
}  
// Version 2.0 of the Address class.  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
    // The older application ignores this data.  
    public string CountryField;  
}  
```  
  
```vb  
' Version 1 of the Address class.  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
End Class  
  
' Version 2.0 of the Address class.  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
    ' The older application ignores this data.  
    Public CountryField As String  
End Class  
```  
  
## Tolleranza di dati mancanti  
 I campi possono essere contrassegnati come facoltativi applicando ad essi l'attributo <xref:System.Runtime.Serialization.OptionalFieldAttribute>.Durante la deserializzazione, se i dati facoltativi risultano mancanti, il motore di serializzazione ignora tale assenza e non genera eccezioni.In tal modo, le applicazioni che prevedono versioni precedenti di un tipo, possono inviare dati ad applicazioni che prevedono versioni più recenti dello stesso tipo.  
  
 Nell'esempio riportato di seguito viene mostrata la versione 2.0 della classe `Address` con il campo `CountryField` contrassegnato come facoltativo.Se un'applicazione precedente invia la versione 1 a un'applicazione più recente che prevede la versione 2.0, l'assenza dei dati viene ignorata.  
  
```csharp  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
  
    [OptionalField]  
    public string CountryField;  
}  
```  
  
```vb  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
  
    <OptionalField> _  
    Public CountryField As String  
End Class  
```  
  
## Callback di serializzazione  
 I callback di serializzazione rappresentano un meccanismo che fornisce hook nel processo di serializzazione\/deserializzazione in quattro punti.  
  
|Attributo|Quando viene chiamato il metodo associato|Utilizzo tipico|  
|---------------|-----------------------------------------------|---------------------|  
|<xref:System.Runtime.Serialization.OnDeserializingAttribute>|Prima della deserializzazione.\*|Inizializzare i valori predefiniti per i campi facoltativi.|  
|<xref:System.Runtime.Serialization.OnDeserializedAttribute>|Dopo la deserializzazione.|Correggere i valori dei campi facoltativi in base al contenuto di altri campi.|  
|<xref:System.Runtime.Serialization.OnSerializingAttribute>|Prima della serializzazione.|Preparare per la serializzazione.Ad esempio, la creazione di strutture di dati facoltativi.|  
|<xref:System.Runtime.Serialization.OnSerializedAttribute>|Dopo la serializzazione.|Registrare gli eventi di serializzazione.|  
  
 \* Questo callback viene richiamato prima del costruttore di deserializzazione, se presente.  
  
### Utilizzo dei callback  
 Per utilizzare i callback, applicare l'attributo appropriato a un metodo che accetta un parametro <xref:System.Runtime.Serialization.StreamingContext>.È possibile contrassegnare solo uno metodo per classe con ciascuno di questi attributi.Ad esempio:  
  
```csharp  
[OnDeserializing]  
private void SetCountryRegionDefault(StreamingContext sc)  
{  
    CountryField = "Japan";  
}  
  
```  
  
```vb  
<OnDeserializing>  
Private Sub SetCountryRegionDefault(StreamingContext sc)  
    CountryField = "Japan";  
End Sub  
```  
  
 L'utilizzo di questi metodi è destinato al controllo la versione.Durante la deserializzazione, un campo facoltativo potrebbe non essere inizializzato correttamente nel caso in cui i dati del campo risultino mancanti.Ciò può essere corretto creando il metodo che assegna il valore corretto e applicando l'attributo **OnDeserializingAttribute** o **OnDeserializedAttribute** al metodo.  
  
 Nell'esempio riportato di seguito, viene mostrato il metodo nel contesto di un tipo.Se una versione precedente di un'applicazione invia un'istanza della classe `Address` a una versione più recente dell'applicazione, i dati del campo `CountryField` risulteranno mancanti.Tuttavia dopo la deserializzazione, il campo verrà impostato su un valore predefinito "Giappone".  
  
```csharp  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
    [OptionalField]  
    public string CountryField;  
  
    [OnDeserializing]  
    private void SetCountryRegionDefault (StreamingContext sc)  
    {  
        CountryField = "Japan";  
    }  
}  
  
```  
  
```vb  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
    <OptionalField> _  
    Public CountryField As String  
  
    <OnDeserializing> _  
    Private Sub SetCountryRegionDefault(StreamingContext sc)  
        CountryField = "Japan";  
    End Sub  
End Class  
```  
  
## Proprietà VersionAdded  
 **OptionalFieldAttribute** dispone della proprietà **VersionAdded**.In .NET Framework versione 2.0, tale proprietà non viene utilizzata.È tuttavia importante impostare correttamente questa proprietà in modo da essere certi che il tipo sia compatibile con i motori di serializzazione futuri.  
  
 La proprietà indica quale versione di un tipo di un determinato campo è stata aggiunta.È necessario che venga incrementato esattamente di uno \(a partire da 2\) ogni volta che viene modificato il tipo, come mostra l'esempio riportato di seguito:  
  
```csharp  
// Version 1.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
}  
  
// Version 2.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
  
    [OptionalField(VersionAdded = 2)]  
    public string NickName;  
    [OptionalField(VersionAdded = 2)]  
    public DateTime BirthDate;  
}  
  
// Version 3.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
  
    [OptionalField(VersionAdded=2)]  
    public string NickName;  
    [OptionalField(VersionAdded=2)]  
    public DateTime BirthDate;  
  
    [OptionalField(VersionAdded=3)]  
    public int Weight;  
}  
```  
  
```vb  
' Version 1.0  
<Serializable> _  
Public Class Person  
    Public FullName  
End Class  
  
' Version 2.0  
<Serializable> _  
Public Class Person  
    Public FullName As String  
  
    <OptionalField(VersionAdded := 2)> _  
    Public NickName As String  
    <OptionalField(VersionAdded := 2)> _  
    Public BirthDate As DateTime  
End Class  
  
' Version 3.0  
<Serializable> _  
Public Class Person  
    Public FullName As String  
  
    <OptionalField(VersionAdded := 2)> _  
    Public NickName As String  
    <OptionalField(VersionAdded := 2)> _  
    Public BirthDate As DateTime  
  
    <OptionalField(VersionAdded := 3)> _  
    Public Weight As Integer  
End Class  
```  
  
## SerializationBinder  
 In alcuni casi potrebbe essere necessario controllare le classi da serializzare e deserializzare ad esempio perché sono richieste versioni diverse della classe sul server e sul client.<xref:System.RuntimeSerialization.SerializationBinder> è una classe astratta utilizzata per controllare i tipi effettivi utilizzati durante la serializzazione e la deserializzazione.Per utilizzare questa classe, derivare una classe da <xref:System.RuntimeSerialization.SerializationBinder> e ignorare i metodi <xref:System.Runtime.Serialization.SerializationBinder.BindToName%2A> System.String, System.String)?qualifyHint=False&autoUpgrade=True e <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> System.String)?qualifyHint=False&autoUpgrade=True.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Controllo di serializzazione e deserializzazione con SerializationBinder](../../../docs/framework/wcf/feature-details/controlling-serialization-and-deserialization-with-serializationbinder.md).  
  
## Suggerimenti  
 Per essere certi del comportamento corretto del controllo della versione, attenersi a queste regole durante la modifica di un tipo da una versione a un'altra:  
  
-   Non rimuovere mai un campo serializzato.  
  
-   Non applicare mai l'attributo <xref:System.NonSerializedAttribute> a un campo se l'attributo non è stato applicato al campo nella versione precedente.  
  
-   Non modificare mai il nome o il tipo di un campo serializzato.  
  
-   Durante l'aggiunta di un nuovo campo serializzato, applicare l'attributo **OptionalFieldAttribute**.  
  
-   Durante la rimozione di un attributo **NonSerializedAttribute** da un campo \(non serializzabile nella versione precedente\), applicare l'attributo **OptionalFieldAttribute**.  
  
-   Per tutti i campi facoltativi, impostare valori predefiniti significativi tramite l'utilizzo di callback di serializzazione, a meno che non risultino accettabili 0 o **null** come valori predefiniti.  
  
 Per essere certi che un tipo sia compatibile con i motori di serializzazione futuri, seguire le linee guida riportate di seguito:  
  
-   Impostare sempre la proprietà **VersionAdded** sull'attributo **OptionalFieldAttribute** in modo corretto.  
  
-   Evitare controlli di versione sottoposti a branching.  
  
## Vedere anche  
 <xref:System.SerializableAttribute>   
 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>   
 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>   
 <xref:System.Runtime.Serialization.OptionalFieldAttribute.VersionAdded%2A>   
 <xref:System.Runtime.Serialization.OptionalFieldAttribute>   
 <xref:System.Runtime.Serialization.OnDeserializingAttribute>   
 <xref:System.Runtime.Serialization.OnDeserializedAttribute>   
 <xref:System.Runtime.Serialization.OnDeserializingAttribute>   
 <xref:System.Runtime.Serialization.OnSerializedAttribute>   
 <xref:System.Runtime.Serialization.StreamingContext>   
 <xref:System.NonSerializedAttribute>   
 [Serializzazione binaria](../../../docs/framework/serialization/binary-serialization.md)