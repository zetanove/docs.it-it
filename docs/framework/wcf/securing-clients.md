---
title: "Protezione di client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "client [WCF], considerazioni sulla protezione"
ms.assetid: 44c8578c-9a5b-4acd-8168-1c30a027c4c5
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# Protezione di client
In [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], il servizio impone i requisiti di sicurezza per i client.Ovvero specifica quale modalità di sicurezza utilizzare e se il client deve fornire o meno una credenziale.Il processo di protezione di un client, pertanto, è semplice: utilizzare i metadati ottenuti dal servizio \(se è pubblicato\) e generare un client.I metadati specificano come configurare il client.Se il servizio richiede al client di fornire una credenziale, è necessario ottenerne una che corrisponda al requisito.In questo argomento viene descritto il processo in modo dettagliato.[!INCLUDE[crabout](../../../includes/crabout-md.md)] creazione di un servizio protetto, vedere [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md).  
  
## Il servizio specifica la protezione  
 Le associazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] hanno le funzionalità di sicurezza attive per impostazione predefinita,a eccezione di <xref:System.ServiceModel.BasicHttpBinding>. Se il servizio, pertanto, è stato creato utilizzando [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], è probabile che implementerà la protezione per assicurare autenticazione, riservatezza e integrità.In tal caso, i metadati forniti dal servizio indicheranno cosa è necessario per stabilire un canale di comunicazione protetto.Se i metadati del servizio non includono requisiti di sicurezza, non esiste alcuna possibilità di imporre uno schema di sicurezza, ad esempio Secure Sockets Layer \(SSL\) su HTTP, in un servizio.Se, tuttavia, il servizio richiede al client di fornire una credenziale, lo sviluppatore, il distributore o l'amministratore client deve fornire la credenziale effettiva che verrà utilizzata dal client per l'autenticazione al servizio.  
  
## Recupero di metadati  
 Quando si crea un client, eseguire innanzitutto il recupero di metadati per il servizio con il quale il client comunicherà.Questa operazione può essere eseguita in due modi.In primo luogo, se il servizio pubblica un endpoint di scambio di metadati \(MEX\) o rende disponibili i metadati su HTTP o HTTPS, è possibile scaricare i metadati utilizzando [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) e generare così sia file di codice per un client, sia un file di configurazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)] sull'utilizzo dello strumento, vedere [Accesso ai servizi tramite client WCF](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md). Se il servizio non pubblica un endpoint MEX e non rende disponibili i metadati su HTTP o HTTPS, è necessario contattare il creatore del servizio per ottenere la documentazione che descrive i requisiti di sicurezza e i metadati.  
  
> [!IMPORTANT]
>  È preferibile che i metadati provengano da un'origine attendibile e che non siano stati alterati.I metadati recuperati utilizzando il protocollo HTTP vengono inviati come testo non crittografato e possono essere alterati.Se il servizio utilizza le proprietà <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> e <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>, utilizzare l'URL fornito dal creatore del servizio per scaricare i dati tramite il protocollo HTTPS.  
  
## Convalida della protezione  
 Le origini di metadati possono essere suddivise in due ampie categorie: origini attendibili e non attendibili.Se l'origine è attendibile e se vengono scaricati il codice client e altri metadati dall'endpoint MEX protetto di quell'origine, è possibile generare il client, fornire le credenziali corrette ed eseguirlo senza altri dubbi.  
  
 Se, tuttavia, si sceglie di scaricare un client e i metadati da un'origine sconosciuta, assicurarsi di convalidare le misure di sicurezza utilizzate dal codice.Non è sufficiente, ad esempio, creare semplicemente un client che invii le informazioni personali o finanziarie a un servizio a meno che quest'ultimo non richieda, come minimo, riservatezza e integrità.È necessario che il proprietario del servizio sia attendibile per l'ambito desiderato di diffusione delle informazioni, dato che queste saranno visibili al proprietario stesso.  
  
 Di norma, pertanto, quando si utilizzano codice e metadati provenienti da un'origine non attendibile, controllare il codice e i metadati per verificare che soddisfino il livello di sicurezza richiesto.  
  
## Impostazione di una credenziale client  
 L'impostazione di una credenziale client in un client è costituita da due passaggi:  
  
