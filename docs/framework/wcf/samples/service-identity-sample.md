---
title: "Esempio identit&#224; del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79fa8c1c-85bb-4b67-bc67-bfaf721303f8
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Esempio identit&#224; del servizio
Questo esempio di identità del servizio illustra come impostare l'identità di un servizio.In fase di progettazione, un client può recuperare l'identità utilizzando i metadati del servizio e quindi al runtime il client può autenticare l'identità del servizio.Il concetto di identità del servizio serve per consentire a un client di autenticare un servizio prima di chiamare qualsiasi operazione, proteggendo in questo modo il client da chiamate non autenticate.Su una connessione sicura il servizio autentica anche le credenziali di un client prima di consentirgli l'accesso, ma questo non è il punto centrale dell'esempio.Vedere gli esempi in [Client](../../../../docs/framework/wcf/samples/client.md) che riguardano l'autenticazione del server.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 In questo esempio vengono illustrate le funzionalità seguenti:  
  
-   Come impostare tipi diversi di identità su endpoint diversi per un servizio.Ogni tipo di identità ha funzionalità diverse.Il tipo di identità da utilizzare dipende dal tipo di credenziali di sicurezza utilizzato sull'associazione dell'endpoint.  
  
-   L'identità può essere impostata in modo dichiarativo a livello di configurazione o in modo imperativo a livello di codice.In genere, sia per il client che per il servizio, per impostare l'identità, è necessario utilizzare la configurazione.  
  
-   Come impostare un'identità personalizzata in un clientUn'identità personalizzata è in genere una personalizzazione di un tipo esistente di identità che consente al client di esaminare le altre informazioni della richiesta fornite nelle credenziali del servizio per prendere decisioni di autorizzazione prima di chiamare il servizio.  
  
    > [!NOTE]
    >  Questo esempio controlla l'identità di un certificato specifico chiamato identity.com e la chiave RSA contenuta al suo interno.Quando si utilizzano i tipi di identità del certificato e di RSA nella configurazione del client, un modo semplice per ottenere questi valori è di controllare il WSDL del servizio dove questi valori vengono serializzati.  
  
 Nel codice di esempio seguente viene mostrato come configurare l'identità di un endpoint del servizio con il DNS di un certificato utilizzando un'associazione WSHttpBinding.  
  
```  
//Create a service endpoint and set its identity to the certificate's DNS                 
WSHttpBinding wsAnonbinding = new WSHttpBinding (SecurityMode.Message);  
// Client are Anonymous to the service  
wsAnonbinding.Security.Message.ClientCredentialType = MessageCredentialType.None;  
WServiceEndpoint ep = serviceHost.AddServiceEndpoint(typeof(ICalculator),wsAnonbinding, String.Empty);  
EndpointAddress epa = new EndpointAddress(dnsrelativeAddress,EndpointIdentity.CreateDnsIdentity("identity.com"));  
ep.Address = epa;  
  
```  
  
 L'identità può anche essere specificata in fase di configurazione nel file App.config.Nell'esempio seguente viene mostrato come impostare l'identità di UPN \(User Principal Name\) per un endpoint del servizio.  
  
```  
<endpoint address="upnidentity"  
        behaviorConfiguration=""  
        binding="wsHttpBinding"  
        bindingConfiguration="WSHttpBinding_Windows"  
        name="WSHttpBinding_ICalculator_Windows"  
        contract="Microsoft.ServiceModel.Samples.ICalculator">  
  <!-- Set the UPN identity for this endpoint -->  
  <identity>  
      <userPrincipalName value="host\myservice.com" />  
  </identity >  
</endpoint>  
  
```  
  
 Un'identità personalizzata può essere impostata sul client derivando dalle classi <xref:System.ServiceModel.EndpointIdentity> e <xref:System.ServiceModel.Security.IdentityVerifier>.Concettualmente la classe <xref:System.ServiceModel.Security.IdentityVerifier> può essere considerata l'equivalente client della classe `AuthorizationManager` del servizio.Nell'esempio di codice seguente viene mostrata un'implementazione di `OrgEndpointIdentity` che archivia il nome di un'organizzazione affinché corrisponda al nome dell'oggetto del certificato del server.Il controllo dell'autorizzazione per il nome dell'organizzazione si verifica nel metodo `CheckAccess` sulla classe `CustomIdentityVerifier`.  
  
