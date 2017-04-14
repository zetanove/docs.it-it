---
title: "&lt;declaredTypes&gt; | Microsoft Docs"
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
  - "elemento <declaredTypes>"
  - "DataContractSerializer"
  - "elemento dataContractSerializer"
  - "elemento declaredTypes"
  - "KnownTypes"
ms.assetid: f35184e4-9d9e-4d37-8fb4-d5b58220eb3e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;declaredTypes&gt;
Contiene i tipi noti usati dal serializzatore <xref:System.Runtime.Serialization.DataContractSerializer> durante la deserializzazione.  
  
 Per altre informazioni sui contratti di dati e sui tipi noti, vedere [Tipi conosciuti di contratto dati](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  
  
## Sintassi  
  
```  
  
<configuration>  
  <system.runtime.serialization>  
    <dataContractSerializer>  
      <declaredTypes>  
        <add type="String ">  
          <knownType type="String">  
                <parameter index="Integer"/>  
          </knownType>  
        </add>  
      </declaredTypes>  
    <dataContractSerializer>  
  </system.runtime.serialization>  
</configuration>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)|Aggiunge tipi che richiedono tipi noti.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-of-system-runtime-serialization.md)|Contiene dati di configurazione per <xref:System.Runtime.Serialization.DataContractSerializer>.|  
  
## Note  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] sui tipi noti, vedere [Tipi conosciuti di contratto dati](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md) e <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
## Esempio  
 Il codice XML seguente illustra l'aggiunta di tipi dichiarati e di tipi noti a un elemento `DataContractSerializer` .  In particolare, l'esempio illustra l'aggiunta di tre tipi.  Il primo è un tipo personalizzato denominato "Orders" che usa un tipo conosciuto denominato "Item".  Il secondo tipo dichiarato è un elenco <xref:System.Collections.Generic.List%601> che usa `Item` come tipo conosciuto.  Infine, il terzo tipo dichiarato è un dizionario <xref:System.Collections.Generic.Dictionary%602>.  Il tipo della classe <xref:System.Collections.Generic.Dictionary%602> è un tipo generico, con due parametri di tipo.  Il primo rappresenta la chiave e il secondo rappresenta il valore.  Nell'esempio seguente viene aggiunto un elenco <xref:System.Collections.Generic.List%601> del secondo tipo \(ovvero il valore\) all'elenco dei tipi noti.  È necessario usare l'attributo `index` per specificare quale parametro di tipo usare nel tipo conosciuto.  In questo caso, il tipo di valore viene indicato impostando l'attributo index su "1", in quanto la raccolta è in base zero.  
  
```  
<configuration>  
  <system.runtime.serialization>  
    <dataContractSerializer>  
      <declaredTypes>  
        <add type="Examples.Types.Orders, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
          <knownType type="Examples.Types.Item, SerializationTypes, Version=2.0.0.0, Culture=neutral, PublicKey=null" />  
        </add>  
        <add type="System.Collections.Generic.List`1, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
          <knownType type="Examples.Types.Item, SerializationTypes, Version=2.0.0.0, Culture=neutral, PublicKey=null" />  
        </add>  
        <add type="System.Collections.Generic.Dictionary`2, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
          <knownType type="System.Collections.Generic.List`1, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">  
            <parameter index="1"/>  
          </knownType>  
        </add>  
      </declaredTypes>  
    <dataContractSerializer>  
  </system.runtime.serialization>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [\<dataContractSerializer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-element.md)   
 [Tipi conosciuti di contratto dati](../../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-declaredtypes-element.md)