---
title: "&lt;transport&gt; di &lt;netTcpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49462e0a-66e1-463f-b3e1-c83a441673c6
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# &lt;transport&gt; di &lt;netTcpBinding&gt;
Definisce il tipo di requisiti di sicurezza a livello di messaggio di un endpoint configurato con l'[\<netTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).  
  
## Sintassi  
  
```  
<netTcpBinding>  
    <binding>  
        <security  
         mode="None|Transport|Message|TransportWithMessageCredential">  
            <transport clientCredentialType="None|Windows|Certificate"  
             protectionLevel="None|Sign|EncryptAndSign"  
             sslProtocols="Ssl3|Tls|Tls11|Tls12">  
                <extendedProtectionPolicy  
                     policyEnforcement="Never|WhenSupported|Always"  
                     protectionScenario="TransportSelected|TrustedProxy">  
                    <customServiceNames></customServiceNames>  
                        </extendedProtectionPolicy>  
            </transport>  
        </security>  
    </binding>  
</netTcpBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|clientCredentialType|Parametro facoltativo.  Specifica il tipo di credenziale da usare se l'autenticazione client viene eseguita usando la sicurezza del trasporto.<br /><br /> -   Il valore predefinito è `Windows`.<br />-   L'attributo è di tipo <xref:System.ServiceModel.TcpClientCredentialType>.|  
|protectionLevel|Parametro facoltativo.  Definisce il livello di sicurezza del trasporto TCP.  La firma dei messaggi riduce il rischio di manomissione da parte di terzi durante il trasferimento.  La crittografia fornisce riservatezza a livello di dati durante il trasporto.<br /><br /> Il valore predefinito è `EncryptAndSign`.|  
|sslProtocols|Valore del flag di enumerazione SslProtocols che specifica gli elementi SslProtocol supportati.  L'impostazione predefinita è Ssl3&#124;Tls&#124;Tls11&#124;Tls12.|  
|policyEnforcement|Questa enumerazione specifica il momento in cui deve essere applicato l'oggetto <xref:System.Security.Authentication.ExtendedProtectionPolicy>.<br /><br /> 1.  Never – I criteri non vengono mai applicati e la protezione estesa è disabilitata.<br />2.  WhenSupported – I criteri vengono applicati solo se il client supporta la protezione estesa.<br />3.  Always \- I criteri vengono sempre applicati.  L'autenticazione dei client che non supportano la protezione estesa avrà esito negativo.|  
  
## Attributo clientCredentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|Il client è anonimo.  Richiede un certificato per il servizio.|  
|Windows|Specifica l'autenticazione Windows del client mediante la negoziazione SP \(negoziazione Kerberos\).|  
|Certificato|Il client viene autenticato mediante un certificato.  Viene usata la negoziazione SSL ed è necessario un certificato per il servizio.|  
  
## Attributo protectionLevel  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|Nessuna protezione.|  
|Sign|I messaggi vengono firmati.|  
|EncryptAndSign|-   I messaggi vengono crittografati e firmati.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)|Consente di specificare le funzionalità di sicurezza dell'[\<netTcpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).|  
  
## Note  
 Usare la sicurezza del trasporto garantire l'integrità e la riservatezza del messaggio SOAP, nonché l'esecuzione dell'autenticazione reciproca.  Se questa modalità di sicurezza viene selezionata per un'associazione, lo stack di canali viene configurato in modo da usare un trasporto protetto nonché proteggere i messaggi SOAP tramite una sicurezza di trasporto quale Windows \(Negotiate\) o SSL su TCP.  
  
## Vedere anche  
 <xref:System.ServiceModel.TcpTransportSecurity>   
 <xref:System.ServiceModel.Configuration.NetTcpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.NetTcpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.NetTcpTransportSecurityElement>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)