1.  Determinare il *tipo di credenziale client* richiesto dal servizio.Questa operazione viene eseguita tramite uno dei due metodi seguenti.In primo luogo, se si dispone della documentazione proveniente dal creatore del servizio, è necessario specificare il tipo di credenziale client \(se presente\) richiesto dal servizio.Quindi, se si dispone solo di un file di configurazione generato dallo strumento Svcutil.exe, è possibile esaminare le singole associazioni per determinare il tipo di credenziale richiesto.  
  
2.  Specificare una credenziale client effettiva.La credenziale client effettiva viene chiamata *valore della credenziale client* per distinguerla dal tipo.Se, ad esempio, il tipo di credenziale client specifica un certificato, è necessario fornire un certificato X.509 emesso da un'autorità di certificazione che il servizio considera attendibile.  
  
### Determinazione del tipo di credenziale client  
 Se si dispone del file di configurazione generato dallo strumento Svcutil.exe, esaminare la sezione [\<associazioni\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) per determinare il tipo di credenziale client richiesto.All'interno della sezione esistono elementi di associazione che specificano i requisiti di sicurezza.Esaminare, in particolare, l'elemento \<security\> di ogni associazione.L'elemento include l'attributo `mode` che è possibile impostare su uno dei tre valori seguenti, `Message`, `Transport` o `TransportWithMessageCredential`.Il valore dell'attributo determina la modalità che a sua volta determina quale degli elementi figlio è significativo.  
  
 L'elemento `<security>``<transport>` è in grado di contenere un elemento `<message>`  o  o entrambi.L'elemento significativo è quello che corrisponde alla modalità di sicurezza.Nel codice seguente, ad esempio, viene specificato che la modalità di sicurezza è `"Message"` e il tipo di credenziale client per l'elemento `<message>` è `"Certificate"`.In questo caso, l'elemento `<transport>` può essere ignorato.L'elemento `<message>`, tuttavia, specifica che è necessario che venga fornito un certificato X.509.  
  
```  
<wsHttpBinding>  
    <binding name="WSHttpBinding_ICalculator">  
       <security mode="Message">  
           <transport clientCredentialType="Windows"   
                      realm="" />  
           <message clientCredentialType="Certificate"   
                    negotiateServiceCredential="true"  
                    algorithmSuite="Default"   
                    establishSecurityContext="true" />  
       </security>  
    </binding>  
</wsHttpBinding>  
```  
  
 Si noti che se l'attributo `clientCredentialType` è impostato su `"Windows"`, come illustrato nell'esempio seguente, non è necessario fornire un valore della credenziale effettivo.Questo avviene perché la protezione integrata di Windows fornisce la credenziale effettiva \(un token Kerberos\) della persona che sta eseguendo il client.  
  
```  
<security mode="Message">  
    <transport clientCredentialType="Windows "   
        realm="" />  
</security>  
```  
  
### Impostazione del valore della credenziale client  
 Se è stato stabilito che il client debba fornire una credenziale, utilizzare il metodo appropriato per configurare il client.Per impostare un certificato client, ad esempio, utilizzare il metodo <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>.  
  
 Un tipo comune di credenziale è il certificato X.509.È possibile fornire la credenziale in due modi:  
  
-   Tramite la programmazione della credenziale nel codice client \(utilizzando il metodo `SetCertificate`\).  
  
 Tramite l'aggiunta della sezione [\<comportamenti\>](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) del file di configurazione per il client e l'utilizzo dell'elemento `clientCredentials` come descritto di seguito.  
  
#### Impostazione del valore \<clientCredentials\> nel codice  
 Per impostare un valore [\<credenzialiClient\>](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) nel codice, è necessario accedere alla proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> della classe <xref:System.ServiceModel.ClientBase%601>.La proprietà restituisce un oggetto <xref:System.ServiceModel.Description.ClientCredentials> che consente l'accesso a vari tipi di credenziali, come illustrato nella tabella seguente.  
  
