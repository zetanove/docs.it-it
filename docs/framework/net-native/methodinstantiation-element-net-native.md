---
title: "Elemento &lt;MethodInstantiation&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a3355d78-2a88-4109-8521-830d7cae260a
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Elemento &lt;MethodInstantiation&gt; (.NET Native)
Applica i criteri di reflection di runtime a un metodo generico costruito.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<MethodInstantiation Name="method_name"  
                     Signature="method_signature"  
                     Arguments="method_arguments"  
                     Browse="policy_type"  
                     Dynamic="policy_type" />  
  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Tipo di attributo|Descrizione|  
|---------------|--------------------|-----------------|  
|`Name`|Generale|Attributo obbligatorio. Specifica il nome del metodo.|  
|`Signature`|Generale|Attributo facoltativo. Specifica i parametri denominati del metodo. Più parametri denominati sono separati da virgole. L'attributo `Signature` viene usato per differenziare i metodi sottoposti a overload.|  
|`Arguments`|Generale|Attributo obbligatorio. Specifica gli argomenti di tipo generico. Se sono presenti più argomenti, saranno separati da virgole.|  
|`Browse`|Reflection|Attributo facoltativo. Controlla l'esecuzione di query per informazioni sul metodo o la sua enumerazione, ma non abilita alcuna chiamata dinamica in fase di esecuzione.|  
|`Dynamic`|Reflection|Attributo facoltativo. Controlla l'accesso del runtime a un costruttore o al metodo per attivare la programmazione dinamica. Questo criterio assicura che un membro possa essere richiamato in modo dinamico in fase di esecuzione.|  
  
## <a name="name-attribute"></a>Name (attributo)  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*nome_metodo*|Nome del metodo. Il tipo del metodo è definito dall'elemento padre [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) o [ <> \> ](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) elemento.|  
  
## <a name="signature-attribute"></a>Attributo Signature  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*method_signature*|Specifica i parametri del metodo denominati. Se esistono più parametri, sono separati da virgole.|  
  
## <a name="arguments-attribute"></a>Attributo di argomenti  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*method_arguments*|Specifica gli argomenti tipo generico. Se sono presenti più argomenti, saranno separati da virgole. Ogni argomento deve essere costituito dal nome completo del tipo.|  
  
## <a name="all-other-attributes"></a>Tutti gli altri attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri per il metodo. I valori consentiti sono `Auto`, `Excluded`, `Included` e `Required`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo e a tutti i membri.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Applica i criteri di reflection a un tipo generico costruito e a tutti i membri.|  
  
## <a name="remarks"></a>Note  
 L'elemento `<MethodInstantiation>` prevale sui criteri di reflection di runtime del corrispondente metodo generico aperto.  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [<>\>Elemento](../../../docs/framework/net-native/method-element-net-native.md)