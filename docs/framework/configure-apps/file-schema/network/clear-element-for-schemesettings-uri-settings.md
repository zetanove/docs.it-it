---
title: "Elemento &lt;clear&gt; per schemeSettings (impostazioni URI) | Microsoft Docs"
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
ms.assetid: 65098332-ce61-4542-ab8d-e7dc0257d31f
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Elemento &lt;clear&gt; per schemeSettings (impostazioni URI)
Deseleziona tutte le impostazioni dello schema esistenti.  
  
## Sintassi  
  
```  
  
<clear/>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<schemeSettings\> \(impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|Specifica come un oggetto <xref:System.Uri> verrà analizzato per schemi specifici.|  
  
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
 Nell'esempio di codice seguente viene mostrata una configurazione utilizzata dalla classe <xref:System.Uri> che cancella tutte le impostazioni dello schema e quindi viene aggiunto il supporto per non eseguire l'operazione di escape dei delimitatori di percorso con codifica percentuale dello schema HTTP.  
  
```  
<configuration>  
  <uri>  
    <schemeSettings>  
      <clear/>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Configuration.SchemeSettingElement?displayProperty=fullName>   
 <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=fullName>   
 <xref:System.GenericUriParserOptions?displayProperty=fullName>   
 <xref:System.Uri?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)