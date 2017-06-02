---
title: "Elemento &lt;oidEntry&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/oidMap/oidEntry"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#oidEntry"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<oidEntry> (elemento)"
  - "oidEntry (elemento)"
ms.assetid: 22fb88b0-bf27-489c-9ca0-e65950ac136c
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;oidEntry&gt;
Esegue il mapping di un identificatore di oggetto \(OID\) ASN.1 su un nome descrittivo.  
  
## Sintassi  
  
```  
<oidEntry OID="object identifier number" name="friendly name" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|**OID**|Attributo obbligatorio.<br /><br /> Specifica l'identificatore OID ASN.1 corrispondente all'algoritmo implementato dalla classe.|  
|**name**|Attributo obbligatorio.<br /><br /> Specifica il valore per l'attributo **name** nel tag [\<nameEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md).|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`cryptographySettings`|Contiene le impostazioni di crittografia.|  
|`mscorlib`|Contiene l'elemento `cryptographySettings`.|  
|`oidMap`|Contiene i mapping degli identificatori di oggetto \(OID\) ASN.1 sulle classi.|  
  
## Note  
 Gli identificatori di oggetto ASN.1 identificano gli algoritmi in alcuni formati di crittografia.  Eseguire il mapping degli identificatori di oggetto sui nomi descrittivi per gli algoritmi da identificare.  Per ulteriori dettagli sugli identificatori di oggetto, consultare le informazioni in MSDN Library.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento **\<oidEntry\>** per eseguire il mapping di un identificatore di oggetto per l'algoritmo hash RIPEMD\-160 su un'implementazione di tale algoritmo hash.  
  
```  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RIPEMD-160" class="MyCrypto"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Schema delle impostazioni di crittografia](../../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)   
 [Servizi di crittografia](../../../../../docs/standard/security/cryptographic-services.md)   
 [Configurazione di classi di crittografia](../../../../../docs/framework/configure-apps/configure-cryptography-classes.md)   
 [Mapping di identificatori di oggetti ad algoritmi di crittografia](../../../../../docs/framework/configure-apps/map-object-identifiers-to-cryptography-algorithms.md)