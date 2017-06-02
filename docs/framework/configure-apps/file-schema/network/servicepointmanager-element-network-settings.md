---
title: "Elemento &lt;servicePointManager&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#servicePointManager"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/servicePointManager"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<servicePointManager> (elemento)"
  - "servicePointManager (elemento)"
ms.assetid: 6e5def51-3646-4ef6-a7bd-c69151321bec
caps.latest.revision: 16
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 16
---
# Elemento &lt;servicePointManager&gt; (Impostazioni di rete)
Configura le connessioni alle risorse di rete.  
  
## Sintassi  
  
```  
  
      <servicePointManager  
  checkCertificateName="true|false"  
  checkCertificateRevocationList="true|false"  
  encryptionPolicy="AllowNoEncryption|NoEncryption|RequireEncryption"  
  expect100Continue="true|false"  
  useNagleAlgorithm="true|false"  
  enableDnsRoundRobin="true|false"  
  dnsRefreshTimeout="time"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`checkCertificateName`|Specifica se il sistema deve verificare che il nome riportato sul certificato corrisponda al nome host del server prima di utilizzare il certificato.  Il valore predefinito è `true`.|  
|`checkCertificateRevocationList`|Specifica se il sistema deve verificare se il certificato è stato revocato prima che venisse utilizzato.  Il valore predefinito è `false`.|  
|`dnsRefreshTimeout`|Specifica l'intervallo di tempo, in millisecondi, durante il quale le risoluzioni Domain Name Service \(DNS\) vengono memorizzate nella cache insieme all'opzione Round robin DNS.  Il valore predefinito è 120.000 millisecondi \(due minuti\).|  
|`enableDnsRoundRobin`|Specifica se le risoluzioni DNS dei nomi host con più indirizzi IP \(Internet Protocol\) restituiscono tutti gli indirizzi o solo il primo.  Il valore predefinito è `false`.|  
|`encryptionPolicy`|Specifica i criteri di crittografia applicati a una sessione SSL\/TLS in un'istanza della classe <xref:System.Net.ServicePointManager>.  I valori possibili sono equivalenti ai valori per l'enumerazione <xref:System.Net.Security.EncryptionPolicy>.  L'utilizzo di <xref:System.Security.Authentication.CipherAlgorithmType> è necessario quando il criterio di crittografia è impostato su `NoEncryption`.  Il valore predefinito è `RequireEncryption`.|  
|`expect100Continue`|Specifica se i metodi POST devono prevedere di ricevere una risposta `100-continue` dal server.  Il valore predefinito è `true`.|  
|`useNagleAlgorithm`|Specifica se le connessioni controllate dal gestore dei punti di servizio utilizzano l'algoritmo Nagle.  Il valore predefinito è `true`.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[Impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.|  
  
## Note  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Vedere anche  
 <xref:System.Net.ServicePointManager>   
 <xref:System.Net.Security.EncryptionPolicy>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)