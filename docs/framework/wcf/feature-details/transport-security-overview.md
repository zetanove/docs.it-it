---
title: "Panoramica sulla sicurezza del trasporto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00959326-aa9d-44d0-af61-54933d4adc7f
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# Panoramica sulla sicurezza del trasporto
I meccanismi di sicurezza del trasporto di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] dipendono dall'associazione e dal trasporto utilizzati. Ad esempio, quando si utilizza il <xref:System.ServiceModel.WSHttpBinding> (classe), il trasporto è HTTP e il meccanismo principale per la sicurezza del trasporto è Secure Sockets Layer (SSL) su HTTP, comunemente noto come HTTPS. In questo argomento vengono illustrati i principali meccanismi di sicurezza del trasporto utilizzati nelle associazioni fornite dal sistema [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
> [!NOTE]
>  Quando viene utilizzata la sicurezza SSL con .NET Framework 3.5 e versioni successive, un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza sia i certificati intermedi presenti nel proprio archivio certificati che quelli ricevuti durante la negoziazione SSL per eseguire la convalida della catena di certificati sul certificato del servizio. In .NET Framework 3.0 vengono usati solo i certificati intermedi installati nell'archivio certificati locale.  
  
> [!WARNING]
>  Quando viene utilizzata la sicurezza del trasporto, il <xref:System.Treading.Thread.CurrentPrincipal%2A> proprietà può essere sovrascritte. Per evitare questo problema, impostare il <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermission%2A> su None. <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> è un comportamento del servizio che può essere impostato sulla descrizione del servizio.  
  
## <a name="basichttpbinding"></a>BasicHttpBinding  
 Per impostazione predefinita, il <xref:System.ServiceModel.BasicHttpBinding> classe non fornisce la sicurezza. Questa associazione è progettata per essere interoperabile con i provider di servizi Web che non implementano funzionalità di sicurezza. Tuttavia, è possibile passare in sicurezza impostando il <xref:System.ServiceModel.BasicHttpSecurity.Mode%2A> su qualsiasi valore eccetto <xref:System.ServiceModel.BasicHttpSecurityMode>. Per abilitare la sicurezza del trasporto, impostare la proprietà su <xref:System.ServiceModel.BasicHttpSecurityMode>.  
  
