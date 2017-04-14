---
title: "Elemento &lt;Namespace&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 57c614e5-18a9-4e87-bfd5-d0fe3396a192
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Elemento &lt;Namespace&gt; (.NET Native)
Applica i criteri di reflection di runtime a tutti i tipi in un determinato spazio dei nomi.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Namespace Name="namespace_name"   
           Activate="policy_type"   
           Browse="policy_type" />  
           Dynamic="policy_setting"  
           Serialize="policy_setting"  
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
|`Name`|Generale|Attributo obbligatorio. Specifica il nome dello spazio dei nomi.|  
|`Activate`|Reflection|Attributo facoltativo. Controlla l'accesso in fase di esecuzione ai costruttori per abilitare l'attivazione di istanze.|  
|`Browse`|Reflection|Attributo facoltativo. Controlla le query per le informazioni sugli elementi di programma, ma non abilita l'accesso in fase di esecuzione.|  
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
|*namespace_name*|Nome dello spazio dei nomi. Se il <> \> è un elemento figlio di un [ <> \</> \> ](../../../docs/framework/net-native/application-element-net-native.md), [ <> \</> \> ](../../../docs/framework/net-native/library-element-net-native.md), o [ <> \> ](../../../docs/framework/net-native/assembly-element-net-native.md) elemento *namespace_name* deve essere un nome completo dello spazio dei nomi. Se il <> \> è un elemento figlio di un altro <> \> elemento *namespace_name* deve essere un nome relativo dello spazio dei nomi.|  
  
## <a name="all-other-attributes"></a>Tutti gli altri attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri per tutti i tipi nello spazio dei nomi. I valori consentiti sono `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` e `Required All`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|`<Namespace>`|Applica i criteri di reflection di runtime a tutti i tipi in uno spazio dei nomi padre.|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Applica i criteri di reflection a un tipo generico costruito.|  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/application-element-net-native.md)|Viene usato come contenitore per i tipi e i membri dei tipi a livello di applicazione i cui metadati sono disponibili per la reflection al runtime. Il [ <> \> ](../../../docs/framework/net-native/application-element-net-native.md) elemento può avere zero, uno o più [ <> \> ](../../../docs/framework/net-native/assembly-element-net-native.md) elementi.|  
|[<>\>](../../../docs/framework/net-native/assembly-element-net-native.md)|Applica i criteri di reflection di runtime a tutti i tipi in un determinato assembly.|  
|[<>\>](../../../docs/framework/net-native/library-element-net-native.md)|Definisce l'assembly che contiene i tipi e i membri dei tipi i cui metadati sono disponibili per la reflection al runtime. Il [ <> \> ](../../../docs/framework/net-native/library-element-net-native.md) elemento può avere zero o uno [ <> \> ](../../../docs/framework/net-native/assembly-element-net-native.md) elemento.|  
|`<Namespace>`|Applica i criteri di reflection a tutti i tipi in uno spazio dei nomi padre.|  
  
## <a name="remarks"></a>Note  
 Gli attributi `Activate`, `Browse`, `Dynamic` e `Serialize` sono tutti facoltativi. Se non ne è presente nessuno, l'elemento `<Namespace>` funge solo da contenitore per gli elementi figlio. Se sono presenti, l'elemento `<Namespace>` consente di applicare criteri di reflection di runtime a tutti i tipi dello spazio dei nomi specificato.  
  
 Quando è un figlio di [ <> \> ](../../../docs/framework/net-native/assembly-element-net-native.md) elemento, il `<Namespace>` elemento esegue l'override di criteri di reflection di runtime definiti dalla [ <> \> ](../../../docs/framework/net-native/assembly-element-net-native.md) elemento.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)