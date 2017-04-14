---
title: "Elemento &lt;Subtypes&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb854070-248b-46cf-9dab-c322e2b4d624
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Elemento &lt;Subtypes&gt; (.NET Native)
Applica i criteri di runtime a tutte le classi ereditate per il tipo contenitore.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Subtypes Activate="policy_type"  
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
  
## <a name="all-attributes"></a>Tutti gli attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri. I valori consentiti sono `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` e `Required All`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo e a tutti i membri.|  
  
## <a name="remarks"></a>Note  
 L'elemento `<Subtypes>` applica i criteri a tutti i sottotipi del tipo contenitore. Viene usato per applicare criteri diversi ai tipi derivati e alle classi base.  
  
 Gli attributi di reflection, serializzazione e interoperabilità sono tutti facoltativi, ma è necessario usarne almeno uno.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente definisce una classe denominata `BaseClass` e una sottoclasse denominata `Derived1`.  
  
 [!code-csharp[ProjectN_Reflection#4](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/subtypes.cs#4)]  
  
 Come mostrato nel seguente codice, il file di direttive di runtime imposta esplicitamente i criteri `Dynamic` e `Activate` per `BaseClass` su `Excluded`. Di conseguenza, non è possibile creare un'istanza degli oggetti di tipo `BaseClass` dinamicamente o mediante chiamate al costruttore di classi `BaseClass`. Tuttavia, l'elemento `<Subtypes>` consente di creare un'istanza delle classi derivate da `BaseClass` dinamicamente e mediante chiamate ai relativi costruttori di classi.  
  
```xml  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
   <Assembly Name="*Application*" Dynamic="Required All" />  
     <Type Name="Examples.Libraries.BaseClass" Activate ="Excluded" Dynamic="Excluded" >  
        <Subtypes Activate="Public" Dynamic ="Public"/>  
     </Type>  
  </Application>  
</Directives>  
  
```  
  
 Perché il `<Subtypes>` (direttiva), il codice seguente che crea un'istanza di un `Derived1` istanza chiamando in modo dinamico il <xref:System.Activator.CreateInstance%28System.Type%29?displayProperty=fullName> metodo viene eseguito correttamente.  Questa variabile del blocco è un <xref:System.Windows.Controls.TextBlock> oggetto in un'applicazione Windows Store vuota.  
  
 [!code-csharp[ProjectN_Reflection#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/subtypes.cs#5)]  
  
## <a name="see-also"></a>Vedere anche  
 [<>\>Elemento](../../../docs/framework/net-native/type-element-net-native.md)   
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)