### <a name="interoperation-with-iis"></a>Interazione con IIS  
 Il <xref:System.ServiceModel.BasicHttpBinding> classe viene utilizzata principalmente per interagire con i servizi Web esistenti e molti di questi servizi sono ospitati da Internet Information Services (IIS). Di conseguenza, la sicurezza del trasporto per questa associazione è progettata per interagire senza difficoltà con i siti IIS. Questa operazione viene eseguita impostando la modalità di sicurezza <xref:System.ServiceModel.BasicHttpSecurityMode> e quindi impostando tipo di credenziale client. I valori relativi al tipo di credenziale corrispondono ai meccanismi di sicurezza directory ISS. Nel codice seguente viene illustrata l'impostazione della modalità e del tipo di credenziale su Windows. È possibile utilizzare questa configurazione quando il client e il server si trovano nello stesso dominio Windows.  
  
 [!code-csharp[c_ProgrammingSecurity#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#10)]
 <!-- TODO: review snippet reference [!code-vb[c_ProgrammingSecurity#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#10)]  -->  
  
 oppure in configurazione:  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <binding name="SecurityByTransport">  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" />  
       </security>  
     </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 Nelle sezioni seguenti vengono illustrati altri tipi di credenziali client.  
  
#### <a name="basic"></a>Di base  
 Questo tipo corrisponde al metodo di autenticazione di base di IIS. Quando si utilizza questa modalità, il server IIS deve essere configurato con gli account utente di Windows e le autorizzazioni del file system NTFS appropriate. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], vedere [abilitazione dell'autenticazione di base e configurazione del nome dell'area di autenticazione](http://go.microsoft.com/fwlink/?LinkId=88592). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], vedere [IIS 7.0 Beta: configurare l'autenticazione di base](http://go.microsoft.com/fwlink/?LinkId=88593).  
  
#### <a name="certificate"></a>Certificato  
 In IIS è disponibile un'opzione affinché i client debbano eseguire l'accesso con un certificato. Questa funzionalità consente inoltre di eseguire il mapping di un certificato client a un account di Windows. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], vedere [abilitazione dei certificati Client in IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88594). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], vedere [IIS 7.0 Beta: configurazione dei certificati del Server in IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=88595).  
  
#### <a name="digest"></a>Digest  
 L'autenticazione digest è simile all'autenticazione di base, ma offre il vantaggio di inviare le credenziali come un hash, anziché in testo non crittografato. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], vedere [l'autenticazione del Digest in IIS 6.0](http://go.microsoft.com/fwlink/?LinkID=88443). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], vedere [IIS 7.0 Beta: configurazione dell'autenticazione Digest](http://go.microsoft.com/fwlink/?LinkId=88596).  
  
#### <a name="windows"></a>Windows  
 Questo tipo corrisponde al metodo di autenticazione integrata di Windows di IIS. In caso di impostazione su questo valore, si prevede inoltre che il server sia in un dominio Windows che utilizza il protocollo Kerberos come controller di dominio. Se il server non è in un dominio con supporto Kerberos o se il sistema Kerberos ha esito negativo, è possibile utilizzare il valore NTLM (NT LAN Manager) descritto nella sezione successiva. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], vedere [l'autenticazione Windows integrata in IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88597). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], vedere [IIS 7.0 Beta: configurazione dei certificati del Server in IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=88595).  
  
#### <a name="ntlm"></a>NTLM  
 Consente al server di utilizzare NTLM per l'autenticazione se il protocollo Kerberos ha esito negativo. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]configurazione di IIS in [!INCLUDE[iis601](../../../../includes/iis601-md.md)], vedere [forzatura dell'autenticazione NTLM](http://go.microsoft.com/fwlink/?LinkId=88598). Per [!INCLUDE[iisver](../../../../includes/iisver-md.md)], l'autenticazione di Windows include l'autenticazione NTLM. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][IIS 7.0 Beta: configurazione dei certificati del Server in IIS 7.0](http://go.microsoft.com/fwlink/?LinkID=88595).  
  
## <a name="wshttpbinding"></a>WsHttpBinding  
 Il <xref:System.ServiceModel.WSHttpBinding> classe è progettata per l'interoperabilità con servizi che implementano WS-* specifiche. La sicurezza basata sul trasporto di questa associazione è SSL (Secure Sockets Layer) su HTTP, ovvero HTTPS. Per creare un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che utilizza SSL, utilizzare IIS per ospitarla. In alternativa, se si sta creando un'applicazione indipendente, utilizzare lo strumento HttpCfg.exe per associare un certificato X.509 a una porta specifica in un computer. Il numero della porta viene specificato all'interno dell'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] come indirizzo dell'endpoint. Quando si utilizza la modalità di trasporto, l'indirizzo dell'endpoint deve includere il protocollo HTTPS; in caso contrario verrà generata un'eccezione in fase di esecuzione. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Sicurezza del trasporto HTTP](../../../../docs/framework/wcf/feature-details/http-transport-security.md).  
  
 Per l'autenticazione client, impostare il <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> proprietà del <xref:System.ServiceModel.HttpTransportSecurity> classe a una del <xref:System.ServiceModel.HttpClientCredentialType> valori di enumerazione. I valori di enumerazione sono identici ai tipi di credenziali client per <xref:System.ServiceModel.BasicHttpBinding> e sono progettati per essere ospitati nei servizi IIS.  
  
 Nell'esempio seguente viene illustrata l'associazione utilizzata con un tipo di credenziale client di Windows.  
  
 [!code-csharp[c_ProgrammingSecurity#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#11)]
 [!code-vb[c_ProgrammingSecurity#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#11)]  
  
## <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 Questa associazione fornisce sicurezza solo a livello di messaggio, non a livello di trasporto.  
  
## <a name="nettcpbinding"></a>NetTcpBinding  
 Il <xref:System.ServiceModel.NetTcpBinding> classe utilizza TCP per il trasporto dei messaggi. La sicurezza per la modalità di trasporto viene fornita implementando il protocollo TLS (Transport Layer Security) su TCP. L'implementazione di TLS viene fornita dal sistema operativo.  
  
 È inoltre possibile specificare il tipo di credenziali del client impostando il <xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A> proprietà del <xref:System.ServiceModel.TcpTransportSecurity> classe a una del <xref:System.ServiceModel.TcpClientCredentialType> valori, come illustrato nel codice seguente.  
  
 [!code-csharp[c_ProgrammingSecurity#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#12)]
 [!code-vb[c_ProgrammingSecurity#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#12)]  
  
#### <a name="client"></a>Client  
 Sul client, è necessario specificare un certificato utilizzando il <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> metodo il <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential> (classe).  
  
> [!NOTE]
>  Se si utilizza la sicurezza di Windows, non è necessario un certificato.  
  
 Nel codice seguente viene utilizzata l'identificazione digitale del certificato, che lo identifica in modo univoco. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]i certificati, vedere [utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 [!code-csharp[c_ProgrammingSecurity#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#13)]
 [!code-vb[c_ProgrammingSecurity#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#13)]  
  
 In alternativa, specificare il certificato nella configurazione del client utilizzando un [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) elemento nella sezione dei comportamenti.  
  
```xml  
<behaviors>  
  <behavior>  
   <clientCredentials>  
     <clientCertificate findValue= "101010101010101010101010101010000000000"   
      storeLocation="LocalMachine" storeName="My"   
      X509FindType="FindByThumbPrint"/>  
     </clientCertificate>  
   </clientCredentials>  
 </behavior>  
</behaviors>    
```  
  
## <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 Il <xref:System.ServiceModel.NetNamedPipeBinding> classe è progettata per consentire una comunicazione efficiente intra-computer, ovvero per i processi in esecuzione nello stesso computer, sebbene canali named pipe è possibile creare tra due computer nella stessa rete. Questa associazione fornisce sicurezza solo a livello di trasporto. Quando si creano applicazioni utilizzando questa associazione, gli indirizzi di endpoint devono includere "net.pipe" come protocollo.  
  
## <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 Quando si utilizza la sicurezza del trasporto, questa associazione utilizza SSL su HTTP, noto come HTTPS, con un token emesso (<xref:System.ServiceModel.WSFederationHttpSecurityMode>). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]applicazioni federate, vedere [federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).  
  
## <a name="netpeertcpbinding"></a>NetPeerTcpBinding  
 Il <xref:System.ServiceModel.NetPeerTcpBinding> classe costituisce un trasporto protetto progettato per consentire una comunicazione efficiente utilizzando la funzionalità di rete peer-to-peer. Come indicato dal nome della classe e dell'associazione, il protocollo è TCP. Quando la modalità di sicurezza è impostata su Trasporto, l'associazione implementa TLS su TCP. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]la funzionalità peer-to-peer, vedere [Peer-to-Peer Networking](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## <a name="msmqintegrationbinding-and-netmsmqbinding"></a>MsmqIntegrationBinding e NetMsmqBinding  
 Per una descrizione completa del trasporto con Accodamento messaggi (precedentemente chiamato MSMQ), protezione vedere [protezione dei messaggi mediante protezione del trasporto](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione della sicurezza WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)