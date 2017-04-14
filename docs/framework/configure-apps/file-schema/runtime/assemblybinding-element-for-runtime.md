---
title: "Elemento &lt;assemblyBinding&gt; per &lt;runtime&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<assemblyBinding> (elemento)"
  - "assemblyBinding (elemento)"
  - "tag contenitore, <assemblyBinding> (elemento)"
ms.assetid: 964cbb35-ab49-4498-8471-209689e5dada
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Elemento &lt;assemblyBinding&gt; per &lt;runtime&gt;
Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.  
  
## Sintassi  
  
```  
  
        <assemblyBinding    
   xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
</assemblyBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**xmlns**|Attributo obbligatorio.<br /><br /> Specifica lo spazio dei nomi XML necessario per il binding di assembly.  Usare la stringa "urn:schemas\-microsoft\-com:asm.v1" come valore.|  
|**appliesTo**|Specifica la versione di runtime a cui si applica il reindirizzamento di assembly .NET Framework.  Questo attributo facoltativo usa un numero di versione di .NET Framework per indicare la versione a cui deve essere applicato.  Se non si specifica alcun attributo **appliesTo**, l'elemento **\<assemblyBinding\>** viene applicato a tutte le versioni di .NET Framework.  L'attributo **appliesTo** è stato introdotto in .NET Framework versione 1.1 e viene ignorato dalla versione 1.0.  Quando si usa .NET Framework versione 1.0, vengono quindi applicati tutti gli elementi **\<assemblyBinding\>**, anche se viene specificato un attributo **appliesTo**.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<dependentAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md)|Incapsula i criteri di binding e il percorso dell'assembly per ciascun assembly.  Utilizzare un tag **\<dependentAssembly\>** per ciascun assembly.|  
|[\<probing\>](../../../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md)|Specifica le sottodirectory in cui in Common Language Runtime viene effettuata la ricerca al momento del caricamento degli assembly.|  
|[\<publisherPolicy\>](../../../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md)|Specifica se il runtime applica i criteri dell'editore.|  
|[\<qualifyAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/qualifyassembly-element.md)|Specifica il nome completo dell'assembly da caricare in modo dinamico quando viene usato un nome parziale.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione usato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Esempio  
 L'esempio seguente illustra come reindirizzare una versione dell'assembly a un'altra versione e fornire un elemento codeBase.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
            <codeBase version="2.0.0.0"  
                      href="http://www.litwareinc.com/myAssembly.dll"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 L'esempio che segue illustra l'uso dell'attributo **appliesTo** per reindirizzare l'associazione di un assembly di .NET Framework.  
  
```  
<runtime>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
      <dependentAssembly>   
         <assemblyIdentity name="mscorcfg" publicKeyToken="b03f5f7f11d50a3a" culture=""/>  
         <bindingRedirect oldVersion="0.0.0.0-65535.65535.65535.65535" newVersion="1.0.3300.0"/>  
      </dependentAssembly>  
   </assemblyBinding>  
</runtime>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)