---
title: "Elemento &lt;Assembly&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cfe629eb-1106-4113-86e1-052f402d8d8b
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Elemento &lt;Assembly&gt; (.NET Native)
Applica i criteri di reflection di runtime a tutti i tipi in un determinato assembly.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Assembly Name="assembly_name"   
          Activate="policy_setting"  
          Browse="policy_setting"  
          Dynamic="policy_setting"  
          Serialize="policy_setting" />  
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
|`Name`|Generale|Attributo obbligatorio. Specifica il nome semplice di un assembly.|  
|`Activate`|Reflection|Attributo facoltativo. Controlla l'accesso in fase di esecuzione ai costruttori per abilitare l'attivazione di istanze.|  
|`Browse`|Reflection|Attributo facoltativo. Controlla le query per le informazioni o per l'enumerazione dei tipi nell'assembly, ma non abilita l'accesso dinamico al runtime.|  
|`Dynamic`|Reflection|Attributo facoltativo. Controlla l'accesso in fase di esecuzione a tutti i membri dei tipi, inclusi costruttori, metodi, campi, proprietà ed eventi, per abilitare la programmazione dinamica.|  
|`Serialize`|Serializzazione|Attributo facoltativo. Controlla l'accesso in fase di esecuzione a costruttori, campi e proprietà per abilitare la serializzazione e la deserializzazione delle istanze del tipo da parte di librerie quali il serializzatore JSON di Newtonsoft.|  
|`DataContractSerializer`|Serializzazione|Attributo facoltativo. Controlla i criteri per la serializzazione che utilizza il <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> (classe).|  
|`DataContractJsonSerializer`|Serializzazione|Attributo facoltativo. Controlla i criteri per la serializzazione JSON che utilizza il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> (classe).|  
|`XmlSerializer`|Serializzazione|Attributo facoltativo. Controlla i criteri per la serializzazione XML che utilizza il <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> (classe).|  
|`MarshalObject`|Interoperabilità|Attributo facoltativo. Controlla i criteri per effettuare il marshalling dei tipi di riferimento a Windows Runtime e COM.|  
|`MarshalDelegate`|Interoperabilità|Attributo facoltativo. Controlla i criteri per effettuare il marshalling dei tipi delegati come puntatori a funzioni al codice nativo.|  
|`MarshalStructure`|Interoperabilità|Attributo facoltativo. Controlla i criteri per il marshalling delle strutture al codice nativo.|  
  
## <a name="name-attribute"></a>Name (attributo)  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*assembly_name*|Il nome semplice dell'assembly, senza estensione di file. Questo attributo corrisponde al <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=fullName> proprietà. Ad esempio, il nome di un assembly denominato Extensions.dll è "Extensions".<br /><br /> È anche possibile specificare la stringa letterale `*Application*` per applicare i criteri a tutti gli assembly nel pacchetto dell'app, a prescindere se siano caricati o meno. `*Application*` non applica mai i criteri agli assembly di .NET Framework.|  
  
## <a name="all-other-attributes"></a>Tutti gli altri attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri per tutti i tipi nell'assembly. I valori consentiti sono `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` e `Required All`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/namespace-element-net-native.md)|Applica i criteri di reflection a tutti i tipi in uno spazio dei nomi figlio.|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Applica i criteri di reflection a un tipo generico costruito.|  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/application-element-net-native.md)|Viene usato come contenitore per i tipi e i membri dei tipi a livello di applicazione i cui metadati sono disponibili per la reflection al runtime. Il [ <> \> ](../../../docs/framework/net-native/application-element-net-native.md) elemento può avere zero, uno o più `<Assembly>` elementi.|  
|[<>\>](../../../docs/framework/net-native/library-element-net-native.md)|Definisce l'assembly che contiene i tipi e i membri dei tipi i cui metadati sono disponibili per la reflection al runtime. Il [ <> \> ](../../../docs/framework/net-native/library-element-net-native.md) elemento può avere zero o uno `<Assembly>` elemento.|  
  
## <a name="remarks"></a>Note  
 L'elemento `<Assembly>` definisce i criteri di runtime per tutti i tipi in un assembly. Differisce dal [ <> \> ](../../../docs/framework/net-native/library-element-net-native.md) elemento, che specifica una raccolta, ma dipende dagli elementi figlio per definire i criteri di reflection di runtime. L'elemento `<Assembly>` si applica a tutti i tipi in un assembly a meno che questi non siano sottoposti a override da un elemento figlio.  
  
 Nell'esempio seguente viene illustrato come applicare i criteri di runtime a tutti i tipi negli assembly all'interno del pacchetto di app assegnando il `Name` un valore dell'attributo "* Application\*". Il `<Assembly>` elemento deve essere un figlio di [ <> \> ](../../../docs/framework/net-native/application-element-net-native.md) elemento.  
  
```xml  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">   
  <Application>   
     <Assembly Name="*Application*" Dynamic="Required All" />   
  </Application>   
</Directives>  
  
```  
  
 Gli attributi `Activate`, `Browse`, `Dynamic` e `Serialize` sono tutti facoltativi. Tuttavia, l'elemento `<Assembly>` deve contenere almeno uno di questi attributi.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)