|Proprietà ClientCredential|Descrizione|Note|  
|--------------------------------|-----------------|----------|  
|<xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>|Restituisce <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>.|Rappresenta un certificato X.509 fornito dal client per l'autenticazione al servizio.|  
|<xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>|Restituisce <xref:System.ServiceModel.Security.HttpDigestClientCredential>.|Rappresenta una credenziale digest HTTP.La credenziale è un hash del nome utente e della password.|  
|<xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>|Restituisce <xref:System.ServiceModel.Security.IssuedTokenClientCredential>.|Rappresenta un token di sicurezza personalizzato emesso da un servizio token di sicurezza, utilizzato generalmente negli scenari di federazioni.|  
|<xref:System.ServiceModel.Description.ClientCredentials.Peer%2A>|Restituisce <xref:System.ServiceModel.Security.PeerCredential>.|Rappresenta una credenziale peer per la partecipazione in una rete di peer in un dominio Windows.|  
|<xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>|Restituisce <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>.|Rappresenta un certificato X.509 fornito dal servizio in una negoziazione fuori banda.|  
|<xref:System.ServiceModel.Description.ClientCredentials.UserName%2A>|Restituisce <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>.|Rappresenta una coppia nome utente e password.|  
|<xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>|Restituisce <xref:System.ServiceModel.Security.WindowsClientCredential>.|Rappresenta una credenziale client di Windows \(credenziale Kerberos\).Le proprietà della classe sono in sola lettura.|  
  
#### Impostazione del valore \<clientCredentials\> nella configurazione  
 I valori della credenziale vengono specificati tramite un comportamento dell'endpoint come elementi figlio dell'elemento [\<credenzialiClient\>](../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md).L'elemento utilizzato dipende dal tipo di credenziale client.Nell'esempio seguente viene illustrata la configurazione utilizzata per impostare un certificato X.509 tramite \<[\<certificatoClient\>](../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-clientcredentials-element.md).  
  
```  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myEndpointBehavior">  
          <clientCredentials>  
            <clientCertificate findvalue="myMachineName"   
            storeLocation="Current" X509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>              
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 Per impostare la credenziale client nella configurazione, aggiungere l'elemento [\<comportamentiEndpoint\>](../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) al file di configurazione.L'elemento di comportamento aggiunto deve inoltre essere collegato all'endpoint del servizio utilizzando l'attributo `behaviorConfiguration` dell'elemento [\<endpoint\>](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) come illustrato nell'esempio seguente.Il valore dell'attributo `behaviorConfiguration` deve corrispondere al valore dell'attributo `name` del comportamento.  
  
 `<configuration>`  
  
 `<system.serviceModel>`  
  
 `<client>`  
  
 `<endpoint address="http://localhost/servicemodelsamples/service.svc"`  
  
 `binding="wsHttpBinding"`  
  
 `bindingConfiguration="Binding1"`  
  
 `behaviorConfiguration="myEndpointBehavior"`  
  
 `contract="Microsoft.ServiceModel.Samples.ICalculator" />`  
  
 `</client>`  
  
 `</system.serviceModel>`  
  
 `</configuration>`  
  
> [!NOTE]
>  È impossibile impostare alcuni dei valori della credenziale client utilizzando i file di configurazione dell'applicazione, ad esempio nome utente e password o i valori utente e password di Windows.È possibile specificare tali valori della credenziale solo nel codice.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] sull'impostazione della credenziale client, vedere [Procedura: specificare valori di credenziali client](../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
> [!NOTE]
>  `ClientCredentialType` viene ignorato quando `SecurityMode` è impostato su `"TransportWithMessageCredential",` come illustrato nell'esempio di configurazione seguente.  
  
```  
<wsHttpBinding>  
    <binding name="PingBinding">  
        <security mode="TransportWithMessageCredential"  >  
           <message  clientCredentialType="UserName"   
               establishSecurityContext="false"    
               negotiateServiceCredential="false" />  
           <transport clientCredentialType="Certificate"  />  
         </security>  
    </binding>  
</wsHttpBinding>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>   
 <xref:System.ServiceModel.ClientBase%601>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>   
 [\<associazioni\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)   
 [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)   
 [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md)   
 [Accesso ai servizi tramite client WCF](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)   
 [Procedura: specificare valori di credenziali client](../../../docs/framework/wcf/how-to-specify-client-credential-values.md)   
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Procedura: specificare il tipo di credenziali client](../../../docs/framework/wcf/how-to-specify-the-client-credential-type.md)