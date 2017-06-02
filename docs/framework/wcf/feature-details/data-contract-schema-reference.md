---
title: "Riferimento allo schema del contratto dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti dati [WCF], riferimento dello schema"
ms.assetid: 9ebb0ebe-8166-4c93-980a-7c8f1f38f7c0
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Riferimento allo schema del contratto dati
In questo argomento viene descritto il sottoinsieme dell'XML Schema \(XSD\) utilizzato da <xref:System.Runtime.Serialization.DataContractSerializer> per descrivere i tipi di Common Language Runtime \(CLR\) per la serializzazione XML.  
  
## Mapping DataContractSerializer  
 `DataContractSerializer` esegue il mapping di tipi CLR a XSD quando i metadati vengono esportati da un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] usando un endpoint di metadati o lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-serializer.md).  
  
 `DataContractSerializer` esegue, inoltre, il mapping di XSD ai tipi CLR quando viene utilizzato Svcutil.exe per accedere a documenti WSDL \(Web Services Description Language\) o XSD e generare contratti dati per servizi o client.  
  
 È possibile eseguire il mapping ai tipi CLR tramite `DataContractSerializer` solo delle istanze dell'XML Schema conformi ai requisiti indicati nel presente documento.  
  
### Livelli di supporto  
 `DataContractSerializer` fornisce i livelli di supporto seguenti per una determinata funzionalità dell'XML Schema:  
  
-   **Supportato**. È disponibile il mapping esplicito da questa funzionalità a tipi e\/o attributi CLR mediante `DataContractSerializer`.  
  
-   **Ignorato**. La funzionalità è consentita negli schemi importati da `DataContractSerializer`, ma non ha alcun effetto sulla generazione di codice.  
  
-   **Non consentito**.`DataContractSerializer` non supporta l'importazione di uno schema mediante la funzionalità. Svcutil.exe, ad esempio, quando si accede a un documento WSDL con uno schema che utilizza tale funzionalità, torna a utilizzare <xref:System.Xml.Serialization.XmlSerializer>. Questo accade per impostazione predefinita.  
  
## Informazioni generali  
  
