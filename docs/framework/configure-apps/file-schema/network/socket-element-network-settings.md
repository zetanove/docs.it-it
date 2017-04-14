---
title: "Elemento &lt;socket&gt; (Impostazioni di rete) | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/socket"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#socket"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<socket> (elemento)"
  - "socket (elemento)"
ms.assetid: 366c634c-7d16-478f-aedf-053eda94a1a0
caps.latest.revision: 21
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 21
---
# Elemento &lt;socket&gt; (Impostazioni di rete)
Specifica se le operazioni socket utilizzano porte di completamento.  
  
## Sintassi  
  
```  
  
      <socket  
  alwaysUseCompletionPortsForConnect="true|false"  
  alwaysUseCompletionPortsForAccept="true|false"  
  ipProtectionLevel ="EdgeRestricted|Restricted|Unrestricted|Unspecified"  
/socket>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attribute**|**Descrizione**|  
|-------------------|---------------------|  
|`alwaysUseCompletionPortsForAccept`|Indica se il socket deve utilizzare sempre porte di completamento per le chiamate al metodo Accept.  Il valore predefinito è `false`.|  
|`alwaysUseCompletionPortsForConnect`|Indica se il socket deve utilizzare sempre porte di completamento per le chiamate al metodo Connect.  Il valore predefinito è `false`.|  
|`ipProtectionLevel`|Specifica l'oggetto <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName> predefinito da utilizzare per un socket.  Il valore predefinito dipende dalla versione di Windows.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.|  
  
## Note  
 Gli attributi `alwaysUseCompletionPortsForAccept` e `alwaysUseCompletionPortsForConnect` vengono utilizzati per specificare il comportamento predefinito riguardante l'utilizzo di porte di completamento da parte delle classi in <xref:System.Net.Sockets?displayProperty=fullName>.namespace.  Sono inoltre consigliate per le applicazioni server a elevate prestazioni.  
  
 Il valore predefinito per gli attributi `alwaysUseCompletionPortsForAccept` e `alwaysUseCompletionPortsForConnect` è **false**.  
  
 La proprietà <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForAccept%2A> può essere utilizzata per ottenere il valore corrente dell'attributo `alwaysUseCompletionPortsForAccept` dai file di configurazione applicabili.  La proprietà <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForConnect%2A> può essere utilizzata per ottenere il valore corrente dell'attributo `alwaysUseCompletionPortsForConnect` dai file di configurazione applicabili.  
  
 L'attributo `ipProtectionLevel` specifica l'oggetto predefinito <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName> da utilizzare per un socket.  La proprietà <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A> consente la configurazione di una restrizione per un socket IPv6 a un ambito specificato, ad esempio gli indirizzi con lo stesso prefisso link\-local o site\-local.  Questa opzione consente alle applicazioni di applicare restrizioni di accesso ai socket IPv6.  Tali restrizioni consentono a un'applicazione in esecuzione su una LAN privata di proteggersi in modo semplice e affidabile da attacchi esterni.  Questa opzione allarga o restringe l'ambito di un socket in attesa, consentendo l'accesso illimitato di utenti pubblici e privati, laddove appropriato, o limitando l'accesso solo al medesimo sito, secondo le necessità.  
  
 L'impostazione dell'attributo `ipProtectionLevel` influisce solo sul traffico iniziale in ingresso:  
  
-   Un server TCP in attesa delle connessioni in ingresso su un socket.  
  
-   Un'applicazione UDP che riceve un pacchetto su un socket.  
  
 Tale impostazione di configurazione non influisce sulle connessioni TCP già stabilite \(il traffico è senza restrizioni in entrambe le direzioni\) e non ha effetti su un'applicazione che invia pacchetti UDP.  
  
 I valori possibili per l'impostazione dell'attributo `ipProtectionLevel` corrispondono ai livelli di protezione definiti specificati nell'enumerazione <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName> nel modo seguente:  
  
|||  
|-|-|  
|**Valore attributo**|**Descrizione**|  
|EdgeRestricted|Il livello di protezione IP è limitato dal perimetro.  Questo valore verrebbe utilizzato dalle applicazioni progettate per operare in Internet.  Questa impostazione non consente l'attraversamento NAT \(Network Address Translation\) tramite l'implementazione di Windows Teredo.  Tali applicazioni possono aggirare i firewall IPv4 e pertanto le applicazioni devono essere protette contro gli attacchi provenienti da Internet diretti alla porta aperta.  In Windows Server 2003 e in Windows XP, il valore predefinito per il livello di protezione IP in un socket è limitato dal perimetro.|  
|Restricted|Il livello di protezione IP è limitato.  Questo valore verrebbe utilizzato da applicazioni Intranet che non implementano scenari Internet.  Queste applicazioni non sono in genere testate o protette da attacchi analoghi a quelli provenienti da Internet.  Questa impostazione limiterà il traffico ricevuto solo a quello locale rispetto al collegamento.|  
|Illimitato|Il livello di protezione IP è illimitato.  Questo valore verrebbe utilizzato dalle applicazioni progettate per operare in Internet, incluse la applicazioni che usufruiscono delle funzionalità di attraversamento NAT IPv6 compilate in Windows \(ad esempio, Teredo\).  Tali applicazioni possono aggirare i firewall IPv4 e pertanto le applicazioni devono essere protette contro gli attacchi provenienti da Internet diretti alla porta aperta.  In Windows Server 2008 R2 e in Windows Vista, il valore predefinito per il livello di protezione IP in un socket è illimitato.|  
|Non specificato|Il livello di protezione IP non è specificato.  In Windows 7 e in Windows Server 2008 R2, il valore predefinito per il livello di protezione IP in un socket non è specificato.|  
  
 Il valore predefinito per l'attributo `ipProtectionLevel` è **Unspecified**.  
  
 La proprietà <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A> può essere utilizzata per ottenere il valore corrente dell'attributo `ipProtectionLevel` dai file di configurazione applicabili.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrato come specificare che è necessario utilizzare le porte di completamento e che il <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName> predefinito non deve avere restrizioni.  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <socket  
        alwaysUseCompletionPortsForAccept="true"  
        alwaysUseCompletionPortsForConnect="true"  
        ipProtectionLevel="Unrestricted"  
       />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net?displayProperty=fullName>   
 <xref:System.Net.Configuration.SocketElement?displayProperty=fullName>   
 <xref:System.Net.Sockets?displayProperty=fullName>   
 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName>   
 <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)