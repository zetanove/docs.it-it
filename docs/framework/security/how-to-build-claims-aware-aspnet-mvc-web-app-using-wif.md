---
title: "Procedura: Compilare un&#39;applicazione Web ASP.NET MVC in grado di riconoscere attestazioni con WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0efb76bc-9f7b-4afe-be1c-2a57c917010b
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Procedura: Compilare un&#39;applicazione Web ASP.NET MVC in grado di riconoscere attestazioni con WIF
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® MVC  
  
## Riepilogo  
 In questa procedura vengono fornite le procedure dettagliate per creare l'applicazione web su consapevole semplice MVC ASP.NET.  Fornisce inoltre le istruzioni come testare l'applicazione web su consapevole semplice MVC ASP.NET per la corretta implementazione di di autenticazione basata su richiesta.  In questa procedura non ha dettagliato le istruzioni per creare un servizio token di sicurezza \(STS\) e si presuppone sia già configurato un servizio token di sicurezza.  
  
## Contenuto  
  
-   Obiettivi  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione semplice MVC ASP.NET  
  
-   Passaggio 2 \- configurare l'applicazione MVC ASP.NET di autenticazione Basata su richiesta  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
-   Elementi correlati  
  
## Obiettivi  
  
-   Configurare l'applicazione web ASP.NET per autenticazione basata su richiesta  
  
-   Verificare la corrispondenza applicazione web della ricezione di MVC ASP.NET  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione semplice MVC ASP.NET  
  
-   Passaggio 2 \- configurare l'applicazione MVC ASP.NET di autenticazione Basata su richiesta  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Passaggio 1 \- creare un'applicazione semplice MVC ASP.NET  
 In questo passaggio, verrà creata una nuova applicazione MVC ASP.NET.  
  
#### Per creare un'applicazione semplice MVC ASP.NET  
  
1.  Avviare Visual Studio e clic **File**, **Nuova**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web ASP.NET MVC 3**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
4.  Nella finestra di dialogo **Nuovo progetto ASP.NET MVC 3**, selezionare **Applicazione Internet** dai modelli disponibili, assicurarsi **Motore di visualizzazione** è impostato su **Razor**quindi fare clic **OK**.  
  
5.  Quando il nuovo progetto viene aperto, fare clic con il pulsante destro del mouse sul progetto **TestApp** in **Esplora soluzioni** e selezionare l'opzione **Proprietà**.  
  
6.  Le proprietà del progetto pagina, fare clic su nella scheda **Web** a sinistra e verificare che l'opzione **Usa server Web IIS locale** è selezionata.  
  
## Passaggio 2 \- configurare l'applicazione MVC ASP.NET di autenticazione Basata su richiesta  
 In questo passaggio si aggiungeranno voci di configurazione *nel file di configurazione Web.config* dell'applicazione web MVC ASP.NET rendono riconoscere attestazioni.  
  
#### Per configurare un'applicazione ASP.NET MVC di autenticazione basata su richiesta  
  
1.  Aggiungere le seguenti definizioni di sezione di configurazione *nel file di configurazione Web.config*.  Questi definiscono sezioni di configurazione richiesti dal fondamento di identità Windows.  Aggiungere le definizioni immediatamente dopo **\<configuration\>** l'elemento di apertura:  
  
    ```xml  
    <configSections>  
        <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
        <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    </configSections>  
    ```  
  
2.  Aggiungere un elemento **\<location\>** che consente l'accesso ai metadati della federazione dell'applicazione:  
  
    ```xml  
    <location path="FederationMetadata">  
        <system.web>  
            <authorization>  
                <allow users="*" />  
            </authorization>  
        </system.web>  
    </location>  
    ```  
  
3.  Aggiungere le voci seguenti di configurazione negli elementi **\<system.web\>** per negare gli utenti, disabilitare l'autenticazione nativa e consentono a WIF per gestire l'autenticazione.  
  
    ```xml  
    <authorization>  
        <deny users="?" />  
    </authorization>  
    <authentication mode="None" />  
    ```  
  
