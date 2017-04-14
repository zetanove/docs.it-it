---
title: "Procedura: Visualizzare lo stato di accesso effettuato con WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4d1174e4-5397-4962-9a5f-3b1ad7b3fc14
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Procedura: Visualizzare lo stato di accesso effettuato con WIF
## Si applica a  
  
-   Foundation \(WIF\) 4,5 di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 In questo argomento viene descritto come visualizzare il segno nello stato in un'applicazione ASP.NET WIF\- abilitata.  WIF fornisce un meccanismo per rendere l'applicazione consapevole su e gestire l'autenticazione e l'autorizzazione per le risorse dell'applicazione.  
  
## Contenuto  
  
-   Panoramica  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- installazione l'identità e accedere all'estensione  
  
-   Passaggio 2 \- creare un'applicazione ASP.NET del componente  
  
-   Passaggio 3 \- consentire allo sviluppo locale servizio token di sicurezza per l'autenticazione degli utenti  
  
-   Passaggio 4 \- modificare l'applicazione ASP.NET visualizzati nello stato  
  
-   Passaggio 5 \- testare l'integrazione tra e WIF l'applicazione ASP.NET  
  
## Panoramica  
 In questo argomento viene illustrato come creare un'applicazione su consapevole semplice mediante WIF e come visualizzare facilmente se un utente è firmato o meno in.  I passaggi seguenti viene utilizzato lo sviluppo locale servizio token di sicurezza incluso con l'identità e l'estensione di Visual Studio Access.  Lo sviluppo locale servizio token di sicurezza è previsto che un test e un ambiente di sviluppo fornire un metodo semplice per l'integrazione delle richieste nell'applicazione.  Non venga mai utilizzato in un ambiente di produzione, poiché non esegue l'autenticazione reale e le credenziali non sono necessarie.  Tuttavia, il codice deve superare i passaggi è identico per un'applicazione pronta per la produzione utilizzando l'autenticazione reale.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- installazione l'identità e accedere all'estensione  
  
-   Passaggio 2 \- creare un'applicazione ASP.NET del componente  
  
-   Passaggio 3 \- consentire allo sviluppo locale servizio token di sicurezza per l'autenticazione degli utenti  
  
-   Passaggio 4 \- modificare l'applicazione ASP.NET visualizzati nello stato  
  
-   Passaggio 5 \- testare l'integrazione tra e WIF l'applicazione ASP.NET  
  
## Passaggio 1 \- installazione l'identità e accedere all'estensione  
 Questo passaggio viene descritto come configurare l'estensione di accesso e di identità a Visual Studio 2012.  Questa estensione automatizzare il processo di configurazione dell'applicazione comunicare con gli endpoint di servizi token di sicurezza.  
  
#### Per installare l'estensione di accesso e di identità  
  
1.  Avviare Visual Studio in modalità con privilegi elevati come amministratore.  
  
2.  In Visual Studio, clicchi **Strumenti** e clicchi **Gestione estensioni**.  Verrà visualizzata la finestra **Gestione estensioni**.  
  
3.  Nella **Gestione estensioni**, scegliere dal menu **Estensioni online** sinistro, quindi **Visual Studio Gallery**.  
  
4.  Nell'angolo superiore destro **Gestione estensioni**, individuare *l'identità e accedere*.  
  
5.  L'elemento **Identità e accesso** verrà visualizzato nei risultati della ricerca.  Fare clic su e quindi fare clic su **Download**.  
  
6.  La finestra di dialogo **Scarica e installa**.  Se si è d'accordo con le condizioni di licenza, fare clic **Installa**.  
  
7.  Quando l'estensione **Identità e accesso** ha completato l'installazione, riavviare Visual Studio in modalità di gestione.  
  
## Passaggio 2 \- creare un'applicazione ASP.NET del componente  
 Questo passaggio viene descritto come creare un'applicazione Web Form ASP.NET del componente che integrerà con WIF.  
  
#### Per creare un'applicazione ASP.NET semplice  
  
1.  Avviare Visual Studio e **File**, **Nuovo**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
## Passaggio 3 \- consentire allo sviluppo locale servizio token di sicurezza per l'autenticazione degli utenti  
 Questo passaggio viene descritto come abilitare lo sviluppo locale servizio token di sicurezza nell'applicazione.  Lo sviluppo locale servizio token di sicurezza è attivata utilizzando l'estensione di accesso e di identità per Visual Studio.  
  
#### Per abilitare sviluppo locale servizio token di sicurezza nell'applicazione ASP.NET  
  
1.  In Visual Studio, fare clic con il pulsante destro del mouse sul progetto **TestApp** in **Esplora soluzioni**, quindi selezionare **Identità e accesso**.  
  
2.  Verrà visualizzata la finestra **Identità e accesso**.  In **Provider**, selezionare **Esegui test dell'applicazione con l'STS di sviluppo locale**, quindi **Applica**.  
  
## Passaggio 4 \- modificare l'applicazione ASP.NET visualizzati nello stato  
 Questo passaggio viene descritto come modificare l'applicazione ASP.NET visualizzazione dinamica se l'utente corrente è firmato in.  Una volta che il provider del servizio token di sicurezza è stato configurato, WIF gestisce le richieste in arrivo.  È necessario configurare il codice dell'applicazione per visualizzare il risultato dell'autenticazione.  
  
#### Per visualizzare accedere allo stato  
  
1.  In Visual Studio, aprire **Default.aspx** sotto il progetto **TestApp**.  
  
2.  Sostituire il markup esistente nel file **Default.aspx** con il markup seguente:  
  
    ```  
    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head runat="server">  
        <title>Logged In Status</title>  
    </head>  
    <body>  
        <asp:label ID="myLabel" runat="server" />  
    </body>  
    </html>  
    ```  
  
3.  Salvare **Default.aspx**quindi aprire il relativo code\-behind denominato **Default.aspx.cs**file.  
  
    > [!NOTE]
    >  **Default.aspx.cs** può essere nascosto in **Default.aspx** in Esplora soluzioni.  Se **Default.aspx.cs** non è visibile, **Default.aspx** facendo clic sul triangolo accanto.  
  
4.  Sostituire il codice esistente in **Default.aspx.cs** con il codice seguente:  
  
    ```csharp  
    using System;  
    using System.Web.UI;  
    using System.Security.Claims;  
  
    namespace TestApp  
    {  
        protected void Page_Load(object sender, EventArgs e)  
        {  
            ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
            if (claimsPrincipal != null)  
            {  
                myLabel.Text = "You are signed in.";  
            }  
            else  
            {  
                myLabel.Text = "You are not signed in.";  
            }  
        }  
    }  
    ```  
  
5.  **Default.aspx.cs**Salvare e compilare l'applicazione.  
  
## Passaggio 5 \- testare l'integrazione tra e WIF l'applicazione ASP.NET  
 Questo passaggio viene descritto come è possibile testare l'integrazione tra e WIF l'applicazione ASP.NET.  
  
#### Per testare l'integrazione tra e WIF ASP.NET  
  
1.  In Visual Studio, premere **F5** per avviare il debug dell'applicazione.  Se nessun errore viene trovato, verrà visualizzata una nuova finestra del browser verrà aperto.  
  
2.  È possibile osservare che il browser viene reindirizzato automaticamente la richiesta al servizio token di sicurezza quindi aprire la pagina Default.aspx.  WIF se è configurato correttamente, verrà visualizzato il sito viene visualizzato il seguente testo: **“È stato effettuato l'accesso”**.