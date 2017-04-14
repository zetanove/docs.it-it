---
title: "Elemento &lt;Uri&gt; (impostazioni URI) | Microsoft Docs"
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
ms.assetid: c22bab8b-477c-4ae4-8498-65ad409e0847
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;Uri&gt; (impostazioni URI)
Contiene impostazioni che specificano come vengono gestiti in .NET Framework gli indirizzi Web espressi tramite URI \(Uniform Resource Identifier\).  
  
## Gerarchia dello schema  
 [Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<uri\>](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
## Sintassi  
  
```  
<uri>  
</uri>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[non](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)|Specifica se l'analisi IDN \(Internationalized Domain Name\) viene applicata ai nomi di dominio.|  
|[iriParsing](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)|Specifica se l'analisi IRI \(International Resource Identifier\) viene applicata a <xref:System.Uri> e se devono essere applicate le regole di analisi IRI.|  
|[schemeSettings](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|Specifica come un oggetto <xref:System.Uri> verrà analizzato per schemi specifici.|  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[configurazione](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Contiene impostazioni per tutti gli spazi dei nomi.|  
  
## Note  
 L'elemento `uri` contiene impostazioni per i membri della classe <xref:System.Uri> utilizzata dalle classi nello spazio dei nomi <xref:System.Net>.  Le impostazioni configurano il supporto per IRI e IDN.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice seguente viene illustrata una configurazione utilizzata dalla classe <xref:System.Uri> per supportare l'analisi IRI e i nomi IDN.  Nell'esempio vengono inoltre cancellate tutte le impostazioni dello schema e quindi viene aggiunto il supporto per non eseguire l'operazione di escape dei delimitatori di percorso con codifica percentuale dello schema HTTP.  
  
### Codice  
  
```  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
    <schemeSettings>  
      <clear/>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)