---
title: "Provider di appartenenza e di ruoli | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0d11a31c-e75f-4fcf-9cf4-b7f26e056bcd
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Provider di appartenenza e di ruoli
Nell'esempio del provider di appartenenza e di ruoli viene illustrato in che modo un servizio può utilizzare i provider di appartenenza e di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] per autenticare e autorizzare i client.  
  
 In questo esempio, il client è un'applicazione console \(exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 In questo esempio viene illustrato come eseguire le seguenti operazioni:  
  
-   Un client può eseguire l'autenticazione utilizzando una combinazione nome utente\-password.  
  
-   Il server può convalidare le credenziali client in base al provider di appartenenza [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
-   Il server può essere autenticato tramite il certificato X.509 del server.  
  
-   Il server può eseguire il mapping del client autenticato a un ruolo utilizzando il provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
-   Il server può utilizzare `PrincipalPermissionAttribute` per controllare l'accesso a determinati metodi esposti dal servizio.  
  
 I provider di appartenenza e di ruoli sono configurati per utilizzare un archivio supportato da SQL Server.Una stringa di connessione e varie opzioni sono specificate nel file di configurazione del servizio.Al provider di appartenenza viene assegnato il nome `SqlMembershipProvider` mentre al provider di ruoli viene assegnato il nome `SqlRoleProvider`.  
  
```  
<!-- Set the connection string for SQL Server -->  
<connectionStrings>  
  <add name="SqlConn"   
       connectionString="Data Source=localhost;Integrated Security=SSPI;Initial Catalog=aspnetdb;" />  
</connectionStrings>  
  
<system.web>  
  <!-- Configure the Sql Membership Provider -->  
  <membership defaultProvider="SqlMembershipProvider" userIsOnlineTimeWindow="15">  
    <providers>  
      <clear />  
      <add   
        name="SqlMembershipProvider"   
        type="System.Web.Security.SqlMembershipProvider"   
        connectionStringName="SqlConn"  
        applicationName="MembershipAndRoleProviderSample"  
        enablePasswordRetrieval="false"  
        enablePasswordReset="false"  
        requiresQuestionAndAnswer="false"  
        requiresUniqueEmail="true"  
        passwordFormat="Hashed" />  
    </providers>  
  </membership>  
  
  <!-- Configure the Sql Role Provider -->  
  <roleManager enabled ="true"   
               defaultProvider ="SqlRoleProvider" >  
    <providers>  
      <add name ="SqlRoleProvider"   
           type="System.Web.Security.SqlRoleProvider"   
           connectionStringName="SqlConn"   
           applicationName="MembershipAndRoleProviderSample"/>  
    </providers>  
  </roleManager>  
</system.web>  
```  
  
 Il servizio espone un solo endpoint per la comunicazione con il servizio, che viene definito mediante il file di configurazione Web.config.L'endpoint è costituito da un indirizzo, un'associazione e un contratto.L'associazione viene configurata con una classe standard `wsHttpBinding`, per la quale è impostata l'autenticazione Windows come predefinita.In questo esempio viene impostata la classe `wsHttpBinding` standard per utilizzare l'autenticazione del nome utente.Il comportamento specifica che il certificato server deve essere utilizzato per autenticare il servizio.Il certificato server deve contenere per `SubjectName` lo stesso valore dell'attributo `findValue` nell'elemento di configurazione [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md).Il comportamento specifica inoltre che l'autenticazione della coppia nome utente\-password deve essere eseguita dal provider di appartenenze [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e il mapping del ruolo deve essere eseguito dal provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] specificando i nomi definiti per i due provider.  
  
```  
<system.serviceModel>  
  
  <protocolMapping>  
    <add scheme="http" binding="wsHttpBinding" />  
  </protocolMapping>  
  
  <bindings>  
    <wsHttpBinding>  
      <!-- Set up a binding that uses Username as the client credential type -->  
      <binding>  
        <security mode ="Message">  
          <message clientCredentialType ="UserName"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
  
  <behaviors>  
    <serviceBehaviors>  
      <behavior>  
        <!-- Configure role based authorization to use the Role Provider -->  
        <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                              roleProviderName ="SqlRoleProvider" />  
        <serviceCredentials>  
          <!-- Configure user name authentication to use the Membership Provider -->  
          <userNameAuthentication userNamePasswordValidationMode ="MembershipProvider"   
                                  membershipProviderName ="SqlMembershipProvider"/>  
          <!-- Configure the service certificate -->  
          <serviceCertificate storeLocation ="LocalMachine"   
                              storeName ="My"   
                              x509FindType ="FindBySubjectName"  
                              findValue ="localhost" />  
        </serviceCredentials>  
        <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
        <serviceDebug includeExceptionDetailInFaults="false" />  
        <serviceMetadata httpGetEnabled="true"/>  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
 Quando si esegue l'esempio, il client chiama le varie operazioni del servizio con tre account utente diversi: Alice, Bob e Charlie.Le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Tutte le 4 chiamate eseguite con l'account utente "Alice" hanno esito positivo.L'utente "Bob" ottiene un errore di accesso negato nel tentativo di chiamare il metodo Divide.L'utente "Charlie" ottiene un errore di accesso negato nel tentativo di chiamare il metodo Multiply.Premere INVIO nella finestra del client per arrestare il client.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
2.  Verificare che sia stato configurato il [database dei servizi per le applicazioni ASP.NET](http://go.microsoft.com/fwlink/?LinkId=94997).  
  
    > [!NOTE]
    >  Se si sta eseguendo SQL Server Express Edition, il nome del server è .\\SQLEXPRESS.Questo server deve essere utilizzato quando si configura il database dei servizi per le applicazioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e nella stringa di connessione di Web.config.  
  
    > [!NOTE]
    >  L'account del processo di lavoro [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] deve disporre delle autorizzazioni sul database creato in questo passaggio.Utilizzare l'utilità sqlcmd o SQL Server Management Studio per questo scopo.  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni indicate di seguito.  
  
### Per eseguire l'esempio nello stesso computer  
  
1.  Verificare che il percorso includa la cartella in cui si trova Makecert.exe.  
  
2.  Aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.In questo modo vengono installati i certificati dei servizi necessari per l'esecuzione dell'esempio.  
  
3.  Avviare Client.exe da \\client\\bin.L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
4.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio.Creare un'applicazione virtuale denominata servicemodelsamples per questa directory utilizzando lo strumento di gestione di Internet Information Services \(IIS\).  
  
2.  Copiare i file del programma del servizio da \\inetpub\\wwwroot\\servicemodelsamples nella directory virtuale sul computer del servizio.Assicurarsi di copiare i file nella sottodirectory \\bine i file Setup.bat, GetComputerName.vbs e Cleanup.bat nel computer del servizio.  
  
3.  Creare una directory sul client del servizio per i file binari del client.  
  
4.  Copiare i file di programma del client nella directory del client sul computer relativoe i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel computer del client.  
  
5.  Sul server aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire `setup.bat service`.Quando si esegue `setup.bat` con l'argomento `service` viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service.cer.  
  
6.  Modificare Web.config per riflettere il nuovo nome del certificato \(nell'attributo `findValue` in [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)\) che corrisponde al nome di dominio completo del computer.  
  
7.  Copiare il file Service.cer dalla directory del servizio nella directory del client sul computer relativo.  
  
8.  Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.  
  
9. Sul client aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire ImportServiceCert.bat.In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
10. Sul computer client avviare Client.exe da un prompt dei comandi.Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi dopo che l'esempio è stato completato.  
  
> [!NOTE]
>  Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.Se sono stati eseguiti esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che utilizzano certificati tra più computer, verificare di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.Per eseguire questa operazione, utilizzare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
## File batch di installazione  
 Il file batch Setup.bat incluso in questo esempio consente di configurare il server con i certificati attinenti per eseguire un'applicazione indipendente che richiede la sicurezza server basata su certificato.Questo file batch deve essere modificato per funzionare tra computer diversi o nel caso in cui non sia ospitato.  
  
 Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.  
  
-   Creazione del certificato server.  
  
     Le righe seguenti del file batch Setup.bat creano il certificato server da utilizzare.La variabile %SERVER\_NAME% specifica il nome del server.Modificare questa variabile per specificare il nome del server.Il valore predefinito di questo file batch è localhost.  
  
     Il certificato viene memorizzato nell'archivio personale nel percorso di archivio LocalMachine.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
-   Installazione del certificato server nell'archivio certificati attendibili del client.  
  
     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client.Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.Se è già disponibile un certificato impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
## Vedere anche