-   Lo spazio dei nomi dello schema viene descritto nella pagina relativa a [XML Schema](http://go.microsoft.com/fwlink/?LinkId=95475). In questo documento viene utilizzato il prefisso "xs".  
  
-   Tutti gli attributi con un spazio dei nomi non di schema vengono ignorati.  
  
-   Tutte le annotazioni, ad eccezione di quelle descritte in questo documento, vengono ignorate.  
  
### \<xs:schema\>: attributi  
  
|Attributo|DataContract|  
|---------------|------------------|  
|`attributeFormDefault`|Ignorato.|  
|`blockDefault`|Ignorato.|  
|`elementFormDefault`|Deve essere qualificato. Per essere supportati da `DataContractSerializer`, tutti gli elementi devono essere qualificati per uno schema. Questo risultato può essere ottenuto impostando xs:schema\/@elementFormDefault o xs:element\/@form su "qualified" in ogni singola dichiarazione di elemento.|  
|`finalDefault`|Ignorato.|  
|`Id`|Ignorato.|  
|`targetNamespace`|Supportato e associato allo spazio dei nomi del contratto dati. Se questo attributo non viene specificato, viene utilizzato lo spazio dei nomi vuoto, che però non può essere lo spazio dei nomi riservato http:\/\/schemas.microsoft.com\/2003\/10\/Serialization\/.|  
|`version`|Ignorato.|  
  
### \<xs:schema\>: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`include`|Supportata.`DataContractSerializer` supporta xs:include e xs:import. Tuttavia, Svcutil.exe restringe i seguenti riferimenti `xs:include/@schemaLocation` e `xs:import/@location` quando i metadati vengono caricati da un file locale. In questo caso, l'elenco dei file di schema deve essere passato tramite un meccanismo fuori banda e non tramite `include`; i documenti dello schema `include` vengono ignorati.|  
|`redefine`|Non consentito. L'utilizzo di `xs:redefine` non è consentito da `DataContractSerializer` per motivi di sicurezza: `x:redefine` rende necessario seguire `schemaLocation`. In alcune circostanze, Svcutil.exe che utilizza DataContract restringe l'utilizzo di `schemaLocation`.|  
|`import`|Supportata.`DataContractSerializer` supporta `xs:include` e `xs:import`. Tuttavia, Svcutil.exe restringe i seguenti riferimenti `xs:include/@schemaLocation` e `xs:import/@location` quando i metadati vengono caricati da un file locale. In questo caso, l'elenco dei file di schema deve essere passato tramite un meccanismo fuori banda e non tramite `include`; i documenti dello schema `include` vengono ignorati.|  
|`simpleType`|Supportata. Vedere la sezione `xs:simpleType`.|  
|`complexType`|Supportato, esegue il mapping ai contratti dati. Vedere la sezione `xs:complexType`.|  
|`group`|Ignorato.`DataContractSerializer` non supporta l'utilizzo di `xs:group`, `xs:attributeGroup` e `xs:attribute`. Queste dichiarazioni vengono ignorate come elementi figlio di `xs:schema`, ma non è possibile fare riferimento a esse da `complexType` o da altri costrutti supportati.|  
|`attributeGroup`|Ignorato.`DataContractSerializer` non supporta l'utilizzo di `xs:group`, `xs:attributeGroup` e `xs:attribute`. Queste dichiarazioni vengono ignorate come elementi figlio di `xs:schema`, ma non è possibile fare riferimento a esse da `complexType` o da altri costrutti supportati.|  
|`element`|Supportata. Vedere Dichiarazione di elemento globale \(GED, Global Element Declaration\).|  
|`attribute`|Ignorato.`DataContractSerializer` non supporta l'utilizzo di `xs:group`, `xs:attributeGroup` e `xs:attribute`. Queste dichiarazioni vengono ignorate come elementi figlio di `xs:schema`, ma non è possibile fare riferimento a esse da `complexType` o da altri costrutti supportati.|  
|`notation`|Ignorato.|  
  
## Tipi complessi – \<xs:complexType\>  
  
### Informazioni generali  
 Ogni tipo complesso \<xs:complexType\> esegue il mapping a un contratto dati.  
  
### \<xs:complexType\>: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`abstract`|Deve essere false \(impostazione predefinita\)|  
|`block`|Non consentito.|  
|`final`|Ignorato.|  
|`id`|Ignorato.|  
|`mixed`|Deve essere false \(impostazione predefinita\)|  
|`name`|Supportato e associato al nome del contratto dati. Se nel nome sono presenti punti, viene effettuato il tentativo di eseguire il mapping del tipo a un tipo interno. Ad esempio, un tipo complesso denominato `A.B` esegue il mapping a un tipo di contratto dati che è un tipo interno di un tipo con il nome di contratto dati `A`, ma solo se tale tipo di contratto dati esiste. Possono esistere più livelli di annidamento: ad esempio, `A.B.C` può essere un tipo interno, ma solo se esistono sia `A` che `A.B`.|  
  
### \<xs:complexType\>: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`simpleContent`|Non sono consentite estensioni.<br /><br /> Sono consentite restrizioni solo da `anySimpleType`.|  
|`complexContent`|Supportata. Vedere "Ereditarietà".|  
|`group`|Non consentito.|  
|`all`|Non consentito.|  
|`choice`|Non consentito|  
|`sequence`|Supportato, esegue il mapping a membri dati di un contratto dati.|  
|`attribute`|Non consentito, anche se use \= "prohibited" \(con un'eccezione\). Sono supportati solo attributi facoltativi dello spazio dei nomi dello schema di serializzazione standard. Essi non eseguono il mapping ai membri dati nel modello di programmazione del contratto dati. Attualmente, solo uno di tali attributi ha significato e viene illustrato nella sezione ISerializable. Tutti gli altri vengono ignorati.|  
|`attributeGroup`|Non consentito. Nella versione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 1, `DataContractSerializer` ignora la presenza di `attributeGroup` in `xs:complexType`.|  
|`anyAttribute`|Non consentito.|  
|\(vuoto\)|Esegue il mapping a un contratto dati senza membri dati.|  
  
### \<xs:sequence\> in un tipo complesso: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`id`|Ignorato.|  
|`maxOccurs`|Deve essere 1 \(impostazione predefinita\)|  
|`minOccurs`|Deve essere 1 \(impostazione predefinita\)|  
  
### \<xs:sequence\> in un tipo complesso: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`element`|Ogni istanza esegue il mapping a un membro dati.|  
|`group`|Non consentito.|  
|`choice`|Non consentito.|  
|`sequence`|Non consentito.|  
|`any`|Non consentito.|  
|\(vuoto\)|Esegue il mapping a un contratto dati senza membri dati.|  
  
## Elementi – \<xs:element\>  
  
### Informazioni generali  
 `<xs:element>` può verificarsi nei contesti seguenti:  
  
-   Può verificarsi all'interno di un tag `<xs:sequence>` che descrive un membro dati di un contratto dati regolare \(non di raccolta\). In questo caso, l'attributo `maxOccurs` deve essere 1. Il valore 0 non è consentito.  
  
-   Può verificarsi all'interno di un tag `<xs:sequence>` che descrive un membro dati di un contratto dati di raccolta. In questo caso, l'attributo `maxOccurs` deve essere maggiore di 1 o "unbounded".  
  
-   Può verificarsi all'interno di un `<xs:schema>` come dichiarazione di elemento globale \(GED\).  
  
### \<xs:element\> con maxOccurs\=1 all'interno di un tag \<xs:sequence\> \(membri dati\)  
  
|Attributo|Schema|  
|---------------|------------|  
|`ref`|Non consentito.|  
|`name`|Supportato, esegue il mapping al nome del membro dati.|  
|`type`|Supportato, esegue il mapping al tipo del membro dati. Per ulteriori informazioni, vedere Mapping di tipi\/primitivi. Se non è specificato \(e se l'elemento non contiene un tipo anonimo\), viene presupposto `xs:anyType`.|  
|`block`|Ignorato.|  
|`default`|Non consentito.|  
|`fixed`|Non consentito.|  
|`form`|Deve essere qualificato. Questo attributo può essere impostato tramite `elementFormDefault` su `xs:schema`.|  
|`id`|Ignorato.|  
|`maxOccurs`|1|  
|`minOccurs`|Esegue il mapping alla proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> di un membro dati \(`IsRequired` è true quando `minOccurs` è 1\).|  
|`nillable`|Influenza il mapping dei tipi. Vedere Mapping di tipi\/primitivi.|  
  
### \<xs:element\> con maxOccurs\>1 all'interno di un tag \<xs:sequence\> \(raccolte\)  
  
-   Esegue il mapping a un <xref:System.Runtime.Serialization.CollectionDataContractAttribute>.  
  
-   Nei tipi di raccolta, è consentito un solo xs:element all'interno di un xs:sequence.  
  
 Le raccolte possono essere dei tipi seguenti:  
  
-   Raccolte regolari \(ad esempio, matrici\).  
  
-   Raccolte dizionario \(esecuzione del mapping di un valore all'altro; ad esempio, <xref:System.Collections.Hashtable>\).  
  
-   La sola differenza tra un dizionario e una matrice di un tipo di coppia chiave\/valore è nel modello di programmazione generato. Esiste un meccanismo di annotazione di schema che può essere utilizzato per indicare che un determinato tipo è una raccolta dizionario.  
  
 Le regole per gli attributi `ref`, `block`, `default`, `fixed`, `form` e `id` solo uguali a quelle valide per il caso non di raccolta. Tra gli altri attributi sono inclusi quelli riportati nella tabella seguente.  
  
|Attributo|Schema|  
|---------------|------------|  
|`name`|Supportato, esegue il mapping alla proprietà <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ItemName%2A> nell'attributo `CollectionDataContractAttribute`.|  
|`type`|Supportato, esegue il mapping al tipo memorizzato nella raccolta.|  
|`maxOccurs`|Maggiore di 1 o "unbounded". Lo schema DC deve utilizzare "unbounded".|  
|`minOccurs`|Ignorato.|  
|`nillable`|Influenza il mapping dei tipi. Questo attributo viene ignorato per le raccolte dizionario.|  
  
### \<xs:element\> all'interno di una dichiarazione di elemento globale \<xs:schema\>  
  
-   Una dichiarazione di elemento globale \(GED\) con lo stesso nome e lo stesso spazio dei nomi di un tipo nello schema, o che definisce un tipo anonimo al suo interno, viene definita come associata al tipo.  
  
-   Esportazione dello schema: vengono generate dichiarazioni di elementi globali associate per ogni tipo generato, sia semplice che complesso.  
  
-   Deserializzazione\/serializzazione: vengono utilizzate dichiarazioni di elementi globali associate come elementi radice per il tipo.  
  
-   Importazione dello schema: le dichiarazioni di elementi globali associate non sono necessarie e vengono ignorate se seguono le regole seguenti \(a meno che non definiscano tipi\).  
  
|Attributo|Schema|  
|---------------|------------|  
|`abstract`|Deve essere false per le dichiarazioni di elementi globali associate.|  
|`block`|Non consentito nelle dichiarazioni di elementi globali associate.|  
|`default`|Non consentito nelle dichiarazioni di elementi globali associate.|  
|`final`|Deve essere false per le dichiarazioni di elementi globali associate.|  
|`fixed`|Non consentito nelle dichiarazioni di elementi globali associate.|  
|`id`|Ignorato.|  
|`name`|Supportata. Vedere la definizione di dichiarazione di elemento globale associata.|  
|`nillable`|Deve essere true per le dichiarazioni di elementi globali associate.|  
|`substitutionGroup`|Non consentito nelle dichiarazioni di elementi globali associate.|  
|`type`|Supportato e deve corrispondere al tipo associato per le dichiarazioni di elementi globali associate \(a meno che l'elemento non contenga un tipo anonimo\).|  
  
### \<xs:element\>: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`simpleType`|Supportato.\*|  
|`complexType`|Supportato.\*|  
|`unique`|Ignorato.|  
|`key`|Ignorato.|  
|`keyref`|Ignorato.|  
|\(vuoto\)|Supportata.|  
  
 \* Quando si utilizzano `simpleType` e `complexType,`, il mapping dei tipi anonimi è uguale a quello dei tipi non anonimi, tranne per il fatto che non esiste alcun contratto dati anonimo e quindi viene creato un contratto dati denominato, con un nome generato derivato dal nome dell'elemento. Le regole per i tipi anonimi sono riportate nell'elenco seguente:  
  
-   Dettaglio di implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]: se il nome `xs:element` non contiene punti, il tipo anonimo esegue il mapping a un tipo interno del tipo di contratto dati esterno. Se il nome contiene punti, il tipo di contratto dati risultante è indipendente \(non è un tipo interno\).  
  
-   Il nome del contratto dati generato del tipo interno è il nome del contratto dati del tipo esterno seguito da un punto, dal nome dell'elemento e dalla stringa "Type".  
  
-   Se esiste già un contratto dati con tale nome, il nome viene reso univoco aggiungendo "1", "2", "3" e così via, fino a creare un nome univoco.  
  
## Tipi semplici \- \<xs:simpleType\>  
  
### \<xs:simpleType\>: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`final`|Ignorato.|  
|`id`|Ignorato.|  
|`name`|Supportato, esegue il mapping al nome del contratto dati.|  
  
### \<xs:simpleType\>: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`restriction`|Supportata. Esegue il mapping a contratti dati di enumerazione. Questo attributo viene ignorato se non corrisponde al modello di enumerazione. Vedere la sezione sulle restrizioni `xs:simpleType`.|  
|`list`|Supportata. Esegue il mapping a contratti dati di enumerazione flag. Vedere la sezione sugli elenchi `xs:simpleType`.|  
|`union`|Non consentito.|  
  
### \<xs:restriction\>  
  
-   Le restrizioni di tipi complessi sono supportate solo per la base \= "`xs:anyType`".  
  
-   Le restrizioni di tipi semplici di `xs:string` che non hanno facet di restrizione diversi da `xs:enumeration` vengono associate a contratti dati di enumerazione.  
  
-   Tutte le altre restrizioni di tipi semplici vengono associate ai tipi che limitano. Ad esempio, una restrizione di `xs:int` esegue il mapping a un Integer, esattamente come fa `xs:int`.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]l mapping dei tipi primitivi, vedere Mapping di tipi\/primitivi.  
  
### \<xs:restriction\>: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`base`|Deve essere un tipo semplice supportato o `xs:anyType`.|  
|`id`|Ignorato.|  
  
### \<xs:restriction\> per tutti gli altri casi: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`simpleType`|Se presente, deve essere derivato da un tipo primitivo supportato.|  
|`minExclusive`|Ignorato.|  
|`minInclusive`|Ignorato.|  
|`maxExclusive`|Ignorato.|  
|`maxInclusive`|Ignorato.|  
|`totalDigits`|Ignorato.|  
|`fractionDigits`|Ignorato.|  
|`length`|Ignorato.|  
|`minLength`|Ignorato.|  
|`maxLength`|Ignorato.|  
|`enumeration`|Ignorato.|  
|`whiteSpace`|Ignorato.|  
|`pattern`|Ignorato.|  
|\(vuoto\)|Supportata.|  
  
## Enumerazione  
  
### \<xs:restriction\> per enumerazioni: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`base`|Se presente, deve essere `xs:string`.|  
|`id`|Ignorato.|  
  
### \<xs:restriction\> per enumerazioni: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`simpleType`|Se presente, deve essere una restrizione di enumerazione supportata dal contratto dati \(questa sezione\).|  
|`minExclusive`|Ignorato.|  
|`minInclusive`|Ignorato.|  
|`maxExclusive`|Ignorato.|  
|`maxInclusive`|Ignorato.|  
|`totalDigits`|Ignorato.|  
|`fractionDigits`|Ignorato.|  
|`length`|Non consentito.|  
|`minLength`|Non consentito.|  
|`maxLength`|Non consentito.|  
|`enumeration`|Supportata. L'"id" dell'enumerazione viene ignorato e il "valore" esegue il mapping al nome del valore nel contratto dati di enumerazione.|  
|`whiteSpace`|Non consentito.|  
|`pattern`|Non consentito.|  
|\(vuoto\)|Supportato, esegue il mapping al tipo di enumerazione vuoto.|  
  
 Nel codice seguente viene illustrata una classe di enumerazione C\#.  
  
```  
public enum MyEnum  
{  
   first = 3,  
   second = 4,  
   third =5  
```  
  
 }  
  
 Questa classe esegue il mapping allo schema seguente da `DataContractSerializer`. Se i valori dell'enumerazione iniziano da 1, non vengono generati blocchi `xs:annotation`.  
  
```  
<xs:simpleType name="MyEnum">  
<xs:restriction base="xs:string">  
 <xs:enumeration value="first">  
  <xs:annotation>  
   <xs:appinfo>  
    <EnumerationValue   
     xmlns="http://schemas.microsoft.com/2003/10/Serialization/">  
     3  
    </EnumerationValue>  
   </xs:appinfo>  
  </xs:annotation>  
 </xs:enumeration>  
 <xs:enumeration value="second">  
  <xs:annotation>  
   <xs:appinfo>  
    <EnumerationValue   
     xmlns="http://schemas.microsoft.com/2003/10/Serialization/">  
     4  
    </EnumerationValue>  
   </xs:appinfo>  
  </xs:annotation>  
 </xs:enumeration>   
</xs:restriction>  
</xs:simpleType>  
```  
  
### \<xs:list\>  
 `DataContractSerializer` esegue il mapping dei tipi di enumerazione contrassegnati con `System.FlagsAttribute` a un `xs:list` derivato da `xs:string`. Non sono supportate altre variazioni di `xs:list`.  
  
### \<xs:list\>: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`itemType`|Non consentito.|  
|`id`|Ignorato.|  
  
### \<xs:list\>: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`simpleType`|Deve essere una restrizione da `xs:string` con utilizzo del facet `xs:enumeration`.|  
  
 Se il valore dell'enumerazione non segue una progressione per potenza di 2 \(impostazione predefinita per i flag\), viene memorizzato nell'elemento `xs:annotation/xs:appInfo/ser:EnumerationValue`.  
  
 Ad esempio, nel codice seguente viene contrassegnato un tipo di enumerazione.  
  
```  
[Flags]  
public enum AuthFlags  
{    
  AuthAnonymous = 1,  
  AuthBasic = 2,  
  AuthNTLM = 4,  
  AuthMD5 = 16,  
  AuthWindowsLiveID = 64,  
}  
```  
  
 Questo tipo esegue il mapping allo schema seguente.  
  
```  
<xs:simpleType name="AuthFlags">  
    <xs:list>  
      <xs:simpleType>  
        <xs:restriction base="xs:string">  
          <xs:enumeration value="AuthAnonymous" />  
          <xs:enumeration value="AuthBasic" />  
          <xs:enumeration value="AuthNTLM" />  
          <xs:enumeration value="AuthMD5">  
            <xs:annotation>  
              <xs:appinfo>  
                <EnumerationValue xmlns="http://schemas.microsoft.com/2003/10/Se  
rialization/">16</EnumerationValue>  
              </xs:appinfo>  
            </xs:annotation>  
          </xs:enumeration>  
          <xs:enumeration value="AuthWindowsLiveID">  
            <xs:annotation>  
              <xs:appinfo>  
                <EnumerationValue xmlns="http://schemas.microsoft.com/2003/10/Se  
rialization/">64</EnumerationValue>  
              </xs:appinfo>  
            </xs:annotation>  
          </xs:enumeration>  
        </xs:restriction>  
      </xs:simpleType>  
    </xs:list>  
  </xs:simpleType>  
```  
  
## Ereditarietà  
  
### Regole generali  
 Un contratto dati può ereditare da un altro contratto dati. Viene eseguito il mapping tra questi contratti dati, derivati da tipi di estensione tramite il costrutto dell'XML Schema `<xs:extension>`, e una base.  
  
 Un contratto dati non può ereditare da un contratto dati di raccolta.  
  
 Ad esempio, nel codice seguente viene illustrato un contratto dati.  
  
```  
[DataContract]  
public class Person  
{  
  [DataMember]  
  public string Name;  
}  
[DataContract]  
public class Employee : Person   
{      
  [DataMember]  
  public int ID;  
}  
```  
  
 Questo contratto dati esegue il mapping alla dichiarazione di tipo dell'XML Schema seguente.  
  
```  
<xs:complexType name="Employee">  
 <xs:complexContent mixed="false">  
  <xs:extension base="tns:Person">  
   <xs:sequence>  
    <xs:element minOccurs="0" name="ID" type="xs:int"/>  
   </xs:sequence>  
  </xs:extension>  
 </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="Person">  
 <xs:sequence>  
  <xs:element minOccurs="0" name="Name"   
    nillable="true" type="xs:string"/>  
 </xs:sequence>  
</xs:complexType>  
```  
  
### \<xs:complexContent\>: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`id`|Ignorato.|  
|`mixed`|Deve essere false.|  
  
### \<xs:complexContent\>: contenuto  
  
|Sommario|Schema|  
|--------------|------------|  
|`restriction`|Non consentito, tranne quando base \= "`xs:anyType`". L'ultima opzione equivale a posizionare il contenuto di `xs:restriction` direttamente sotto il contenitore di `xs:complexContent`.|  
|`extension`|Supportata. Esegue il mapping all'ereditarietà del contratto dati.|  
  
### \<xs:extension\> in \<xs:complexContent\>: attributi  
  
|Attributo|Schema|  
|---------------|------------|  
|`id`|Ignorato.|  
|`base`|Supportata. Esegue il mapping al tipo di contratto dati di base da cui questo tipo eredita.|  
  
### \<xs:extension\> in \<xs:complexContent\>: contenuto  
 Le regole sono le stesse del contenuto `<xs:complexType>`.  
  
 Se viene fornito un `<xs:sequence>`, i relativi elementi membro eseguono il mapping a membri dati aggiuntivi presenti nel contratto dati derivato.  
  
 Se un tipo derivato contiene un elemento con lo stesso nome di un elemento in un tipo di base, la dichiarazione dell'elemento duplicato esegue il mapping a un membro dati con un nome generato per essere univoco. Vengono aggiunti numeri interi positivi al nome del membro dati \("membro1", "membro2" e così via\) fino a trovare un nome univoco. Al contrario:  
  
-   Se un contratto dati derivato ha un membro dati con lo stesso nome e lo stesso tipo di un membro dati in un contratto dati di base, `DataContractSerializer` genera questo elemento corrispondente nel tipo derivato.  
  
-   Se un contratto dati derivato ha un membro dati con lo stesso nome di un membro dati in un contratto dati di base ma con un tipo diverso, `DataContractSerializer` importa uno schema con un elemento del tipo `xs:anyType` nelle dichiarazioni del tipo di base e del tipo derivato. Il nome del tipo originale viene mantenuto in `xs:annotations/xs:appInfo/ser:ActualType/@Name`.  
  
 Entrambe le variazioni possono condurre a un schema con un modello di contenuto ambiguo, che dipende dall'ordine dei rispettivi membri dati.  
  
## Mapping di tipi\/primitivi  
 `DataContractSerializer` utilizza il mapping seguente per i tipi primitivi dello XML Schema.  
  
|Tipo XSD|Tipo .NET|  
|--------------|---------------|  
|`anyType`|<xref:System.Object>.|  
|`anySimpleType`|<xref:System.String>.|  
|`duration`|<xref:System.TimeSpan>.|  
|`dateTime`|<xref:System.DateTime>.|  
|`dateTimeOffset`|<xref:System.DateTime> e <xref:System.TimeSpan> per l'offset. Vedere di seguito DateTimeOffset Serialization.|  
|`time`|<xref:System.String>.|  
|`date`|<xref:System.String>.|  
|`gYearMonth`|<xref:System.String>.|  
|`gYear`|<xref:System.String>.|  
|`gMonthDay`|<xref:System.String>.|  
|`gDay`|<xref:System.String>.|  
|`gMonth`|<xref:System.String>.|  
|`boolean`|<xref:System.Boolean>|  
|`base64Binary`|Matrice <xref:System.Byte>.|  
|`hexBinary`|<xref:System.String>.|  
|`float`|<xref:System.Single>.|  
|`double`|<xref:System.Double>.|  
|`anyURI`|<xref:System.Uri>.|  
|`QName`|<xref:System.Xml.XmlQualifiedName>.|  
|`string`|<xref:System.String>.|  
|`normalizedString`|<xref:System.String>.|  
|`token`|<xref:System.String>.|  
|`language`|<xref:System.String>.|  
|`Name`|<xref:System.String>.|  
|`NCName`|<xref:System.String>.|  
|`ID`|<xref:System.String>.|  
|`IDREF`|<xref:System.String>.|  
|`IDREFS`|<xref:System.String>.|  
|`ENTITY`|<xref:System.String>.|  
|`ENTITIES`|<xref:System.String>.|  
|`NMTOKEN`|<xref:System.String>.|  
|`NMTOKENS`|<xref:System.String>.|  
|`decimal`|<xref:System.Decimal>.|  
|`integer`|<xref:System.Int64>.|  
|`nonPositiveInteger`|<xref:System.Int64>.|  
|`negativeInteger`|<xref:System.Int64>.|  
|`long`|<xref:System.Int64>.|  
|`int`|<xref:System.Int32>.|  
|`short`|<xref:System.Int16>.|  
|`Byte`|<xref:System.SByte>.|  
|`nonNegativeInteger`|<xref:System.Int64>.|  
|`unsignedLong`|<xref:System.UInt64>.|  
|`unsignedInt`|<xref:System.UInt32>.|  
|`unsignedShort`|<xref:System.UInt16>.|  
|`unsignedByte`|<xref:System.Byte>.|  
|`positiveInteger`|<xref:System.Int64>.|  
  
## Mapping dei tipi ISerializable  
 In [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] versione 1.0, `ISerializable` è stato introdotto come meccanismo generale per serializzare oggetti per la persistenza o il trasferimento di dati. Sono disponibili molti tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che implementano `ISerializable` e che possono essere passati tra le applicazioni.`DataContractSerializer` fornisce naturalmente il supporto per le classi `ISerializable`.`DataContractSerializer` esegue il mapping ai tipi dello schema di implementazione di `ISerializable` che differiscono solo per il QName \(nome completo\) del tipo e sono effettivamente raccolte di proprietà. Ad esempio, `DataContractSerializer` esegue il mapping di <xref:System.Exception> al tipo XSD seguente nello spazio dei nomi http:\/\/schemas.datacontract.org\/2004\/07\/System.  
  
```  
<xs:complexType name="Exception">  
 <xs:sequence>  
  <xs:any minOccurs="0" maxOccurs="unbounded"   
      namespace="##local" processContents="skip"/>  
 </xs:sequence>  
 <xs:attribute ref="ser:FactoryType"/>  
</xs:complexType>  
```  
  
 L'attributo facoltativo `ser:FactoryType` dichiarato nello schema di serializzazione del contratto dati fa riferimento a una classe factory che può deserializzare il tipo. La classe factory deve far parte della raccolta dei tipi noti dell'istanza di `DataContractSerializer` utilizzata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]i tipi noti, vedere [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  
  
## Schema di serializzazione del contratto dati  
 Diversi schemi esportati da `DataContractSerializer` utilizzano tipi, elementi e attributi da uno speciale spazio dei nomi di serializzazione del contratto dati:  
  
 http:\/\/schemas.microsoft.com\/2003\/10\/Serialization  
  
 Di seguito è riportata una dichiarazione completa dello schema di serializzazione del contratto dati.  
  
```  
<xs:schema attributeFormDefault="qualified"          
   elementFormDefault="qualified"        
   targetNamespace =   
    "http://schemas.microsoft.com/2003/10/Serialization/"   
   xmlns:xs="http://www.w3.org/2001/XMLSchema"        
   xmlns:tns="http://schemas.microsoft.com/2003/10/Serialization/">  
  
 <!-- Top-level elements for primitive types. -->  
 <xs:element name="anyType" nillable="true" type="xs:anyType"/>  
 <xs:element name="anyURI" nillable="true" type="xs:anyURI"/>  
 <xs:element name="base64Binary"   
       nillable="true" type="xs:base64Binary"/>  
 <xs:element name="boolean" nillable="true" type="xs:boolean"/>  
 <xs:element name="byte" nillable="true" type="xs:byte"/>  
 <xs:element name="dateTime" nillable="true" type="xs:dateTime"/>  
 <xs:element name="decimal" nillable="true" type="xs:decimal"/>  
 <xs:element name="double" nillable="true" type="xs:double"/>  
 <xs:element name="float" nillable="true" type="xs:float"/>  
 <xs:element name="int" nillable="true" type="xs:int"/>  
 <xs:element name="long" nillable="true" type="xs:long"/>  
 <xs:element name="QName" nillable="true" type="xs:QName"/>  
 <xs:element name="short" nillable="true" type="xs:short"/>  
 <xs:element name="string" nillable="true" type="xs:string"/>  
 <xs:element name="unsignedByte"   
       nillable="true" type="xs:unsignedByte"/>  
 <xs:element name="unsignedInt"   
       nillable="true" type="xs:unsignedInt"/>  
 <xs:element name="unsignedLong"   
       nillable="true" type="xs:unsignedLong"/>  
 <xs:element name="unsignedShort"   
       nillable="true" type="xs:unsignedShort"/>  
  
 <!-- Primitive types introduced for certain .NET simple types. -->  
 <xs:element name="char" nillable="true" type="tns:char"/>  
 <xs:simpleType name="char">  
  <xs:restriction base="xs:int"/>  
 </xs:simpleType>  
  
 <!-- xs:duration is restricted to an ordered value space,   
    to map to System.TimeSpan -->  
 <xs:element name="duration" nillable="true" type="tns:duration"/>  
 <xs:simpleType name="duration">  
  <xs:restriction base="xs:duration">  
   <xs:pattern   
     value="\-?P(\d*D)?(T(\d*H)?(\d*M)?(\d*(\.\d*)?S)?)?"/>  
   <xs:minInclusive value="-P10675199DT2H48M5.4775808S"/>  
   <xs:maxInclusive value="P10675199DT2H48M5.4775807S"/>  
  </xs:restriction>  
 </xs:simpleType>  
  
 <xs:element name="guid" nillable="true" type="tns:guid"/>  
 <xs:simpleType name="guid">  
  <xs:restriction base="xs:string">  
   <xs:pattern value="[\da-fA-F]{8}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{12}"/>  
  </xs:restriction>  
 </xs:simpleType>  
  
 <!-- This is used for schemas exported from ISerializable type. -->  
 <xs:attribute name="FactoryType" type="xs:QName"/>  
</xs:schema>  
```  
  
 È necessario tenere presente quanto segue:  
  
-   `ser:char` viene introdotto per rappresentare caratteri Unicode di tipo <xref:System.Char>.  
  
-   Il `valuespace` di `xs:duration` viene ridotto a una raccolta ordinata, in modo che possa essere associato a un <xref:System.TimeSpan>.  
  
-   `FactoryType` viene utilizzato negli schemi esportati da tipi derivati da <xref:System.Runtime.Serialization.ISerializable>.  
  
## Importazione di schemi non di contratto dati  
 `DataContractSerializer` dispone dell'opzione `ImportXmlTypes` per consentire l'importazione di schemi non conformi al profilo XSD `DataContractSerializer` \(vedere la proprietà <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A>\). Se si imposta questa opzione su `true`, si consente l'accettazione di tipi di schema non conformi e il mapping di questi ultimi all'implementazione seguente, con <xref:System.Xml.Serialization.IXmlSerializable> che esegue il wrapping di una matrice di <xref:System.Xml.XmlNode> \(differisce solo il nome della classe\).  
  
```  
[GeneratedCodeAttribute("System.Runtime.Serialization", "3.0.0.0")]  
[System.Xml.Serialization.XmlSchemaProviderAttribute("ExportSchema")]  
[System.Xml.Serialization.XmlRootAttribute(IsNullable=false)]  
public partial class Person : object, IXmlSerializable  
{    
  private XmlNode[] nodesField;    
  private static XmlQualifiedName typeName =   
new XmlQualifiedName("Person","http://Microsoft.ServiceModel.Samples");    
  public XmlNode[] Nodes  
  {  
    get {return this.nodesField;}  
    set {this.nodesField = value;}  
  }    
  public void ReadXml(XmlReader reader)  
  {  
    this.nodesField = XmlSerializableServices.ReadNodes(reader);  
  }    
  public void WriteXml(XmlWriter writer)  
  {  
    XmlSerializableServices.WriteNodes(writer, this.Nodes);  
  }    
  public System.Xml.Schema.XmlSchema GetSchema()  
  {  
    return null;  
  }    
  public static XmlQualifiedName ExportSchema(XmlSchemaSet schemas)  
  {  
    XmlSerializableServices.AddDefaultSchema(schemas, typeName);  
    return typeName;  
  }  
}  
```  
  
## Serializzazione DateTimeOffset  
 <xref:System.DateTimeOffset> non viene considerato un tipo primitivo. Viene invece serializzato come elemento complesso con due parti. La prima parte rappresenta il valore data\/ora e la seconda parte rappresenta l'offset dal valore data\/ora. Nel codice seguente viene illustrato un esempio di valore DateTimeOffset serializzato.  
  
```  
<OffSet xmlns:a="http://schemas.datacontract.org/2004/07/System">  
  <DateTime i:type="b:dateTime"   
    xmlns:b="http://www.w3.org/2001/XMLSchema">2008-08-28T08:00:00    
  </DateTime>   
  <OffsetMinutes i:type="b:short"   
   xmlns:b="http://www.w3.org/2001/XMLSchema">-480  
   </OffsetMinutes>   
</OffSet>  
```  
  
 Lo schema è il seguente.  
  
```  
<xs:schema targetNamespace="http://schemas.datacontract.org/2004/07/System">  
   <xs:complexType name="DateTimeOffset">  
      <xs:sequence minOccurs="1" maxOccurs="1">  
         <xs:element name="DateTime" type="xs:dateTime"  
         minOccurs="1" maxOccurs="1" />  
         <xs:elementname="OffsetMinutes" type="xs:short"  
         minOccurs="1" maxOccurs="1" />  
      </xs:sequence>  
   </xs:complexType>  
</xs:schema>  
```  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)