4.  Aggiungere seguente le voci di configurazione correlate di identità Windows di base e verificare che l'url e il numero di porta dell'applicazione ASP.NET corrispondono ai valori nella voce **\<audienceUris\>**, nell'attributo **area autenticazione** di elemento **\<wsFederation\>** e nell'attributo **rispondi** di elemento **\<wsFederation\>**.  Assicurarsi inoltre che il valore **autorità** appropriata il servizio token di sicurezza \(STS\) URL.  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <audienceUris>  
                <add value="http://localhost:28503/" />  
            </audienceUris>  
            <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
                <trustedIssuers>  
                    <add thumbprint="1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ1234" name="YourSTSName" />  
                </trustedIssuers>   
            </issuerNameRegistry>  
            <certificateValidation certificateValidationMode="None" />  
        </identityConfiguration>  
    </system.identityModel>  
    <system.identityModel.services>  
        <federationConfiguration>  
            <cookieHandler requireSsl="false" />  
            <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:13922/wsFederationSTS/Issue" realm="http://localhost:28503/" reply="http://localhost:28503/" requireHttps="false" />  
        </federationConfiguration>  
    </system.identityModel.services>  
    ```  
  
5.  Aggiungere il riferimento all'assembly [System.IdentityModel](assetId:///System.IdentityModel?qualifyHint=False&amp;autoUpgrade=True).  
  
6.  Compilare la soluzione per assicurarsi che non vi siano errori.  
  
## Passaggio 3 \- eseguire il test della soluzione  
 In questo passaggio verrà l'applicazione web ASP.NET MVC configurata per l'autenticazione basata su richiesta.  Per eseguire il test di base verrà aggiunto un codice semplice che visualizza le richieste del token generato dal servizio token di sicurezza \(STS\).  
  
#### Per testare l'applicazione MVC ASP.NET di autenticazione basata su richiesta  
  
1.  In **Esplora soluzioni**, espandere la cartella **Controller** e aprire il file *HomeController.cs* nell'editor.  Aggiungere il seguente codice al metodo **Indice** :  
  
    ```csharp  
    public ActionResult Index()  
    {  
        ViewBag.ClaimsIdentity = Thread.CurrentPrincipal.Identity;  
  
        return View();  
    }  
  
    ```  
  
2.  In **Esplora soluzioni** espandere le cartelle **Pagina iniziale** quindi e **Visualizzazioni** e *il file di Index.cshtml* aperto nell'editor.  Eliminarne il contenuto e aggiungere il markup seguente:  
  
    ```html  
  
    @{  
        ViewBag.Title = "Home Page";  
    }  
  
    <h2>Welcome: @ViewBag.ClaimsIdentity.Name</h2>  
    <h3>Values from Identity</h3>  
    <table>  
        <tr>  
            <th>  
                IsAuthenticated   
            </th>  
            <td>  
                @ViewBag.ClaimsIdentity.IsAuthenticated   
            </td>  
        </tr>  
        <tr>  
            <th>  
                Name   
            </th>          
            <td>  
                @ViewBag.ClaimsIdentity.Name  
            </td>          
        </tr>  
    </table>  
    <h3>Claims from ClaimsIdentity</h3>  
    <table>  
        <tr>  
            <th>  
                Claim Type  
            </th>  
            <th>  
                Claim Value  
            </th>  
            <th>  
                Value Type  
            </th>  
            <th>  
                Subject Name  
            </th>          
            <th>  
                Issuer Name  
            </th>          
        </tr>  
            @foreach (System.Security.Claims.Claim claim in ViewBag.ClaimsIdentity.Claims ) {  
        <tr>  
            <td>  
                @claim.Type  
            </td>  
            <td>  
                @claim.Value  
            </td>  
            <td>  
                @claim.ValueType  
            </td>  
            <td>  
                @claim.Subject.Name  
            </td>  
            <td>  
                @claim.Issuer  
            </td>  
        </tr>  
    }  
    </table>  
  
    ```  
  
3.  Eseguire la soluzione premendo il tasto **F5**.  
  
4.  Dovrebbe essere visualizzata la pagina che visualizza le richieste del token che è stato rimosso dal servizio token di sicurezza.  
  
## Elementi correlati  
  
-   [Procedura: Compilare un'applicazione Web Form ASP.NET in grado di riconoscere attestazioni con WIF](../../../docs/framework/security/how-to-build-claims-aware-aspnet-web-forms-app-using-wif.md)