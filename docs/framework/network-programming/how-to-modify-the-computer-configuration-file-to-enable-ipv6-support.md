---
title: "Procedura: Modificare il file di configurazione del computer per abilitare il supporto IPv6 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 5611b677-b9cc-43b8-a434-60e18d89aada
caps.latest.revision: 18
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 18
---
# Procedura: Modificare il file di configurazione del computer per abilitare il supporto IPv6
Le esempio di codice seguente viene illustrato come modificare il file di configurazione di computer, *machine.config*, per il supporto IPv6.  Il file *machine.config* viene archiviato nella cartella *%Windir% \\ Microsoft.NET \\ Framework* nella directory in cui Windows è stato installato.  Esiste un file separato *machine.config* in cartelle in *%Windir% \\ Microsoft.NET \\ Framework* per ogni versione di .NET Framework installata nel computer, ad esempio *C:\\WINDOWS\\Microsoft.NET\\Framework\\v2.0 .50727 \\ machine.config*\).  
  
 Queste impostazioni possono essere effettuate nel file di configurazione dell'applicazione, che ha la precedenza sul file di configurazione del computer.  
  
 .NET Framework versione 1.1 e precedenti, il valore dell'opzione di configurazione **ipv6 enabled** specifica se membri degli indirizzi IPv6 della classe restituiscono <xref:System.Net.Dns?displayProperty=fullName>.  
  
 .NET Framework versione 2.0 e successive, se Windows supporta IPv6, tutti i membri della classe <xref:System.Net.Dns?displayProperty=fullName> \(ad esempio, il metodo <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=fullName> \), restituirà gli indirizzi IPv6 con una limitazione.  I membri obsoleti della classe <xref:System.Net.Dns?displayProperty=fullName> \(ad esempio, il metodo <xref:System.Net.Dns.Resolve%2A?displayProperty=fullName> \) e indicheranno riconosceranno il valore nel file di configurazione.  
  
> [!NOTE]
>  .NET Framework versione 2.0 e successive, è IPv6 è abilitato per impostazione predefinita.  Per.NET Framework 1.1 e versioni precedenti, il IPv6 è disabilitato per impostazione predefinita.  
  
## Esempio  
  
```  
<system.net>  
    …………  
    <settings>  
        …………  
        <ipv6 enabled="true"/>   
    ……………  
    </settings>  
    ………………  
<system.net>  
```  
  
## Vedere anche  
 [Indirizzamento IPv6](../../../docs/framework/network-programming/ipv6-addressing.md)   
 [Schema delle impostazioni di rete](../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [Elemento \<ipv6\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)