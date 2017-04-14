---
title: "Elemento &lt;iriParsing&gt; (Impostazioni URI) | Microsoft Docs"
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
ms.assetid: 953d0b53-445e-41f9-b302-77c4030852ce
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Elemento &lt;iriParsing&gt; (Impostazioni URI)
Specifica se l'analisi IRI \(International Resource Identifier\) viene applicata a un oggetto <xref:System.Uri> e se devono essere applicate le regole di analisi IRI.  
  
## Gerarchia dello schema  
 [Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [Elemento \<Uri\> \(impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
 [\<iriParsing\>](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)  
  
## Sintassi  
  
```  
<idn  
  enabled="true|false"  
/idn>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|`enabled`|Specifica se l'analisi IRI è attivata.  Il valore predefinito è `false`.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[uri](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)|Contiene impostazioni che specificano come vengono gestiti in .NET Framework gli indirizzi Web espressi tramite URI \(Uniform Resource Identifier\).|  
  
## Osservazioni  
 La classe esistente <xref:System.Uri> è stata estesa in .NET Framework 3.5, 3.0 SP1 e 2.0 SP1, per fornire il supporto per gli identificatori IRI \(International Resource Identifier\) e i nomi IDN \(Internationalized Domain Name\).  Gli utenti correnti non noteranno alcuna modifica rispetto al comportamento di .NET Framework 2.0, a meno che non attivino in modo specifico il supporto per IRI e IDN.  In questo modo viene assicurata la compatibilità dell'applicazione con le versioni precedenti di .NET Framework.  
  
 Per attivare il supporto IRI, sono necessarie le due modifiche seguenti:  
  
1.  Aggiungere la riga seguente al file machine.config nella directory di .NET Framework 2.0  
  
    ```  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2.  Specificare se devono essere applicate le regole di analisi IRI.  Questa operazione può essere effettuata nel file machine.config o app.config.  
  
 Abilitando l'analisi IRI \(iriParsing enabled \= `true`\) verranno effettuati la normalizzazione e il controllo dei caratteri in base alle regole IRI più recenti descritte nello standard RFC 3987.   Il valore predefinito è `false`\) e la normalizzazione e il controllo dei caratteri verranno effettuati in base agli standard RFC 2396 e RFC 3986 \(per i valori letterali IPv6\).  
  
### File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice seguente viene illustrata una configurazione utilizzata dalla classe <xref:System.Uri> per supportare l'analisi IRI e i nomi IDN.  
  
### Codice  
  
```  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
  </uri>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Configuration.IriParsingElement?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)