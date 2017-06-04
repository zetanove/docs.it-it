---
title: "Procedura: Trasformare le attestazioni in ingresso | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2831d514-d9d8-4200-9192-954bb6da1126
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# Procedura: Trasformare le attestazioni in ingresso
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 In questa procedura vengono fornite le procedure dettagliate per creare un'applicazione Web Form su consapevole ASP.NET semplice e trasformare le richieste in arrivo.  Fornisce inoltre le istruzioni su come verificare l'applicazione per verificare che i requisiti siano state trasformate quando l'applicazione viene eseguita.  
  
## Contenuto  
  
-   Obiettivi  
  
-   Panoramica  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 al centro attesta la trasformazione utilizzando un ClaimsAuthenticationManager personalizzato  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Obiettivi  
  
-   Configurare un'applicazione Web Form ASP.NET per autenticazione basata su richiesta  
  
-   Trasformare le richieste in arrivo aggiungendo un ruolo Amministratore della richiesta  
  
-   Verificare l'applicazione Web Form ASP.NET per verificare se funziona correttamente  
  
## Panoramica  
 WIF espone <xref:System.Security.Claims.ClaimsAuthenticationManager> classe denominata che consente agli utenti di modificare le richieste prima che vengano visualizzate a un'applicazione di \(RP\) del componente.  <xref:System.Security.Claims.ClaimsAuthenticationManager> è utile per la separazione delle problematiche tra autenticazione e il codice dell'applicazione sottostante.  Nell'esempio seguente viene illustrato come aggiungere un ruolo alle richieste in <xref:System.Security.Claims.ClaimsPrincipal> in ingresso che può essere richiesto da RP.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
  
-   Passaggio 2 al centro attesta la trasformazione utilizzando un ClaimsAuthenticationManager personalizzato  
  
-   Passaggio 3 \- eseguire il test della soluzione  
  
## Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice  
 In questo passaggio, verrà creata una nuova applicazione Web Form ASP.NET.  
  
#### Per creare una semplice applicazione ASP.NET  
  
1.  Avviare Visual Studio in modalità con privilegi elevati come amministratore.  
  
2.  In Visual Studio, fare clic su **File**, scegliere **Nuova**quindi fare clic **Progetto**.  
  
3.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
4.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
5.  Fare clic con il pulsante destro del mouse sul progetto **TestApp** in **Esplora soluzioni**, quindi selezionare **Identità e accesso**.  
  
6.  La finestra **Identità e accesso** visualizzato.  In **Provider**, **Verifica applicazione con STS di sviluppo locale**selezionato, quindi scegliere **Applica**.  
  
7.  *Nel file Default.aspx*, sostituire il markup esistente con il codice seguente, quindi salvare il file:  
  
    ```  
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true"  
        CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>  
  
    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">  
          <h3>Your Claims</h3>  
        <p>  
            <asp:GridView ID="ClaimsGridView" runat="server" CellPadding="3">  
                <AlternatingRowStyle BackColor="White" />  
                <HeaderStyle BackColor="#7AC0DA" ForeColor="White" />  
            </asp:GridView>  
        </p>  
    </asp:Content>  
  
    ```  
  
8.  Aprire il file code\-behind denominato *Default.aspx.cs.* Sostituire il codice esistente con il codice seguente, quindi salvare il file:  
  
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
  
## Passaggio 2 al centro attesta la trasformazione utilizzando un ClaimsAuthenticationManager personalizzato  
 In questo passaggio verrà eseguito l'override della funzionalità predefinita nella classe <xref:System.Security.Claims.ClaimsAuthenticationManager> per aggiungere un ruolo Amministratore per l'entità di protezione in ingresso.  
  
#### Per distribuire trasformazione delle richieste utilizzando un ClaimsAuthenticationManager personalizzato  
  
1.  In Visual Studio, fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Aggiungi**quindi scegliere **Nuovo progetto**.  
  
2.  Nella finestra **Aggiungi nuovo progetto**, **Libreria di classi** selezionato dai modelli **Visual C\#** elenca, immette `ClaimsTransformation`quindi premere **OK**.  Verrà creato il nuovo progetto nella cartella Soluzione.  
  
3.  Fare clic con il pulsante destro del mouse su **Riferimenti** sotto il progetto **ClaimsTransformation** quindi scegliere **Aggiungi riferimento**.  
  
4.  Nella finestra **Gestione riferimenti**, **System.IdentityModel**quindi scegliere **OK**.  
  
5.  **Class1.cs**aperto o, se non esiste, fare clic con il pulsante destro del mouse **ClaimsTransformation**, fare clic **Aggiungi**, quindi fare clic **Classe…**  
  
6.  Aggiungere le seguenti istruzioni using al file di codice:  
  
    ```csharp  
    using System.Security.Claims;  
    using System.Security.Principal;  
    ```  
  
7.  Aggiungere la seguente classe e metodo nel file di codice.  
  
    > [!WARNING]
    >  Il codice seguente è solo a scopo dimostrativo, è importante verificare le autorizzazioni desiderate nel codice di produzione.  
  
    ```csharp  
    public class ClaimsTransformationModule : ClaimsAuthenticationManager  
    {  
        public override ClaimsPrincipal Authenticate(string resourceName, ClaimsPrincipal incomingPrincipal)  
        {  
            if (incomingPrincipal != null && incomingPrincipal.Identity.IsAuthenticated == true)  
            {  
               ((ClaimsIdentity)incomingPrincipal.Identity).AddClaim(new Claim(ClaimTypes.Role, "Admin"));  
            }  
  
            return incomingPrincipal;  
        }  
    }  
    ```  
  
8.  Salvare il file e compilare il progetto **ClaimsTransformation**.  
  
9. Nel progetto **TestApp** ASP.NET, fare clic con il pulsante destro del mouse sui riferimenti e scegliere **Aggiungi riferimento**.  
  
10. Nella finestra **Gestione riferimenti**, **Soluzione** scegliere dal menu, **ClaimsTransformation** sinistro selezionare le opzioni compilano quindi fare clic **OK**.  
  
11. Nel file radice **Web.config**, passare a **\<system.identityModel\>** la voce.  Negli elementi **\<identityConfiguration\>**, aggiungere la seguente riga e salvare il file:  
  
    ```  
    <claimsAuthenticationManager type="ClaimsTransformation.ClaimsTransformationModule, ClaimsTransformation" />  
    ```  
  
## Passaggio 3 \- eseguire il test della soluzione  
 In questo passaggio verrà l'applicazione Web Form ASP.NET e verificato che le richieste vengano visualizzate quando un utente in con l'autenticazione basata su form.  
  
#### Per testare l'applicazione Web Form ASP.NET per le richieste utilizzando l'autenticazione basata su form  
  
1.  Premere **F5** per compilare ed eseguire l'applicazione.  Dovrebbe essere visualizzata *Default.aspx.*  
  
2.  *Nella pagina Default.aspx*, verrà visualizzata una tabella nella direzione **Attestazioni** che include **Autorità emittente**, **OriginalIssuer**, **Tipo**, **Valore**e informazioni delle richieste **Tipovalore** sull'account.  L'ultima riga dovrebbe essere eseguita in modo seguente:  
  
    ||||||  
    |-|-|-|-|-|  
    |AUTORITÀ LOCALE|AUTORITÀ LOCALE|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/role|Admin|http:\/\/www.w3.org\/2001\/XMLSchema\#string|