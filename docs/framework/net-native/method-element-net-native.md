---
title: "Elemento &lt;Method&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 348b49e5-589d-4eb2-a597-d6ff60ab52d1
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Elemento &lt;Method&gt; (.NET Native)
Applica i criteri di reflection di runtime a un costruttore o a un metodo.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Method Name="method_name"  
        Signature="method_signature"  
        Browse="policy_type"  
        Dynamic="policy_type" />  
  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Tipo di attributo|Descrizione|  
|---------------|--------------------|-----------------|  
|`Name`|Generale|Attributo obbligatorio. Specifica il nome del metodo.|  
|`Signature`|Generale|Attributo facoltativo. Specifica la firma del metodo. Se esistono più parametri, sono separati da virgole. Ad esempio, `<Method>` elemento definisce i criteri per il <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29> (metodo).<br /><br /> `<Type Name="System.DateTime">    <Method Name="ToString" Signature="System.String,System.IFormatProvider"            Dynamic="Required" /> </Type>`<br /><br /> Se l'attributo è assente, la direttiva di runtime si applica a tutti gli overload del metodo.|  
|`Browse`|Reflection|Attributo facoltativo. Controlla l'esecuzione di query per informazioni sul metodo o la sua enumerazione, ma non abilita alcuna chiamata dinamica in fase di esecuzione.|  
|`Dynamic`|Reflection|Attributo facoltativo. Controlla l'accesso del runtime a un costruttore o al metodo per attivare la programmazione dinamica. Questo criterio assicura che un membro possa essere richiamato in modo dinamico in fase di esecuzione.|  
  
## <a name="name-attribute"></a>Name (attributo)  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*nome_metodo*|Nome del metodo. Il tipo del metodo è definito dall'elemento padre [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) o [ <> \> ](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) elemento.|  
  
## <a name="signature-attribute"></a>Attributo Signature  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*method_signature*|Tipi di parametri che costituiscono la firma del metodo. Più parametri sono separati da virgole, ad esempio `"System.String,System.Int32,System.Int32)"`. I nomi del tipo di parametro devono essere completi.|  
  
## <a name="all-other-attributes"></a>Tutti gli altri attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri. I valori consentiti sono `Auto`, `Excluded`, `Included` e `Required`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/parameter-element-net-native.md)|Applica i criteri al tipo di argomento passato a un metodo.|  
|[<>\>](../../../docs/framework/net-native/genericparameter-element-net-native.md)|Applica i criteri al tipo di parametro di un tipo o di un metodo generico.|  
|[<>\>](../../../docs/framework/net-native/impliestype-element-net-native.md)|Applica criteri a un tipo, se tale criterio è stato applicato al metodo rappresentato dall'oggetto contenente l'elemento `<Method>`.|  
|[<>\>](../../../docs/framework/net-native/typeparameter-element-net-native.md)|Applica i criteri per il tipo rappresentato da un <xref:System.Type> argomento passato a un metodo.|  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo e a tutti i membri.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Applica i criteri di reflection a un tipo generico costruito e a tutti i membri.|  
  
## <a name="remarks"></a>Note  
 Un elemento `<Method>` di un metodo generico applica i relativi criteri a tutte le istanze che non dispongono di propri criteri.  
  
 È possibile usare l'attributo `Signature` per specificare criteri per un overload del metodo specifico. In caso contrario, se l'attributo `Signature` è assente, la direttiva di runtime si applica a tutti gli overload del metodo.  
  
 Non è possibile definire i criteri di reflection di runtime per un costruttore con l'elemento `<Method>`. Instead, use the `Activate` attribute of the  [<>\>](../../../docs/framework/net-native/assembly-element-net-native.md), [<>\>](../../../docs/framework/net-native/namespace-element-net-native.md), [<>\>](../../../docs/framework/net-native/type-element-net-native.md), or [<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) element.  
  
## <a name="example"></a>Esempio  
 Il metodo `Stringify` nell'esempio seguente è un metodo di formattazione generico che usa la reflection per convertire un oggetto nella relativa rappresentazione di stringa. Oltre a chiamare predefinito dell'oggetto `ToString` (metodo), il metodo può produrre una stringa di risultato formattata passando un oggetto `ToString` metodo una stringa di formato, un <xref:System.IFormatProvider> implementazione o entrambi. Inoltre possibile chiamare uno del <xref:System.Convert.ToString%2A?displayProperty=fullName> overload che converte un numero nella relativa rappresentazione binaria, ottale o esadecimale.  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 Il metodo `Stringify` può essere chiamato da codice simile al seguente:  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 Tuttavia, quando viene compilato con .NET Native, l'esempio può generare un numero di eccezioni in fase di esecuzione, tra cui <xref:System.NullReferenceException> e [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) eccezioni, ciò si verifica perché il `Stringify` metodo è destinato principalmente a supportare la formattazione dinamica dei tipi primitivi nella libreria di classi .NET Framework. Tuttavia, i metadati non vengono resi disponibili dal file di direttive predefinito. Anche quando i metadati vengono resi disponibili, tuttavia, l'esempio genererà [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) eccezioni perché appropriato `ToString` implementazioni non sono stati incluse nel codice nativo.  
  
 Queste eccezioni possono essere eliminate utilizzando il [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) elemento per definire i tipi i cui metadati devono essere presenti e aggiungendo `<Method>` gli elementi per verificare che l'implementazione del metodo di overload che possono essere chiamato in modo dinamico è inoltre presente. Di seguito è riportato il file default.rd.xml che elimina queste eccezioni e consente l'esecuzione dell'esempio senza errori.  
  
```xml  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
     <Assembly Name="*Application*" Dynamic="Required All" />  
  
     <Type Name = "System.Convert" Browse="Required Public" Dynamic="Required Public" >  
        <Method Name="ToString"    Dynamic ="Required" />  
     </Type>  
     <Type Name="System.Double" Browse="Required Public">  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int32" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int64" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Namespace Name="System" >  
        <Type Name="Byte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="DateTime" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Decimal" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Guid" Browse ="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Int16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="SByte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Single" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />           
        </Type>  
        <Type Name="TimeSpan" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />           
        </Type>  
        <Type Name="UInt16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt32" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt64" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
     </Namespace>  
  </Application>  
</Directives>  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [<>\>Elemento](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)