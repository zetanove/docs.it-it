---
title: "Procedura: Compilare un&#39;applicazione ASP.NET in grado di riconoscere attestazioni con l&#39;autenticazione basata su moduli | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98a3e029-1a9b-4e0c-b5d0-29d3f23f5b15
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Procedura: Compilare un&#39;applicazione ASP.NET in grado di riconoscere attestazioni con l&#39;autenticazione basata su moduli
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 In questa procedura vengono fornite le procedure dettagliate per creare un'applicazione Web Form su consapevole ASP.NET semplice che utilizza l'autenticazione basata su form.  Fornisce inoltre le istruzioni su come verificare l'applicazione per verificare che le richieste vengano visualizzate quando un utente in con l'autenticazione basata su form.  
  
## Contenuto  
  
-   Obiettivi  
  
-   Panoramica  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per i reclami con l'autenticazione basata su form  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Obiettivi  
  
-   Configurare un'applicazione Web Form ASP.NET per le richieste utilizzando l'autenticazione basata su form  
  
-   Verificare l'applicazione Web Form ASP.NET per verificare se funziona correttamente  
  
## Panoramica  
 In .NET 4,5, WIF e la relativa all'autorizzazione basata su richieste sono stati inclusi come parte integrante del Framework.  In precedenza, si desiderasse le richieste da un utente ASP.NET, è stato richiesto di installare WIF quindi eseguire il cast delle interfacce agli oggetti principali come `Thread.CurrentPrincipal` o `HttpContext.Current.User`.  Ora, le richieste vengono gestite automaticamente da questi oggetti principali.  
  
 L'autenticazione basata su form è tratto vantaggio dall'inclusione di WIF in .NET 4,5 perché tutti gli utenti autenticati automaticamente dai form sono richieste associate.  È possibile avviare utilizzando queste richieste immediatamente in un'applicazione ASP.NET che utilizza l'autenticazione basata su form, come in questa procedura vengono illustrate.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per i reclami con l'autenticazione basata su form  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
 In questo passaggio, verrà creata una nuova applicazione Web Form ASP.NET.  
  
#### Per creare una semplice applicazione ASP.NET  
  
1.  Avviare Visual Studio e clic **File**, **Nuova**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
## Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per i reclami con l'autenticazione basata su form  
 In questo passaggio verrà aggiunta una voce di configurazione al file *Web.config* e si modifica il file *Default.aspx* per visualizzare le informazioni delle richieste di un account.  
  
#### Per configurare un'applicazione ASP.NET di richieste utilizzando l'autenticazione basata su form  
  
1.  *Nel file Default.aspx*, sostituire il markup esistente con quello riportato di seguito:  
  
    ```  
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>  
  
    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">  
        <p>  
            This page displays the claims associated with a Forms authenticated user.          
        </p>  
        <h3>Your Claims</h3>  
        <p>  
            <asp:GridView ID="ClaimsGridView" runat="server" CellPadding="3">  
                <AlternatingRowStyle BackColor="White" />  
                <HeaderStyle BackColor="#7AC0DA" ForeColor="White" />  
            </asp:GridView>  
        </p>  
    </asp:Content>  
  
    ```  
  
     Questo passaggio aggiunge un controllo GridView alla *pagina Default.aspx* che verrà popolata con le richieste recuperate dall'autenticazione basata su form.  
  
2.  Salvare il file *Default.aspx*, quindi aprire il file code\-behind denominato *Default.aspx.cs*.  Sostituire il codice esistente con quello riportato di seguito:  
  
    ```csharp  
    using System;  
    using System.Web.UI;  
    using System.Security.Claims;  
  
    namespace TestApp  
    {  
        public partial class _Default : Page  
        {  
            protected void Page_Load(object sender, EventArgs e)  
            {  
                ClaimsPrincipal claimsPrincipal = Page.User as ClaimsPrincipal;  
  
                if (claimsPrincipal != null)  
                {  
                    this.ClaimsGridView.DataSource = claimsPrincipal.Claims;  
                    this.ClaimsGridView.DataBind();  
                }  
            }  
        }  
    }  
    ```  
  
     Il codice sopra visualizzare le richieste su un utente autenticato, inclusi gli utenti identificati dall'autenticazione basata su form.  
  
## Passaggio 3 \- eseguire il test della soluzione  
 In questo passaggio verrà l'applicazione Web Form ASP.NET e verificato che le richieste vengano visualizzate quando un utente in con l'autenticazione basata su form.  
  
#### Per testare l'applicazione Web Form ASP.NET per le richieste utilizzando l'autenticazione basata su form  
  
1.  Premere **F5** per compilare ed eseguire l'applicazione.  Dovrebbe essere visualizzata *Default.aspx,*con **Registra** e **Accedi** collegamento nella destra superiore della pagina.  Fare clic su **Registra**.  
  
2.  Nella pagina **Registra**, creare un account utente e scegliere **Registra**.  L'account verrà creato utilizzando l'autenticazione basata su form e vengono impostati automaticamente firmato in.  
  
3.  Dopo che è stato reindirizzato alla home page, verrà visualizzata una tabella nella direzione **Attestazioni** che include **Autorità emittente**, **OriginalIssuer**, **Tipo**, **Valore**e informazioni delle richieste **Tipovalore** sull'account.