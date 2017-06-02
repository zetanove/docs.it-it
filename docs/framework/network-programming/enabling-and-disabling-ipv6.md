---
title: "Abilitazione e disabilitazione di IPv6 | Microsoft Docs"
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
ms.assetid: 6408d3ef-c9ba-49d9-b15e-fe74bd3ef031
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Abilitazione e disabilitazione di IPv6
Per utilizzare il protocollo IPv6, assicurarsi che si esegue una versione del sistema operativo che supporta IPv6 e assicurarsi che il sistema operativo e le classi di rete siano configurate correttamente.  
  
## Passaggi di configurazione  
 Nella tabella seguente sono elencate le varie configurazioni  
  
|Sistema operativo IPv6\-enabled?|La rete le classi IPv6\-enabled?|Descrizione|  
|--------------------------------------|--------------------------------------|-----------------|  
|No|No|È possibile analizzare gli indirizzi IPv6.|  
|No|Sì|È possibile analizzare gli indirizzi IPv6.|  
|Sì|No|È possibile analizzare gli indirizzi IPv6 e risolvere gli indirizzi IPv6 utilizzando obsoleto non contrassegnato metodi di risoluzione dei nomi.|  
|Sì|Sì|È possibile analizzare e correggere gli indirizzi IPv6 utilizzando tutti i metodi inclusi quelli ha contrassegnato come obsoleto.|  
  
 Tenere presente che per attivare il supporto IPv6 a tutte le classi nello spazio dei nomi di System.Net, è necessario modificare il file di configurazione del computer o il file di configurazione per l'applicazione.  Il file di configurazione per un'applicazione ha la precedenza sul file di configurazione del computer.  
  
 Per un esempio di come modificare il file di configurazione di computer, *machine.config*, per il supporto Ipv6 vedere, [Procedura: Modificare il file di configurazione del computer per abilitare il supporto Ipv6](../../../docs/framework/network-programming/how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md).  Inoltre, assicurarsi che il supporto IPv6 è abilitato per il sistema operativo.  
  
 .NET Framework include un'opzione di configurazione impostata in un file di configurazione riportato  
  
```  
<system.net>…  
    <settings>…  
        <ipv6 enabled="true"/>…  
    </settings>…  
</system.net>  
```  
  
 .NET Framework versione 1.1 e precedenti, il valore dell'opzione di configurazione **ipv6 enabled** specifica se membri degli indirizzi IPv6 della classe restituiscono <xref:System.Net.Dns?displayProperty=fullName>.  
  
 .NET Framework versione 2.0 e successive, se Windows supporta IPv6, i membri della classe <xref:System.Net.Dns?displayProperty=fullName>, ad esempio, il metodo <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=fullName> \), restituirà gli indirizzi IPv6 con una limitazione.  I membri obsoleti il DNS <xref:System.Net.Dns?displayProperty=fullName> \(ad esempio, il metodo <xref:System.Net.Dns.Resolve%2A?displayProperty=fullName> \) e indicheranno riconosceranno il valore nel file di configurazione dell'impostazione abilitata ipv6.  
  
## Vedere anche  
 [Protocollo IPv6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)   
 [Schema delle impostazioni di rete](../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [Elemento \<ipv6\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)