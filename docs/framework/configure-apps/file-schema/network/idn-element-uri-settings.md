---
title: "Elemento &lt;idn&gt; (Impostazioni URI) | Microsoft Docs"
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
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;idn&gt; (Impostazioni URI)
Specifica se l'analisi IDN \(Internationalized Domain Name\) viene applicata a un nome di dominio.  
  
## Gerarchia dello schema  
 [Elemento \<Configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [Elemento \<Uri\> \(impostazioni URI\)](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
 [\<idn\>](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)  
  
## Sintassi  
  
```  
<idn  
  enabled="All|AllExceptIntranet|None"  
/idn>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|`enabled`|Specifica se l'analisi IDN \(Internationalized Domain Name\) viene applicata a un nome di dominio. Il valore predefinito è None.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[uri](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)|Contiene impostazioni che specificano come vengono gestiti in .NET Framework gli indirizzi Web espressi tramite URI \(Uniform Resource Identifier\).|  
  
## Osservazioni  
 La classe esistente <xref:System.Uri> è stata estesa in .NET Framework 3.5, 3.0 SP1 e 2.0 SP1, con il supporto per gli identificatori IRI \(International Resource Identifier\) e i nomi IDN \(Internationalized Domain Name\).  Gli utenti correnti non noteranno alcuna modifica rispetto al comportamento di .NET Framework 2.0, a meno che non attivino in modo specifico il supporto per IRI e IDN.  In questo modo viene assicurata la compatibilità dell'applicazione con le versioni precedenti di .NET Framework.  
  
 Per attivare il supporto IRI, sono necessarie le due modifiche seguenti:  
  
1.  Aggiungere la riga seguente al file machine.config nella directory di .NET Framework 2.0  
  
    ```  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2.  Specificare se si desidera applicare l'analisi IDN \(Internationalized Domain Name\) al nome di dominio nonché le regole di analisi IRI.  Questa operazione può essere effettuata nel file machine.config o app.config.  
  
 Esistono tre valori possibili per IDN, a seconda dei server DNS utilizzati:  
  
-   idn enabled \= All  
  
     Questo valore convertirà qualsiasi nome di dominio Unicode negli equivalenti Punycode \(nomi IDN\).  
  
-   idn enabled \= AllExceptIntranet  
  
     Questo valore convertirà tutti i nomi di dominio Unicode non presenti sulla rete Intranet locale affinché utilizzino gli equivalenti Punycode \(nomi IDN\).  In questo caso, per gestire nomi internazionali sulla rete Intranet locale, è necessario che i server DNS utilizzati per la rete Intranet supportino la risoluzione dei nomi Unicode.  
  
-   idn enabled \= None  
  
     Questo valore non convertirà alcun nome di dominio Unicode per l'utilizzo di Punycode  Si tratta del valore predefinito coerente con il comportamento di .NET Framework 2.0.  
  
 Se si attiva IDN, tutte le etichette Unicode in un nome di dominio verranno convertite negli equivalenti nomi Punycode,  I nomi Punycode contengono solo caratteri ASCII e vengono sempre avviati con il prefisso xn\-\-  allo scopo di supportare i server DNS esistenti su Internet, poiché la maggior parte dei server DNS supporta solo caratteri ASCII \(vedere RFC 3940\).  
  
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
 <xref:System.Configuration.IdnElement?displayProperty=fullName>   
 <xref:System.Configuration.UriSection?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)