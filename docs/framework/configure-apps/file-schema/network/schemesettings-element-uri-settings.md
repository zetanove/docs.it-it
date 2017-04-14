---
title: "Elemento &lt;schemeSettings&gt; (impostazioni URI) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 0ae45c6e-8c4c-4c0d-8b9f-a93824648890
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Elemento &lt;schemeSettings&gt; (impostazioni URI)
Specifica come un oggetto <xref:System.Uri> verrà analizzato per schemi specifici.  
  
## Sintassi  
  
```  
  
      <schemeSettings>   
</schemeSettings>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 None  
  
### Elementi figlio  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[aggiunta](../../../../../docs/framework/configure-apps/file-schema/network/add-element-for-schemesettings-uri-settings.md)|Aggiunge un'impostazione dello schema per un nome di schema.|  
|[clear](../../../../../docs/framework/configure-apps/file-schema/network/clear-element-for-schemesettings-uri-settings.md)|Deseleziona tutte le impostazioni dello schema esistenti.|  
|[remove](../../../../../docs/framework/configure-apps/file-schema/network/remove-element-for-schemesettings-uri-settings.md)|Aggiunge un'impostazione dello schema per un nome di schema.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[uri](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)|Contiene impostazioni che specificano come vengono gestiti in .NET Framework gli indirizzi Web espressi tramite URI \(Uniform Resource Identifier\).|  
  
## Note  
 Per impostazione predefinita, la classe <xref:System.Uri?displayProperty=fullName> priva dei caratteri escape i delimitatori del percorso con codifica percentuale prima di eseguire la compressione del percorso.  È stato implementato come meccanismo di sicurezza rispetto ad attacchi simili ai seguenti:  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Se questo URI viene passato lungo i moduli che non gestiscono correttamente i caratteri codificati in percentuale, potrebbe verificarsi che il comando seguente venga eseguito dal server:  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 Per questo motivo, la classe <xref:System.Uri?displayProperty=fullName> come prima cosa priva dei caratteri escape i delimitatori del percorso, quindi applica compressione del percorso.  Il risultato di passare l'URL dannoso al costruttore di classe <xref:System.Uri?displayProperty=fullName> è il seguente URI:  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 È possibile modificare questo comportamento predefinito per non consentire l'escape dei delimitatori del percorso con codifica percentuale utilizzando l'opzione di configurazione schemeSettings per uno specifico schema.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice seguente viene mostrata una configurazione utilizzata dalla classe <xref:System.Uri> per il supporto di non eseguire l'operazione di escape dei delimitatori di percorso con codifica percentuale dello schema HTTP.  
  
```  
<configuration>  
  <uri>  
    <schemeSettings>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## Informazioni sull'elemento  
  
|||  
|-|-|  
|Spazio dei nomi|Sistema|  
|Nome di schema||  
|File di convalida||  
|Può essere vuoto||  
  
## Vedere anche  
 <xref:System.Configuration.SchemeSettingElement?displayProperty=fullName>   
 <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=fullName>   
 <xref:System.GenericUriParserOptions?displayProperty=fullName>   
 <xref:System.Uri?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)