```  
  
// This custom EndpointIdentity stores an organization name   
public class OrgEndpointIdentity : EndpointIdentity  
{  
    private string orgClaim;  
    public OrgEndpointIdentity(string orgName)  
    {  
        orgClaim = orgName;  
    }  
    public string OrganizationClaim  
    {  
        get { return orgClaim; }  
        set { orgClaim = value; }  
    }  
}  
  
//This custom IdentityVerifier uses the supplied OrgEndpointIdentity to  
//check that X.509 certificate's distinguished name claim contains  
//the organization name e.g. the string value "O=Contoso"   
class CustomIdentityVerifier : IdentityVerifier  
{  
    public override bool CheckAccess(EndpointIdentity identity, AuthorizationContext authContext)  
    {  
        bool returnvalue = false;  
        foreach (ClaimSet claimset in authContext.ClaimSets)  
        {  
            foreach (Claim claim in claimset)  
            {  
                if (claim.ClaimType == "http://schemas.microsoft.com/ws/2005/05/identity/claims/x500distinguishedname")  
                {  
                    X500DistinguishedName name = (X500DistinguishedName)claim.Resource;  
                    if (name.Name.Contains(((OrgEndpointIdentity)identity).OrganizationClaim))  
                    {  
                        Console.WriteLine("Claim Type: {0}",claim.ClaimType);  
                        Console.WriteLine("Right: {0}", claim.Right);  
                        Console.WriteLine("Resource: {0}",claim.Resource);  
                        Console.WriteLine();  
                        returnvalue = true;  
                    }  
                }  
            }  
        }  
        return returnvalue;  
    }  
}  
```  
  
 Questo esempio utilizza un certificato chiamato identity.com che è situato nella cartella Identity della soluzione specifica del linguaggio.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### Per eseguire l'esempio nello stesso computer  
  
1.  In [!INCLUDE[wxp](../../../../includes/wxp-md.md)] o [!INCLUDE[wv](../../../../includes/wv-md.md)] importare il file del certificato Identity.pfx nella cartella Identity della soluzione nell'archivio dei certificati LocalMachine\/My \(personale\) utilizzando lo strumento snap\-in MMC.Questo file è protetto da password.Durante l'importazione viene richiesta una password.Digitare `xyz` nella casella della password.Per ulteriori informazioni, vedere l'argomento [Procedura: visualizzare certificati con lo snap\-in MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).Completata questa operazione, eseguire Setup.bat in un prompt dei comandi di Visual Studio con privilegi di amministratore che copia questo certificato nell'archivio CurrentUser\/TrustedPeople per l'utilizzo sul client.  
  
2.  In [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] eseguire Setup.bat dalla cartella di installazione dell'esempio in un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore.In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].La variabile di ambiente PATH impostata nel prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] punta alla directory che contiene file eseguibili richiesti dallo script Setup.bat.Assicurarsi di rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio.Gli altri esempi relativi alla sicurezza utilizzano gli stessi certificati.  
  
3.  Avviare Service.exe dalla directory \\service\\bin.Assicurarsi che il servizio indichi che è pronto e visualizzi un prompt per Premere \<Invio\> per terminare il servizio.  
  
4.  Avviare Client.exe dalla directory \\client\\bin o premendo F5 in Visual Studio per compilare ed eseguire l'esempio.L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
5.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire l'esempio tra più computer  
  
1.  Prima di compilare la parte client dell'esempio, assicurarsi di aver modificato il valore dell'indirizzo endpoint del servizio nel file Client.cs nel metodo `CallServiceCustomClientIdentity`.Quindi compilare l'esempio.  
  
2.  Creare una directory sul computer del servizio.  
  
3.  Copiare i file di programma del servizio da \\service\\bin nella directory del computer del servizio.Copiare i file Setup.bat e Cleanup.bat nel computer del servizio.  
  
4.  Creare una directory sul client del servizio per i file binari del client.  
  
5.  Copiare i file di programma del client nella directory del client sul computer relativoe i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel computer del client.  
  
6.  Sul server aprire un prompt dei comandi di Visual Studio con privilegi di amministratore, quindi digitare `setup.bat service`.Quando si esegue `setup.bat` con l'argomento `service` viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service.cer.  
  
7.  Copiare il file Service.cer dalla directory del servizio nella directory del client sul computer relativo.  
  
8.  Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.Sono presenti più istanze che devono essere modificate.  
  
9. Sul client aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire ImportServiceCert.bat.In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
10. Sul computer del servizio eseguire Service.exe dal prompt dei comandi.  
  
11. Sul computer client avviare Client.exe da un prompt dei comandi.Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
    > [!NOTE]
    >  Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.Se sono stati eseguiti esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che utilizzano certificati tra più computer, verificare di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.Per eseguire questa operazione, utilizzare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
## Vedere anche