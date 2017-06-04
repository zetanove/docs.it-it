---
title: "Elemento &lt;ImpliesType&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3abd2071-0f28-40ba-b9a0-d52bd94cd2f6
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;ImpliesType&gt; (.NET Native)
Applica criteri a un tipo, se tale criterio è stato applicato al metodo o al tipo contenitore.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
  
<ImpliesType Name="type_name"  
             Activate="policy_type"  
             Browse="policy_type"  
             Dynamic="policy_type"  
             Serialize="policy_type"   
             DataContractSerializer="policy_setting"  
             DataContractJsonSerializer="policy_setting"  
             XmlSerializer="policy_setting"  
             MarshalObject="policy_setting"  
             MarshalDelegate="policy_setting"  
             MarshalStructure="policy_setting" />  
  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Tipo di attributo|Descrizione|  
|---------------|--------------------|-----------------|  
|`Name`|Generale|Attributo obbligatorio. Specifica il nome del tipo.|  
|`Activate`|Reflection|Attributo facoltativo. Controlla l'accesso in fase di esecuzione ai costruttori per abilitare l'attivazione di istanze.|  
|`Browse`|Reflection|Attributo facoltativo. Controlla le query per le informazioni sugli elementi di programma, ma non abilita l'accesso in fase di esecuzione.|  
|`Dynamic`|Reflection|Attributo facoltativo. Controlla l'accesso in fase di esecuzione a tutti i membri dei tipi, inclusi costruttori, metodi, campi, proprietà ed eventi, per abilitare la programmazione dinamica.|  
|`Serialize`|Serializzazione|Attributo facoltativo. Controlla l'accesso in fase di esecuzione a costruttori, campi e proprietà per abilitare la serializzazione e la deserializzazione delle istanze del tipo da parte di librerie quali il serializzatore JSON di Newtonsoft.|  
|`DataContractSerializer`|Serializzazione|Attributo facoltativo. Controlla i criteri per la serializzazione che utilizza il <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> (classe).|  
|`DataContractJsonSerializer`|Serializzazione|Attributo facoltativo. Controlla i criteri per la serializzazione JSON che utilizza il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> (classe).|  
|`XmlSerializer`|Serializzazione|Attributo facoltativo. Controlla i criteri per la serializzazione XML che utilizza il <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> (classe).|  
|`MarshalObject`|Interoperabilità|Attributo facoltativo. Controlla i criteri per effettuare il marshalling dei tipi di riferimento a Windows Runtime e COM.|  
|`MarshalDelegate`|Interoperabilità|Attributo facoltativo. Controlla i criteri per effettuare il marshalling dei tipi delegati come puntatori a funzioni al codice nativo.|  
|`MarshalStructure`|Interoperabilità|Attributo facoltativo. Controlla i criteri per il marshalling dei tipi di valore al codice nativo.|  
  
## <a name="name-attribute"></a>Name (attributo)  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*TYPE_NAME*|Nome del tipo. Se il tipo rappresentato da questo `<ImpliesType>` elemento si trova nello spazio dei nomi stesso contenitore `<Type>` elemento *type_name* può includere il nome del tipo senza il relativo spazio dei nomi. In caso contrario, *type_name* deve includere il nome completo del tipo.|  
  
## <a name="all-other-attributes"></a>Tutti gli altri attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri. I valori consentiti sono `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` e `Required All`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo e a tutti i membri.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Applica i criteri di reflection a un tipo generico costruito e a tutti i membri.|  
|[<>\>](../../../docs/framework/net-native/method-element-net-native.md)|Applica i criteri di reflection a un metodo.|  
  
## <a name="remarks"></a>Note  
 L'elemento `<ImpliesType>` viene usato principalmente dalle librerie. Consente di risolvere il seguente scenario:  
  
-   Se una routine deve eseguire la reflection su un tipo, deve necessariamente eseguirla anche su un secondo tipo.  
  
-   I metadati per la creazione di istanze implicita del secondo tipo sono altrimenti disponibili, in quanto l'analisi statica non indica che sono necessari.  
  
 I due tipi sono, in genere, creazioni di istanze generiche con gli argomenti di tipo condiviso.  
  
 L'elemento `<ImpliesType>` è stato definito partendo dal presupposto che la necessità di reflection sul tipo specificato dal relativo elemento padre comporta la necessità della reflection sul tipo specificato dall'elemento `<ImpliesType>`. Ad esempio, le seguenti direttive di reflection si applicano a due tipi: `Explicit<T>` e `Implicit<T>`.  
  
```xml  
  
<Type Name=”Explicit{ET}”>  
    <ImpliesType Name=”Implicit{ET}” Dynamic=”Required Public” />  
</Type>  
  
```  
  
 Questa direttiva non ha alcun effetto a meno che non sia stata definita un'impostazione di criteri `Explicit` per un'istanza di `Dynamic`. Se, ad esempio, è il caso per `Explicit<Int32>`, viene creata un'istanza di `Implicit<Int32>` con membri pubblici che contengono una radice e i relativi metadati vengono resi accessibili per la programmazione dinamica.  
  
 Di seguito è riportato un esempio reale che si applica ad almeno un serializzatore. Le direttive assegnano il requisito che effettuare la reflection su un elemento tipizzato come `IList<` *qualcosa* `>` implica la reflection sul corrispondente `List<` *qualcosa* `>` tipo senza richiedere annotazioni per ogni applicazione.  
  
```xml  
  
<Type Name=”System.Collections.Generic.IList{T}”>  
   <ImpliesType Name=”System.Collections.Generic.List{T}” Serialize=”Public” />  
</Type>  
  
```  
  
 L'elemento `<ImpliesType>` può anche essere visualizzato all'interno di un elemento `<Method>`, perché in alcuni casi un'istanza di un metodo generico implica la reflection su un'istanza del tipo. Ad esempio, immaginare un metodo generico `IEnumerable<T> MakeEnumerable<T>(string` `spelling``, T` `defaultValue``)` che una determinata libreria accederà in modo dinamico con associato <xref:System.Collections.Generic.List%601> e <xref:System.Array> tipi. Questa operazione può essere espressa nel seguente modo:  
  
```xml  
  
<Type Name=”MyType”>  
    <Method Name=”MakeEnumerable{T}” Signature=”(System.String, T)” Dynamic=”Included”>  
        <ImpliesType Name=”T[]” Dynamic=”Public” />  
        <ImpliesType Name=”System.Collections.Generic.List{T}” Dynamic=”Public”>  
    </Method>  
</Type>  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)