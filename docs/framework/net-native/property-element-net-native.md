---
title: "Elemento &lt;Property&gt; (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad4ba56d-3bcb-4c10-ba90-1cc66e2175a1
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Elemento &lt;Property&gt; (.NET Native)
Applica i criteri di reflection di runtime a una proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
  
<Property Name="property_name"  
          Browse="policy_type"  
          Dynamic="policy_type"  
          Serialize="policy_type" />  
  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Tipo di attributo|Descrizione|  
|---------------|--------------------|-----------------|  
|`Name`|Generale|Attributo obbligatorio. Specifica il nome della proprietà.|  
|`Browse`|Reflection|Attributo facoltativo. Controlla le query per le informazioni o per l'enumerazione della proprietà, ma non abilita l'accesso dinamico al runtime.|  
|`Dynamic`|Reflection|Attributo facoltativo. Controlla l'accesso in fase di esecuzione alla proprietà per abilitare la programmazione dinamica. Questo criterio assicura che una proprietà può essere impostata o recuperata dinamicamente in fase di esecuzione.|  
|`Serialize`|Serializzazione|Attributo facoltativo. Controlla l'accesso in fase di esecuzione a una proprietà per abilitare le istanze di tipo da serializzare in librerie quali il serializzatore JSON Newtonsoft o da usare per il data binding.|  
  
## <a name="name-attribute"></a>Name (attributo)  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*nome_metodo*|Nome della proprietà. Il tipo della proprietà è definito dall'elemento padre [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) o [ <> \> ](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) elemento.|  
  
## <a name="all-other-attributes"></a>Tutti gli altri attributi  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|*policy_setting*|L'impostazione da applicare a questo tipo di criteri per la proprietà. I valori consentiti sono `Auto`, `Excluded`, `Included` e `Required`. Per ulteriori informazioni, vedere [impostazioni dei criteri della direttiva di Runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementi figlio  
 Nessuno.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Applica i criteri di reflection a un tipo e a tutti i membri.|  
|[<>\>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|Applica i criteri di reflection a un tipo generico costruito e a tutti i membri.|  
  
## <a name="remarks"></a>Note  
 Se i criteri di una proprietà non sono definiti esplicitamente, la proprietà eredita i criteri di runtime dell'elemento padre.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente si usa la reflection per creare un'istanza di un oggetto `Book` e visualizzare i valori delle proprietà. Il file originale default.rd.xml per il progetto viene visualizzato come segue:  
  
```xml  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Namespace Name="LibraryApplications"  Browse="Required Public" >  
         <Type Name="Book"   Activate="All" />  
      </Namespace>  
   </Application>  
</Directives>  
  
```  
  
 Il file applica il valore `All` ai criteri `Activate` per la classe `Book`, che consente di accedere ai costruttori della classe tramite la reflection. I criteri `Browse` per la classe `Book` vengono ereditati dal relativo spazio dei nomi padre. Questa proprietà è impostata su `Required Public`, che rende disponibili i metadati in fase di esecuzione.  
  
 Di seguito viene riportato il codice sorgente per l'esempio. Il `outputBlock` variabile rappresenta un [TextBlock](http://msdn.microsoft.com/library/windows.ui.xaml.controls.textblock.aspx) controllo.  
  
 [!code-csharp[ProjectN_Reflection#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/property1.cs#6)]  
  
 Tuttavia, la compilazione e l'esecuzione di questo esempio genera un [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) (eccezione). Anche se i metadati per il tipo `Book` sono stati resi disponibili, non è stato possibile rendere disponibili le implementazioni di funzioni Get di proprietà in modo dinamico. È possibile correggere l'errore in uno di due modi:  
  
-   definendo il `Dynamic` criteri per il `Book` digitare relativo [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) elemento.  
  
-   Aggiungendo un nidificata [ <> \> ](../../../docs/framework/net-native/property-element-net-native.md) (elemento) per ogni proprietà di cui si desidera richiamare, come nel seguente file default.rd.xml il metodo Get.  
  
    ```  
  
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
       <Application>  
          <Namespace Name="LibraryApplications"  Browse="Required Public" >  
             <Type Name="Book"   Activate="All" >  
                <Property Name="Title" Dynamic="Required" />  
                <Property Name="Author" Dynamic="Required" />  
                  <Property Name="ISBN" Dynamic="Required" />  
             </Type>  
          </Namespace>  
       </Application>  
    </Directives>  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di runtime direttive (RD. XML)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elementi direttiva di runtime](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Impostazioni dei criteri della direttiva di runtime](../../../docs/framework/net-native/runtime-directive-policy-settings.md)