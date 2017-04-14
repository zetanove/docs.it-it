---
title: "Procedura: autenticare con un nome utente e una password | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "autenticazione [WCF], nome utente e password"
ms.assetid: a5415be2-0ef3-464c-9f76-c255cb8165a4
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Procedura: autenticare con un nome utente e una password
In questo argomento viene illustrato come consentire a un servizio di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] di autenticare un client con un nome utente e una password del dominio Windows.Si presuppone che l'utente disponga di un servizio WCF funzionante e indipendente.Per un esempio di creazione di un servizio WCF indipendente di base, vedere [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md).In questo argomento si presuppone che il servizio sia configurato nel codice.Se si desidera visualizzare un esempio di configurazione di un servizio simile tramite un file di configurazione, vedere [Sicurezza dei messaggi tramite nome utente](../../../../docs/framework/wcf/samples/message-security-user-name.md)  
  
 Per configurare l'autenticazione da parte di un servizio dei relativi client mediante il nome utente e la password del dominio Windows, utilizzare l'oggetto <xref:System.ServiceModel.WSHttpBinding> e impostare la relativa proprietà `Security.Mode` su `Message`.Inoltre, è necessario specificare un certificato X509 che verrà utilizzato per crittografare il nome utente e la password quando vengono inviati dal client al servizio.  
  
 Nel client, è necessario richiedere all'utente il nome utente e la password e specificare le credenziali dell'utente nel proxy client WCF.  
  
### Per configurare un servizio WCF per l'autenticazione tramite nome utente e password del dominio Windows.  
  
1.  Creare un'istanza dell'oggetto <xref:System.ServiceModel.WSHttpBinding>, impostare la modalità di sicurezza dell'associazione su `SecurityMode.Message`, impostare `ClientCredentialType` dell'associazione su `MessageCredentialType.UserName` e aggiungere un endpoint del servizio utilizzando l'associazione configurata all'host del servizio come illustrato nel codice seguente:  
  
    ```  
    // ...  
    WSHttpBinding userNameBinding = new WSHttpBinding();  
    userNameBinding.Security.Mode = SecurityMode.Message;  
    userNameBinding.Security.Message.ClientCredentialType = MessageCredentialType.UserName;  
    svcHost.AddServiceEndpoint(typeof(IService1), userNameBinding, "");  
    // ...  
    ```  
  
2.  Specificare il certificato del server utilizzato per crittografare le informazioni relative al nome utente e alla password inviate tramite la rete.Questo codice deve seguire immediatamente il codice precedente.Nell'esempio seguente viene utilizzato il certificato creato dal file setup.bat dell'esempio [Sicurezza dei messaggi tramite nome utente](../../../../docs/framework/wcf/samples/message-security-user-name.md):  
  
    ```  
    // ...  
    svcHost.Credentials.ServiceCertificate.SetCertificate(StoreLocation.LocalMachine, StoreName.My, X509FindType.FindBySubjectName, "localhost");  
    // ...  
    ```  
  
     È possibile utilizzare il proprio certificato; è sufficiente modificare il codice per fare riferimento al certificato.Per ulteriori informazioni sulla creazione e sull'utilizzo di certificati, vedere [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).Assicurarsi che il certificato si trovi nell'archivio TrustedPeople per il computer locale.Questa operazione può essere effettuata eseguendo mmc.exe e selezionando le voci di menu **File**, **Aggiungi\/Rimuovi snap\-in**.Nella finestra di dialogo **Aggiungi o rimuovi snap\-in** selezionare **Snap\-in certificati** e fare clic su **Aggiungi**.Nella finestra di dialogo Snap\-in certificati selezionare **Account del computer**.Per impostazione predefinita, il certificato generato nell'esempio di sicurezza dei messaggi tramite nome utente sarà posizionato nella cartella Personale\/Certificati.Verrà elencato come "localhost" nella colonna Rilasciato a della finestra MMC.Trascinare il certificato nella cartella **Persone attendibili**.Questa operazione consentirà a WCF di trattare il certificato come attendibile quando si effettua l'autenticazione.  
  
### Per chiamare il servizio passando nome utente e password  
  
1.  L'applicazione client deve richiedere all'utente il nome utente e la password.Tramite il codice seguente vengono chiesti all'utente il nome utente e la password.  
  
    > [!WARNING]
    >  Questo codice non deve essere utilizzato in produzione poiché la password viene visualizzata durante l'immissione.  
  
    ```  
    public static void GetPassword(out string username, out string password)  
            {  
                Console.WriteLine("Provide a valid machine or domain account. [domain\\user]");  
                Console.WriteLine("   Enter username:");  
                username = Console.ReadLine();  
                Console.WriteLine("   Enter password:");  
                password = Console.ReadLine();             
                return;  
            }  
  
    ```  
  
2.  Creare un'istanza del proxy client specificando le credenziali del client come illustrato nel codice seguente:  
  
    ```  
    string username;  
    string password;  
  
    // Instantiate the proxy  
    Service1Client proxy = new Service1Client();  
  
    // Prompt the user for username & password  
    GetPassword(out username, out password);  
  
    // Set the user’s credentials on the proxy  
    proxy.ClientCredentials.UserName.UserName = username;  
    proxy.ClientCredentials.UserName.Password = password;  
  
    // Treat the test certificate as trusted  
    proxy.ClientCredentials.ServiceCertificate.Authentication.CertificateValidationMode = System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust;  
    // Call the service operation using the proxy  
    ```  
  
## Vedere anche  
 <xref:System.ServiceModel.WsHttpBinding>   
 <xref:System.ServiceModel.WSHttpSecurity>   
 <xref:System.ServiceModel.SecurityMode>   
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.UserName%2A>   
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.Password%2A>   
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>   
 <xref:System.ServiceModel.WSHttpSecurity.Mode%2A>   
 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A>   
 [Protezione del trasporto con l'autenticazione di base](../../../../docs/framework/wcf/feature-details/transport-security-with-basic-authentication.md)   
 [Protezione delle applicazioni distribuite](../../../../docs/framework/wcf/feature-details/distributed-application-security.md)   
 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)