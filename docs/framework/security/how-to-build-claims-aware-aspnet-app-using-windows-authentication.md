---
title: "Procedura: Compilare un&#39;applicazione ASP.NET in grado di riconoscere attestazioni con l&#39;autenticazione di Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11c53d9d-d34a-44b4-8b5e-22e3eaeaee93
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# Procedura: Compilare un&#39;applicazione ASP.NET in grado di riconoscere attestazioni con l&#39;autenticazione di Windows
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 Ciò presenti In vengono fornite le procedure dettagliate per creare un'applicazione Web Form su consapevole ASP.NET semplice che utilizza l'autenticazione Windows.  Fornisce inoltre le istruzioni su come verificare l'applicazione per verificare che le richieste vengano visualizzate quando un utente nell'autenticazione di Windows.  
  
## Contenuto  
  
-   Obiettivi  
  
-   Panoramica  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per i reclami l'autenticazione di Windows  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Obiettivi  
  
-   Configurare un'applicazione Web Form ASP.NET per le richieste utilizzando l'autenticazione di Windows  
  
-   Verificare l'applicazione Web Form ASP.NET per verificare se funziona correttamente  
  
## Panoramica  
 In .NET 4,5, WIF e la relativa all'autorizzazione basata su richieste sono stati inclusi come parte integrante del Framework.  In precedenza, si desiderasse le richieste da un utente ASP.NET, è stato richiesto di installare WIF quindi eseguire il cast delle interfacce agli oggetti principali come `Thread.CurrentPrincipal` o `HttpContext.Current.User`.  Ora, le richieste vengono gestite automaticamente da questi oggetti principali.  
  
 L'autenticazione di Windows è tratto vantaggio dall'inclusione di WIF in .NET 4,5 perché tutti gli utenti autenticati dalle credenziali di Windows automaticamente sono richieste associate.  È possibile avviare utilizzando queste richieste immediatamente in un'applicazione ASP.NET che utilizza l'autenticazione di Windows, in quanto presenti A illustrate.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per i reclami l'autenticazione di Windows  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
 In questo passaggio, verrà creata una nuova applicazione Web Form ASP.NET.  
  
#### Per creare una semplice applicazione ASP.NET  
  
1.  Visual Studio iniziale, quindi scegliere **File**, **Nuova**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
4.  Dopo aver creato il progetto **TestApp** è stato creato, fare clic su in **Esplora soluzioni**.  Le proprietà del progetto verranno visualizzate nel riquadro **Proprietà** in **Esplora soluzioni**.  Impostare la proprietà **Autenticazione di Windows** a **Abilitato**.  
  
    > [!WARNING]
    >  L'autenticazione di Windows è disabilitata per impostazione predefinita nelle nuove applicazioni ASP.NET, pertanto è necessario abilitarla.  
  
## Passaggio 2 \- configurare l'applicazione Web Form ASP.NET per i reclami l'autenticazione di Windows  
 In questo passaggio verrà aggiunta una voce di configurazione al file *Web.config* e si modifica il file *Default.aspx* per visualizzare le informazioni delle richieste di un account.  
  
#### Per configurare un'applicazione ASP.NET di richieste utilizzando l'autenticazione di Windows  
  
1.  *Nel file Default.aspx* del progetto **TestApp**, sostituire il markup esistente con quello riportato di seguito:  
  
    ```  
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true"  
        CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>  
  
    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">  
        <p>  
            This page displays the claims associated with a Windows authenticated user.          
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
  
     Questo passaggio aggiunge un controllo GridView alla *pagina Default.aspx* che verrà popolata con le richieste recuperate dall'autenticazione di Windows.  
  
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
                this.ClaimsGridView.DataSource = claimsPrincipal.Claims;  
                this.ClaimsGridView.DataBind();  
            }  
        }  
    }  
    ```  
  
     Il codice sopra visualizzare le richieste su un utente autenticato.  
  
3.  Per modificare il tipo di autenticazione dell'applicazione, modificare il blocco **\<authentication\>** nella sezione **\<system.web\>** *del file Web.config* radice del progetto in modo che includa solo la seguente voce di configurazione:  
  
    ```  
    <authentication mode="Windows" />  
    ```  
  
4.  Infine, modificare il blocco **\<authorization\>** nella sezione **\<system.web\>** *del file Web.config* per forzare l'autenticazione:  
  
    ```  
    <authorization>  
        <deny users="?" />  
    </authorization>  
    ```  
  
## Passaggio 3 \- eseguire il test della soluzione  
 In questo passaggio verrà l'applicazione Web Form ASP.NET e verificato che le richieste vengano visualizzate quando un utente in con l'autenticazione di Windows.  
  
#### Per testare l'applicazione Web Form ASP.NET per le richieste utilizzando l'autenticazione di Windows  
  
1.  Premere **F5** per compilare ed eseguire l'applicazione.  Dovrebbe essere visualizzata *Default.aspx*e il nome account di Windows \(nome di dominio incluso\) deve già visualizzato come utente autenticato nella destra superiore della pagina.  Il contenuto della pagina deve includere una tabella compilata di richieste recuperate dall'account di Windows.