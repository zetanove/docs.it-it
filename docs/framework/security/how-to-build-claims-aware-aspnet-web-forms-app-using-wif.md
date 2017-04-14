---
title: "Procedura: Compilare un&#39;applicazione Web Form ASP.NET in grado di riconoscere attestazioni con WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efb264dd-f47b-49a9-85ee-9f45d4425765
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# Procedura: Compilare un&#39;applicazione Web Form ASP.NET in grado di riconoscere attestazioni con WIF
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 In questa procedura vengono fornite le procedure dettagliate per creare l'applicazione Web Form su consapevole ASP.NET semplice.  Fornisce inoltre le istruzioni su come verificare l'applicazione Web Form su consapevole ASP.NET semplice per la corretta implementazione di autenticazione organizzata in modo federativo.  In questa procedura non ha dettagliato le istruzioni per creare un servizio token di sicurezza \(STS\) e si presuppone sia già configurato un servizio token di sicurezza.  
  
## Contenuto  
  
-   Obiettivi  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per autenticazione Basata su richiesta  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Obiettivi  
  
-   Configurare l'applicazione Web Form ASP.NET per autenticazione basata su richiesta  
  
-   Verificare la corrispondenza applicazione Web Form la ricezione di ASP.NET  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare l'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per autenticazione organizzata in modo federativo  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
 In questo passaggio, verrà creata una nuova applicazione Web Form ASP.NET.  
  
#### Per creare una semplice applicazione ASP.NET  
  
1.  Avviare Visual Studio e clic **File**, **Nuova**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
## Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per autenticazione Basata su richiesta  
 In questo passaggio si aggiungeranno voci di configurazione *nel file di configurazione Web.config* dell'applicazione Web Form ASP.NET rendono riconoscere attestazioni.  
  
#### Per configurare un'applicazione ASP.NET per autenticazione basata su richiesta  
  
1.  Aggiungere le voci seguenti della sezione di configurazione *nel file di configurazione Web.config* immediatamente dopo **\<configuration\>** l'elemento di apertura:  
  
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
  
4.  Aggiungere un elemento **\<system.webServer\>** che definisce i moduli per l'autenticazione organizzata in modo federativo.  Si noti che l'attributo *di PublicKeyToken* deve essere uguale all'attributo *di PublicKeyToken* per le voci **\<configSections\>** abbia inserito in precedenza:  
  
    ```  
    <system.webServer>  
      <modules>  
        <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
        <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      </modules>  
    </system.webServer>  
    ```  
  
5.  Aggiungere seguente le voci di configurazione correlate di identità Windows di base e verificare che l'url e il numero di porta dell'applicazione ASP.NET corrispondono ai valori nella voce **\<audienceUris\>**, nell'attributo **area autenticazione** di elemento **\<wsFederation\>** e nell'attributo **rispondi** di elemento **\<wsFederation\>**.  Assicurarsi inoltre che il valore **autorità** appropriata il servizio token di sicurezza \(STS\) URL.  
  
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
  
6.  Aggiungere il riferimento all'assembly [System.IdentityModel](assetId:///System.IdentityModel?qualifyHint=False&amp;autoUpgrade=True).  
  
7.  Compilare la soluzione per assicurarsi che non vi siano errori.  
  
## Passaggio 3 \- eseguire il test della soluzione  
 In questo passaggio verrà l'applicazione Web Form ASP.NET configurata per l'autenticazione basata su richiesta.  Per eseguire un test di base, si aggiungerà il codice che visualizza le richieste del token generato dal servizio token di sicurezza \(STS\).  
  
#### Per testare l'applicazione Web Form ASP.NET di autenticazione basata su richiesta  
  
1.  Aprire il file **Default.aspx** sotto il progetto **TestApp** e sostituire il markup esistente con il seguente:  
  
    ```  
    %@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head id="Head1" runat="server">  
        <title></title>  
    </head>  
    <body>  
        <h1><asp:label ID="signedIn" runat="server" /></h1>  
        <asp:label ID="claimType" runat="server" />  
        <asp:label ID="claimValue" runat="server" />  
        <asp:label ID="claimValueType" runat="server" />  
        <asp:label ID="claimSubjectName" runat="server" />  
        <asp:label ID="claimIssuer" runat="server" />  
    </body>  
    </html>  
    ```  
  
2.  Salvare **Default.aspx**quindi aprire il relativo code\-behind **Default.aspx.cs**denominato file.  
  
    > [!NOTE]
    >  **Default.aspx.cs** può essere nascosto in **Default.aspx** in Esplora soluzioni.  Se **Default.aspx.cs** non è visibile, espandere **Default.aspx** facendo clic sul triangolo accanto.  
  
3.  Sostituire il codice esistente nel metodo **Page\_Load** **Default.aspx.cs** con il codice seguente:  
  
    ```csharp  
    using System;  
    using System.IdentityModel;  
    using System.Security.Claims;  
    using System.Threading;  
    using System.Web.UI;  
  
    namespace TestApp  
    {  
        public partial class _Default : System.Web.UI.Page  
        {  
            protected void Page_Load(object sender, EventArgs e)  
            {  
                ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
                if (claimsPrincipal != null)  
                {  
                    signedIn.Text = "You are signed in.";  
  
                    foreach (Claim claim in claimsPrincipal.Claims)  
                    {  
                        claimType.Text = claim.Type;  
                        claimValue.Text = claim.Value;  
                        claimValueType.Text = claim.ValueType;  
                        claimSubjectName.Text = claim.Subject.Name;  
                        claimIssuer.Text = claim.Issuer;  
                    }  
                }  
                else  
                {  
                    signedIn.Text = "You are not signed in.";  
                }  
            }  
        }  
    }  
    ```  
  
4.  Salvare **Default.aspx.cs**e compilare la soluzione.  
  
5.  Eseguire la soluzione premendo il tasto **F5**.  
  
6.  Dovrebbe essere visualizzata la pagina che visualizza le richieste del token che è stato rimosso dal servizio token di sicurezza.