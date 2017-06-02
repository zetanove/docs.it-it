---
title: "Procedura dettagliata: utilizzo di servizi delle applicazioni client | Microsoft Docs"
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
  - "host di servizi delle applicazioni [servizi delle applicazioni client]"
  - "servizi delle applicazioni client, procedure dettagliate"
ms.assetid: bb7c8950-4517-4dae-b705-b74a14059b26
caps.latest.revision: 47
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 47
---
# Procedura dettagliata: utilizzo di servizi delle applicazioni client
Questo argomento descrive come creare un'applicazione Windows che usa i servizi delle applicazioni client per autenticare gli utenti e recuperare impostazioni e ruoli utente.  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creare un'applicazione Windows Form e usare Progettazione progetti di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per abilitare e configurare i servizi delle applicazioni client.  
  
-   Creare una semplice applicazione del servizio Web ASP.NET per ospitare i servizi delle applicazioni e testare la configurazione client.  
  
-   Aggiungere l'autenticazione basata su form all'applicazione. Si inizierà usando un nome utente e una password specificati a livello di codice \(hardcoded\) per testare il servizio. Si proseguirà quindi aggiungendo un form di accesso specificandolo come provider di credenziali nella configurazione dell'applicazione.  
  
-   Aggiungere la funzionalità basata sui ruoli, abilitando e visualizzando un pulsante solo per gli utenti nel ruolo "manager".  
  
-   Accedere alle impostazioni Web. Si inizierà con il caricamento delle impostazioni Web di un utente \(test\) autenticato nella pagina **Impostazioni** di Progettazione progetti. Si proseguirà quindi con l'uso di Progettazione Windows Form per associare una casella di testo a un'impostazione Web. Infine, il valore modificato verrà salvato nuovamente sul server.  
  
-   Implementare la disconnessione. Verrà aggiunta un'opzione di disconnessione al form e verrà chiamato un metodo di disconnessione.  
  
-   Abilitare la modalità offline. Si fornirà una casella di controllo che consenta agli utenti di specificare lo stato della connessione. Si userà quindi questo valore per specificare se i provider di servizi delle applicazioni client dovranno usare localmente i dati memorizzati nella cache anziché accedere ai servizi Web. Infine, verrà autenticato di nuovo l'utente corrente dopo che l'applicazione torna in modalità online.  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre del componente seguente:  
  
-   [!INCLUDE[vs_orcas_long](../../../includes/vs-orcas-long-md.md)].  
  
## Creazione dell'applicazione client  
 È innanzitutto necessario creare un progetto Windows Form. Questa procedura dettagliata usa i Windows Form perché familiari a più persone. Il processo è tuttavia simile per i progetti Windows Presentation Foundation \(WPF\).  
  
#### Per creare un'applicazione client e abilitare i servizi dell'applicazione client  
  
1.  In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] selezionare l'opzione di menu **File &#124; Nuovo &#124; Progetto**.  
  
2.  Nel riquadro **Tipi progetto** della finestra di dialogo **Nuovo progetto** espandere il nodo **Visual Basic** o **Visual C\#**, quindi selezionare il tipo di progetto **Windows**.  
  
3.  Assicurarsi che l'opzione **.NET Framework 3.5** sia selezionata, quindi selezionare il modello **Applicazione Windows Form**.  
  
4.  Modificare il **Nome** del progetto in `ClientAppServicesDemo`, quindi fare clic su **OK**.  
  
     In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] verrà aperto un nuovo progetto Windows Form.  
  
5.  Scegliere **Proprietà di ClientAppServicesDemo** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra Progettazione progetti.  
  
6.  Nella scheda **Servizi** selezionare **Attiva servizi applicazioni client**.  
  
7.  Assicurarsi che l'opzione **Usa autenticazione basata su form** sia selezionata, quindi impostare **Percorso servizio di autenticazione**, **Percorso servizi ruoli** e **Percorso servizi impostazioni Web** su `http://localhost:55555/AppServices`.  
  
8.  In [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] selezionare la scheda **Applicazione** e scegliere **Definita dall'applicazione** per **Modalità di autenticazione**.  
  
 Le impostazioni specificate nel file app.config dell'applicazione vengono archiviate nella finestra di progettazione.  
  
 A questo punto l'applicazione è configurata per accedere a tutti e tre i servizi dallo stesso host. Nella sezione successiva verrà creato l'host come semplice applicazione del servizio Web in modo che sia possibile testare la configurazione client.  
  
## Creazione dell'host per i servizi delle applicazioni  
 In questa sezione verrà creata una semplice applicazione servizio Web in grado di accedere ai dati dell'utente da un file di database di SQL Server Compact locale. Quindi, il database verrà popolato usando lo [ASP.NET Web Site Administration Tool](../Topic/ASP.NET%20Web%20Site%20Administration%20Tool.md). Questa semplice configurazione consente di testare rapidamente l'applicazione client. In alternativa, è possibile configurare l'host del servizio Web per accedere ai dati dell'utente da un database SQL Server completo o mediante le classi personalizzate <xref:System.Web.Security.MembershipProvider> e <xref:System.Web.Security.RoleProvider>. Per altre informazioni, vedere [Creating and Configuring the Application Services Database for SQL Server](../Topic/Creating%20and%20Configuring%20the%20Application%20Services%20Database%20for%20SQL%20Server.md).  
  
 Nella procedura seguente viene creato e configurato il servizio Web di AppServices.  
  
#### Per creare e configurare l'host dei servizi delle applicazioni  
  
1.  In **Esplora soluzioni** selezionare la soluzione ClientAppServicesDemo, quindi scegliere **Aggiungi &#124; Nuovo progetto** dal menu **File**.  
  
2.  Nel riquadro **Tipi progetto** della finestra di dialogo **Aggiungi nuovo progetto** espandere il nodo **Visual Basic** o **Visual C\#**, quindi scegliere il tipo di progetto **Web**.  
  
3.  Assicurarsi che l'opzione **.NET Framework 3.5** sia selezionata, quindi selezionare il modello **Applicazione servizio Web ASP.NET**.  
  
4.  Modificare il **Nome** del progetto in `AppServices`, quindi fare clic su **OK**.  
  
     Viene aggiunto un nuovo progetto di applicazione del servizio Web ASP.NET alla soluzione e nell'editor viene visualizzato il file Service1.asmx.vb o Service1.asmx.cs.  
  
    > [!NOTE]
    >  Il file Service1.asmx.vb o Service1.asmx.cs in questo esempio non viene usato. È possibile chiuderlo ed eliminarlo da **Esplora soluzioni** per non ingombrare l'ambiente di lavoro.  
  
5.  In **Esplora soluzioni** selezionare il progetto AppServices, quindi scegliere **Proprietà di AppServices** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra Progettazione progetti.  
  
6.  Nella scheda **Web** verificare che l'opzione **Usa Visual Studio Development Server** sia selezionata.  
  
7.  Selezionare **Porta specifica**, specificare il valore `55555`, quindi impostare **Percorso virtuale** su `/AppServices`.  
  
8.  Salvare tutti i file.  
  
9. In **Esplora soluzioni** aprire il file Web.config e individuare il tag di apertura `<system.web>`.  
  
10. Aggiungere il markup seguente prima del tag `<system.web>`.  
  
     Gli elementi `authenticationService`, `profileService` e `roleService` in questo markup abilitano e configurano i servizi delle applicazioni. Ai fini dell'esecuzione del test, l'attributo `requireSSL` dell'elemento `authenticationService` viene impostato su "false". Gli attributi `readAccessProperties` e `writeAccessProperties` dell'elemento `profileService` indicano che la proprietà `WebSettingsTestText` è di lettura\/scrittura.  
  
    > [!NOTE]
    >  Nel codice di produzione è consigliabile accedere al servizio di autenticazione sempre tramite SSL \(Secure Sockets Layer\) usando il protocollo HTTPS. Per informazioni sulla configurazione di SSL, vedere [Configurazione di SSL \(Secure Sockets Layer\) nella guida operativa di IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=91844).  
  
    ```  
    <system.web.extensions>  
      <scripting>  
        <webServices>  
          <authenticationService enabled="true" requireSSL = "false"/>  
          <profileService enabled="true"  
            readAccessProperties="WebSettingsTestText"  
            writeAccessProperties="WebSettingsTestText" />  
          <roleService enabled="true"/>  
        </webServices>  
      </scripting>  
    </system.web.extensions>  
    ```  
  
11. Aggiungere il markup seguente dopo il tag di apertura `<system.web>` in modo che venga incluso nell'elemento `<system.web>`.  
  
     L'elemento `profile` configura una sola impostazione Web denominata `WebSettingsTestText`.  
  
    ```  
    <profile enabled="true" >  
      <properties>  
        <add name="WebSettingsTestText" type="string"   
          readOnly="false" defaultValue="DefaultText"   
          serializeAs="String" allowAnonymous="false" />  
      </properties>  
    </profile>  
  
    ```  
  
 Nella procedura seguente viene usato lo strumento Amministrazione sito Web di ASP.NET per completare la configurazione del servizio e popolare il file di database locale. Vengono aggiunti due utenti denominati `employee` e `manager` appartenenti ai due ruoli con gli stessi nomi. Le password utente sono, rispettivamente, `employee!` e `manager!`.  
  
#### Per configurare l'appartenenza e i ruoli  
  
1.  In **Esplora soluzioni** selezionare il progetto AppServices, quindi scegliere **Configurazione ASP.NET** dal menu **Progetto**.  
  
     Viene visualizzato lo **Strumento Amministrazione sito Web di ASP.NET**.  
  
2.  Nella scheda **Sicurezza** scegliere **Usare la Configurazione guidata sicurezza per configurare la sicurezza mediante passaggi successivi**.  
  
     Viene aperta la **Configurazione guidata sicurezza** e viene visualizzato il passaggio **Introduzione**.  
  
3.  Scegliere **Avanti**.  
  
     Viene visualizzato il passaggio **Selezione del metodo di accesso**.  
  
4.  Selezionare **Da Internet**. Il servizio viene configurato in modo da usare l'autenticazione basata su form anziché l'autenticazione di Windows.  
  
5.  Scegliere **Avanti** per due volte.  
  
     Viene visualizzato il passaggio **Definizione dei ruoli**.  
  
6.  Selezionare **Abilitare i ruoli per il sito Web**.  
  
7.  Scegliere **Avanti**. Viene visualizzato il form **Crea nuovo ruolo**.  
  
8.  Nella casella di testo **Nuovo nome ruolo** digitare `manager`, quindi fare clic su **Aggiungi ruolo**.  
  
     Viene visualizzata la tabella **Ruoli esistenti** con il valore specificato.  
  
9. Nella casella di testo **Nuovo nome ruolo** sostituire `manager` con `employee`, quindi fare clic su **Aggiungi ruolo**.  
  
     Il nuovo valore viene visualizzato nella tabella **Ruoli esistenti**.  
  
10. Scegliere **Avanti**.  
  
     Viene visualizzato il passaggio **Aggiunta di nuovi utenti**.  
  
11. Nel form **Crea utente** specificare i valori seguenti.  
  
    |||  
    |-|-|  
    |**Nome utente**|`manager`|  
    |**Password**|`manager!`|  
    |**Conferma password**|`manager!`|  
    |**Posta elettronica**|`manager@contoso.com`|  
    |**Domanda segreta**|`manager`|  
    |**Risposta segreta**|`manager`|  
  
12. Fare clic su **Crea utente**.  
  
     Viene visualizzato un messaggio che indica l'esito positivo dell'operazione.  
  
    > [!NOTE]
    >  Nel form è richiesta l'immissione dei valori **Posta elettronica**, **Domanda segreta** e **Risposta segreta**; in questo esempio tuttavia questi valori non vengono usati.  
  
13. Scegliere **Continua**.  
  
     Viene visualizzato nuovamente il form **Crea utente**.  
  
14. Nel form **Crea utente** specificare i valori seguenti.  
  
    |||  
    |-|-|  
    |**Nome utente**|`employee`|  
    |**Password**|`employee!`|  
    |**Conferma password**|`employee!`|  
    |**Posta elettronica**|`employee@contoso.com`|  
    |**Domanda segreta**|`Employee`|  
    |**Risposta segreta**|`employee`|  
  
15. Fare clic su **Crea utente**.  
  
     Viene visualizzato un messaggio che indica l'esito positivo dell'operazione.  
  
16. Scegliere **Fine**.  
  
     Viene visualizzato nuovamente lo **Strumento Amministrazione sito Web di ASP.NET**.  
  
17. Fare clic su **Utenti Manager**.  
  
     Viene visualizzato l'elenco degli utenti.  
  
18. Fare clic su **Modifica ruoli** per l'utente **employee**, quindi selezionare il ruolo **employee**.  
  
19. Fare clic su **Modifica ruoli** per l'utente **manager**, quindi selezionare il ruolo **manager**.  
  
20. Chiudere la finestra del browser contenente lo **Strumento Amministrazione sito Web**.  
  
21. Se viene visualizzata una finestra di messaggio in cui viene chiesto se si vuole ricaricare il file Web.config modificato, fare clic su **Sì**.  
  
 Questo completa la configurazione del servizio Web. A questo punto è possibile premere F5 per eseguire l'applicazione client insieme alla quale verrà automaticamente avviato il **Server di sviluppo ASP.NET**. Il server rimarrà in esecuzione dopo la chiusura dell'applicazione, ma verrà riavviato al riavvio dell'applicazione. In questo modo è possibile rilevare tutte le modifiche apportate al file Web.config.  
  
 Per arrestare manualmente il server, fare clic con il pulsante destro del mouse sull'icona di Server di sviluppo ASP.NET nell'area di notifica della barra delle applicazioni, quindi scegliere **Arresta**. Questa operazione è talvolta utile per assicurarsi che il riavvio venga eseguito correttamente.  
  
## Aggiunta dell'autenticazione basata su form  
 Nella procedura seguente viene aggiunto il codice al form principale che tenta di convalidare l'utente e nega l'accesso quando l'utente specifica credenziali non valide. Vengono usati un nome utente e una password specificati a livello di codice \(hardcoded\) per testare il servizio.  
  
#### Per convalidare l'utente nel codice dell'applicazione  
  
1.  Nel progetto ClientAppServicesDemo in **Esplora soluzioni** aggiungere un riferimento all'assembly System.Web.  
  
2.  Selezionare il file Form1, quindi scegliere **Visualizza &#124; Codice** dal menu principale di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
3.  Nell'editor del codice aggiungere le seguenti istruzioni all'inizio del file Form1.  
  
     [!code-csharp[ClientApplicationServices#001](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#001)]
     [!code-vb[ClientApplicationServices#001](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#001)]  
  
4.  In **Esplora soluzioni** fare doppio clic su Form1 per visualizzare la finestra di progettazione.  
  
5.  Nella finestra di progettazione fare doppio clic nell'area del form per generare un gestore eventi <xref:System.Windows.Forms.Form.Load?displayProperty=fullName> denominato `Form1_Load`.  
  
     Verrà visualizzato il cursore nel metodo `Form1_Load` all'interno dell'editor del codice.  
  
6.  Aggiungere al metodo `Form1_Load` il seguente codice.  
  
     Questo codice nega l'accesso agli utenti non autenticati chiudendo l'applicazione. In alternativa, è possibile consentire agli utenti non autenticati di accedere al form ma non a specifiche funzionalità. Generalmente non è necessario specificare a livello di codice il nome utente e la password, tuttavia questa operazione è utile a scopo di test. Nella sezione successiva verrà sostituito questo codice con un codice più affidabile che visualizza una finestra di dialogo di accesso e include la gestione delle eccezioni.  
  
     Si noti che il metodo `static`<xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> è incluso in [!INCLUDE[dnprdnext](../../../includes/dnprdnext-md.md)]. Questo metodo delega il lavoro al provider di autenticazione configurato e restituisce `true` se l'autenticazione viene eseguita correttamente. L'applicazione non richiede un riferimento diretto al provider di autenticazione del client.  
  
     [!code-csharp[ClientApplicationServices#300](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#300)]
     [!code-vb[ClientApplicationServices#300](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#300)]  
  
 È ora possibile premere F5 per eseguire l'applicazione. Poiché sono stati specificati un nome utente e una password corretti, è possibile vedere il form.  
  
> [!NOTE]
>  Se non si è in grado di eseguire l'applicazione, provare ad arrestare il server di sviluppo ASP.NET. Al riavvio del server verificare che la porta sia impostata su 55555.  
  
 Per visualizzare invece il messaggio di errore, modificare i parametri <xref:System.Web.Security.Membership.ValidateUser%2A>. Sostituire ad esempio il secondo parametro `"manager!"` con una password non corretta come `"MANAGER"`.  
  
## Aggiunta di un form di accesso come provider di credenziali  
 È possibile acquisire le credenziali utente nel codice dell'applicazione e passarli al metodo <xref:System.Web.Security.Membership.ValidateUser%2A>. Tuttavia, è spesso utile separare il codice di acquisizione delle credenziali da quello dell'applicazione, qualora dovesse essere necessario modificarlo in seguito.  
  
 Nella procedura seguente viene configurata l'applicazione per usare un provider di credenziali e quindi viene modificata la chiamata al metodo <xref:System.Web.Security.Membership.ValidateUser%2A> in modo da passare <xref:System.String.Empty> per entrambi i parametri. Le stringhe vuote indicano al metodo <xref:System.Web.Security.Membership.ValidateUser%2A> di chiamare il metodo <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> del provider di credenziali configurato.  
  
#### Per configurare l'applicazione in modo da usare un provider di credenziali  
  
1.  In **Esplora soluzioni** selezionare il progetto ClientAppServicesDemo, quindi scegliere **Proprietà di ClientAppServicesDemo** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra Progettazione progetti.  
  
2.  Nella scheda **Servizi** impostare il valore seguente per **Facoltativo: provider di credenziali**. Questo valore indica il nome di tipo qualificato dall'assembly.  
  
    ```  
    ClientAppServicesDemo.Login, ClientAppServicesDemo  
    ```  
  
3.  Nel file di codice Form1 sostituire il codice nel metodo `Form1_Load` con il codice seguente.  
  
     Questo codice visualizza un messaggio di benvenuto e quindi chiama il metodo `ValidateUsingCredentialsProvider` che verrà aggiunto nel passaggio successivo. Se l'utente non è autenticato, il metodo `ValidateUsingCredentialsProvider` restituisce `false` e viene restituito il metodo `Form1_Load`. In questo modo si evita l'esecuzione di codice aggiuntivo prima di uscire dall'applicazione. Il messaggio di benvenuto è utile per capire quando viene riavviata l'applicazione. Il codice per riavviare l'applicazione verrà aggiunto quando si implementa la disconnessione più avanti in questa procedura dettagliata.  
  
     [!code-csharp[ClientApplicationServices#011](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#011)]
     [!code-vb[ClientApplicationServices#011](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#011)]  
  
4.  Aggiungere il metodo seguente dopo il metodo `Form1_Load`.  
  
     Questo metodo passa stringhe vuote al metodo `static`<xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> in modo che venga visualizzata la finestra di dialogo Accesso. Se il servizio di autenticazione non è disponibile, il metodo <xref:System.Web.Security.Membership.ValidateUser%2A> genererà un'eccezione <xref:System.Net.WebException>. In questo caso, il metodo `ValidateUsingCredentialsProvider` visualizza un messaggio di avviso e chiede se l'utente vuole riprovare in modalità offline. Questa funzionalità richiede la funzione **Salva hash della password localmente per consentire l'accesso offline** descritta in [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md). Questa funzionalità è abilitata per impostazione predefinita per i nuovi progetti.  
  
     Se l'utente non è convalidato, il metodo `ValidateUsingCredentialsProvider` visualizza un messaggio di errore e chiude l'applicazione. Quindi, restituisce il risultato del tentativo di autenticazione.  
  
     [!code-csharp[ClientApplicationServices#020](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#020)]
     [!code-vb[ClientApplicationServices#020](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#020)]  
  
### Creazione di un form di accesso  
 Un provider di credenziali è una classe che implementa l'interfaccia <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>. Questa interfaccia contiene un solo metodo denominato <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> che restituisce un oggetto <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>. Le procedure seguenti illustrano come creare una finestra di dialogo di accesso che implementi <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> in modo che venga visualizzata la finestra stessa e vengano restituite le credenziali specificate dall'utente.  
  
 È necessario seguire procedure separate per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] e C\# perché [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] include un modello **Form di accesso**, che consente di risparmiare tempo richiedendo meno codice da scrivere.  
  
##### Per creare una finestra di dialogo di accesso come provider di credenziali in Visual Basic  
  
1.  In **Esplora soluzioni** selezionare il progetto ClientAppServicesDemo, quindi scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare il modello **Form di accesso**, modificare l'elemento **Nome** su `Login.vb`, quindi fare clic su **Aggiungi**.  
  
     In Progettazione Windows Form verrà visualizzata la finestra di dialogo di accesso.  
  
3.  Nella finestra di progettazione scegliere **OK**, quindi impostare `DialogResult` su `OK` nella finestra **Proprietà**.  
  
4.  Nella finestra di progettazione aggiungere un controllo `CheckBox` al form sotto la casella di testo **Password**.  
  
5.  Nella finestra **Proprietà** specificare il valore `rememberMeCheckBox` per **\(Name\)** e il valore `&Remember me` per **Text**.  
  
6.  Scegliere **Visualizza &#124; Codice** dal menu principale di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
7.  Nell'editor del codice aggiungere il codice seguente all'inizio del file.  
  
     [!code-vb[ClientApplicationServices#101](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Login.vb#101)]  
  
8.  Modificare la firma della classe in modo che quest'ultima implementi l'interfaccia <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>.  
  
     [!code-vb[ClientApplicationServices#110](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#110)]  
  
9. Assicurarsi che il cursore sia posizionato dopo `IClientformsAuthenticationCredentialsProvider`, quindi premere INVIO per generare il metodo `GetCredentials`.  
  
10. Individuare l'implementazione di <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A>, quindi sostituirla con il codice seguente.  
  
     [!code-vb[ClientApplicationServices#120](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Login.vb#120)]  
  
 La procedura C\# seguente fornisce l'elenco di codice completo per la generazione di una semplice finestra di dialogo di accesso. La parte importante di questa finestra di dialogo dal layout piuttosto essenziale è costituita dall'implementazione di <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A>.  
  
##### Per creare una finestra di dialogo di accesso come provider di credenziali in C\#  
  
1.  In **Esplora soluzioni** selezionare il progetto ClientAppServicesDemo, quindi scegliere **Aggiungi classe** dal menu **Progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** modificare il **Nome** in `Login.cs`, quindi fare clic su **Aggiungi**.  
  
     Il file Login.cs verrà aperto nell'editor del codice.  
  
3.  Sostituire il codice predefinito con il codice seguente.  
  
     [!code-csharp[ClientApplicationServices#200](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Login.cs#200)]  
  
 È ora possibile eseguire l'applicazione che visualizzerà la finestra di dialogo di accesso. Per testare questo codice, provare a specificare credenziali diverse, sia valide che non valide, e verificare che sia possibile accedere al form solo con le credenziali valide. I nomi utente validi sono `employee` e `manager` con le password `employee!` e `manager!`, rispettivamente.  
  
> [!NOTE]
>  Non selezionare **Memorizza dati** in questa fase, altrimenti non sarà possibile accedere come altro utente finché non si implementa la disconnessione più avanti in questa procedura dettagliata.  
  
## Aggiunta di funzionalità basate su ruoli  
 Nella procedura seguente verrà aggiunto al form un pulsante che verrà visualizzato solo dagli utenti nel ruolo di manager.  
  
#### Per modificare l'interfaccia utente basata sul ruolo utente  
  
1.  In **Esplora soluzioni**, nel progetto ClientAppServicesDemo, selezionare Form1, quindi scegliere **Visualizza &#124; Finestra di progettazione** dal menu principale di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
2.  Nella finestra di progettazione aggiungere un controllo <xref:System.Windows.Forms.Button> al form dalla **Casella degli strumenti**.  
  
3.  Nella finestra **Proprietà** impostare le proprietà seguenti per il pulsante.  
  
    |Proprietà|Valore|  
    |---------------|------------|  
    |**\(Nome\)**|managerOnlyButton|  
    |**Testo**|&Manager task|  
    |**Visible**|`False`|  
  
4.  Nell'editor di codice relativo a Form1 aggiungere il codice seguente alla fine del metodo `Form1_Load`.  
  
     Questo codice chiama il metodo `DisplayButtonForManagerRole` che verrà aggiunto nel passaggio successivo.  
  
     [!code-csharp[ClientApplicationServices#012](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#012)]
     [!code-vb[ClientApplicationServices#012](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#012)]  
  
5.  Aggiungere il metodo seguente alla fine della classe Form1.  
  
     Questo metodo chiama il metodo <xref:System.Security.Principal.IPrincipal.IsInRole%2A> dell'oggetto <xref:System.Security.Principal.IPrincipal> restituito dalla proprietà `static`<xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName>. Per le applicazioni configurate per l'uso dei servizi delle applicazioni client, questa proprietà restituisce un oggetto <xref:System.Web.ClientServices.ClientRolePrincipal>. Poiché questa classe implementa l'interfaccia <xref:System.Security.Principal.IPrincipal>, non è necessario farvi riferimento in modo esplicito.  
  
     Se l'utente appartiene al ruolo "manager", il metodo `DisplayButtonForManagerRole` imposta la proprietà <xref:System.Windows.Forms.Control.Visible%2A> di `managerOnlyButton` su `true`. Se viene generata un'eccezione <xref:System.Net.WebException>, questo metodo visualizza anche un messaggio di errore che indica che il servizio dei ruoli non è disponibile.  
  
    > [!NOTE]
    >  Il metodo <xref:System.Web.ClientServices.ClientRolePrincipal.IsInRole%2A> restituirà sempre `false` se l'accesso utente è scaduto. Questo messaggio di errore non viene visualizzato se l'applicazione chiama il metodo <xref:System.Security.Principal.IPrincipal.IsInRole%2A> una volta subito dopo l'autenticazione, come illustrato nel codice di esempio nella presente procedura dettagliata. Se l'applicazione deve recuperare ruoli utente in altri momenti, è necessario aggiungere il codice per riconvalidare gli utenti con accesso scaduto. Se tutti gli utenti validi sono stati assegnati ai ruoli, è possibile determinare se l'accesso è scaduto chiamando il metodo <xref:System.Web.ClientServices.Providers.ClientRoleProvider.GetRolesForUser%2A?displayProperty=fullName>. Se non viene restituito alcun ruolo, l'accesso è scaduto. Per un esempio di questa funzionalità, vedere il metodo <xref:System.Web.ClientServices.Providers.ClientRoleProvider.GetRolesForUser%2A>. Questa funzionalità è necessaria solo se è stato selezionato **Richiedi agli utenti di accedere di nuovo a ogni scadenza del cookie del server** nella configurazione dell'applicazione. Per altre informazioni, vedere [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md).  
  
     [!code-csharp[ClientApplicationServices#030](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#030)]
     [!code-vb[ClientApplicationServices#030](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#030)]  
  
 Se l'autenticazione viene eseguita correttamente, il provider di autenticazione del client imposta la proprietà <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> su un'istanza della classe <xref:System.Web.ClientServices.ClientRolePrincipal>. Questa classe implementa il metodo <xref:System.Security.Principal.IPrincipal.IsInRole%2A> in modo che il lavoro venga delegato al provider di ruoli configurato. Come in precedenza il codice dell'applicazione non richiede un riferimento diretto al provider di servizi.  
  
 È ora possibile eseguire l'applicazione e accedere come employee per non vedere il pulsante e come manager per visualizzarlo.  
  
## Accesso alle impostazioni Web  
 Nella procedura seguente verrà aggiunta al form una casella di testo che verrà associata a un'impostazione Web. Come il codice precedente che usa autenticazione e ruoli, il codice delle impostazioni non accede direttamente al provider delle impostazioni. Usa invece la classe `Settings` fortemente tipizzata \(alla quale si accede come `Properties.Settings.Default` in C\# e come `My.Settings` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) generata per il progetto da [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
#### Per usare le impostazioni Web nell'interfaccia utente  
  
1.  Assicurarsi che il **Server di sviluppo Web ASP.NET** sia ancora in esecuzione controllando l'area di notifica della barra delle applicazioni. Se è stato arrestato il server, riavviare l'applicazione \(la quale avvia automaticamente il server\), quindi chiudere la finestra di dialogo di accesso.  
  
2.  In **Esplora soluzioni** selezionare il progetto ClientAppServicesDemo, quindi scegliere **Proprietà di ClientAppServicesDemo** dal menu **Progetto**.  
  
     Verrà visualizzata la finestra Progettazione progetti.  
  
3.  Nella scheda **Impostazioni** fare clic su **Carica impostazioni Web**.  
  
     Verrà visualizzata la finestra di dialogo **Accesso**.  
  
4.  Immettere le credenziali per employee o manager, quindi fare clic su **Accedi**. L'impostazione Web che verrà usata è configurata per l'accesso solo da parte di utenti autenticati. Pertanto, se si seleziona **Ignora accesso**, non verrà caricata alcuna impostazione.  
  
     L'impostazione `WebSettingsTestText` viene visualizzata nella finestra di progettazione con il valore predefinito `DefaultText`. Inoltre, per il progetto viene generata una classe `Settings` che contiene una proprietà `WebSettingsTestText`.  
  
5.  In **Esplora soluzioni**, nel progetto ClientAppServicesDemo, selezionare Form1, quindi scegliere **Visualizza &#124; Finestra di progettazione** dal menu principale di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
6.  Nella finestra di progettazione aggiungere un controllo <xref:System.Windows.Forms.TextBox> al form.  
  
7.  Nella finestra **Proprietà** specificare una valore `webSettingsTestTextBox` per **\(Name\)**.  
  
8.  Nell'editor del codice aggiungere il codice seguente alla fine del metodo `Form1_Load`.  
  
     Questo codice chiama il metodo `BindWebSettingsTestTextBox` che verrà aggiunto nel passaggio successivo.  
  
     [!code-csharp[ClientApplicationServices#013](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#013)]
     [!code-vb[ClientApplicationServices#013](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#013)]  
  
9. Aggiungere il metodo seguente alla fine della classe Form1.  
  
     Questo metodo associa la proprietà <xref:System.Windows.Forms.TextBox.Text%2A> di `webSettingsTestTextBox` alla proprietà `WebSettingsTestText` della classe `Settings` generata precedentemente in questa procedura. Se viene generata un'eccezione <xref:System.Net.WebException>, questo metodo visualizza inoltre un messaggio di errore che indica che il servizio di impostazioni Web non è disponibile.  
  
     [!code-csharp[ClientApplicationServices#040](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#040)]
     [!code-vb[ClientApplicationServices#040](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#040)]  
  
    > [!NOTE]
    >  In genere viene usato un data binding per abilitare la comunicazione bidirezionale automatica tra un controllo e un'impostazione Web. Tuttavia, è anche possibile accedere direttamente alle impostazioni Web come illustrato nell'esempio seguente:  
  
     [!code-csharp[ClientApplicationServices#322](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#322)]
     [!code-vb[ClientApplicationServices#322](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#322)]  
  
10. Selezionare il form nella finestra di progettazione, quindi fare clic sul pulsante **Eventi** nella finestra **Proprietà**.  
  
11. Selezionare l'evento <xref:System.Windows.Forms.Form.FormClosing>, quindi premere INVIO per generare un gestore eventi.  
  
12. Sostituire il metodo generato con il codice seguente.  
  
     Il gestore eventi <xref:System.Windows.Forms.Form.FormClosing> chiama il metodo `SaveSettings` che viene usato anche dalla funzionalità di disconnessione che verrà aggiunta nella sezione successiva. Il metodo `SaveSettings` verifica innanzitutto che l'utente non sia disconnesso. Questa operazione viene eseguita controllando la proprietà <xref:System.Security.Principal.IIdentity.AuthenticationType%2A> dell'oggetto <xref:System.Security.Principal.IIdentity> restituito dall'entità corrente, la quale viene recuperata mediante la proprietà `static`<xref:System.Threading.Thread.CurrentPrincipal%2A>. Se l'utente è stato autenticato per i servizi delle applicazioni client, il tipo di autenticazione sarà "ClientForms." Il metodo `SaveSettings` non può controllare solo la proprietà <xref:System.Security.Principal.IIdentity.IsAuthenticated%2A?displayProperty=fullName> perché l'utente potrebbe usare un'identità di Windows valida dopo la disconnessione.  
  
     Se l'utente non si è disconnesso, il metodo `SaveSettings` chiama il metodo <xref:System.Configuration.ApplicationSettingsBase.Save%2A> della classe `Settings` generata precedentemente in questa procedura. Questo metodo può generare un'eccezione <xref:System.Net.WebException> se il cookie di autenticazione è scaduto. Questa situazione si verifica solo se è stata selezionata l'opzione **Richiedi agli utenti di accedere di nuovo a ogni scadenza del cookie del server** nella configurazione dell'applicazione. Per altre informazioni, vedere [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md). Il metodo `SaveSettings` gestisce la scadenza del cookie chiamando <xref:System.Web.Security.Membership.ValidateUser%2A> per visualizzare la finestra di dialogo di accesso. Se l'utente accede correttamente, il metodo `SaveSettings` tenta di salvare nuovamente le impostazioni chiamando se stesso.  
  
     Come nel codice precedente, il metodo `SaveSettings` visualizza un messaggio di errore se il servizio remoto non è disponibile. Se il provider delle impostazioni non può accedere al servizio remoto, le impostazioni vengono ancora salvate nella cache locale e ricaricate all'avvio dell'applicazione.  
  
     [!code-csharp[ClientApplicationServices#050](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#050)]
     [!code-vb[ClientApplicationServices#050](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#050)]  
  
13. Aggiungere il metodo seguente alla fine della classe Form1.  
  
     Questo codice gestisce l'evento <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved?displayProperty=fullName> e visualizza un messaggio di avviso se non è stato possibile salvare un'impostazione. L'evento <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved> non si verifica se il servizio delle impostazioni non è disponibile o se il cookie di autenticazione è scaduto. L'evento <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved> si verifica ad esempio se l'utente si è già disconnesso. È possibile testare questo gestore eventi aggiungendo il codice di disconnessione al metodo `SaveSettings` direttamente prima della chiamata al metodo <xref:System.Configuration.ApplicationSettingsBase.Save%2A>. Il codice di disconnessione che è possibile usare verrà descritto nella sezione successiva.  
  
     [!code-csharp[ClientApplicationServices#090](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#090)]
     [!code-vb[ClientApplicationServices#090](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#090)]  
  
14. Per il linguaggio C\# aggiungere il codice seguente alla fine del metodo `Form1_Load`. Questo codice associa il metodo aggiunto nell'ultimo passaggio all'evento <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved>.  
  
     [!code-csharp[ClientApplicationServices#015](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#015)]  
  
 Per testare l'applicazione in questa fase, eseguire più volte questo codice sia come employee che come manager e digitare i diversi valori nella casella di testo. I valori rimarranno validi per tutte le sessioni di ciascun utente.  
  
## Implementazione della disconnessione  
 Se l'utente seleziona la casella di controllo **Memorizza dati** all'accesso, l'applicazione autenticherà automaticamente l'utente nelle esecuzioni successive. L'autenticazione automatica continuerà quindi mentre l'applicazione è in modalità offline o fino alla scadenza del cookie di autenticazione. Può tuttavia capitare che all'applicazione debbano accedere più utenti oppure un solo utente più volte con credenziali diverse. Per consentire questo scenario, è necessario implementare la funzionalità di disconnessione, come descritto nella procedura seguente.  
  
#### Per implementare la funzionalità di disconnessione  
  
1.  Nella finestra di progettazione Form1 aggiungere un controllo <xref:System.Windows.Forms.Button> al form dalla **Casella degli strumenti**.  
  
2.  Nella finestra **Proprietà** specificare il valore `logoutButton` per **\(Name\)** e il valore **&Disconnetti** per **Text**.  
  
3.  Fare doppio clic su `logoutButton` per generare un gestore eventi <xref:System.Windows.Forms.Control.Click>.  
  
     Verrà visualizzato il cursore nel metodo `logoutButton_Click` all'interno dell'editor del codice.  
  
4.  Sostituire il metodo `logoutButton_Click` generato con il codice seguente.  
  
     Questo gestore eventi chiama innanzitutto il metodo `SaveSettings` aggiunto nella sezione precedente. Il gestore eventi chiama quindi il metodo <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.Logout%2A?displayProperty=fullName>. Se il servizio di autenticazione non è disponibile, il metodo <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.Logout%2A> genererà un'eccezione <xref:System.Net.WebException>. In questo caso, il metodo `logoutButton_Click` visualizza un messaggio di avviso e passa temporaneamente alla modalità offline per disconnettere l'utente. La modalità offline viene descritta nella sezione successiva.  
  
     Con la disconnessone viene eliminato il cookie di autenticazione locale in modo che all'avvio dell'applicazione vengano richieste le credenziali di accesso. Dopo la disconnessione il gestore eventi riavvia l'applicazione. Al riavvio dell'applicazione viene visualizzato il messaggio di benvenuto seguito dalla finestra di dialogo di accesso. Il messaggio di benvenuto serve a indicare in modo esplicito che l'applicazione è stata riavviata. Questo processo semplifica le operazioni qualora l'utente dovesse effettuare l'accesso per salvare le impostazioni e quindi eseguire di nuovo l'accesso a causa del riavvio dell'applicazione.  
  
     [!code-csharp[ClientApplicationServices#070](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#070)]
     [!code-vb[ClientApplicationServices#070](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#070)]  
  
 Per testare la funzionalità di disconnessione, eseguire l'applicazione e selezionare **Memorizza dati** nella finestra di dialogo Accesso. Quindi, chiudere e riavviare l'applicazione per assicurarsi di non dover più eseguire l'accesso. Riavviare quindi l'applicazione facendo clic su Disconnessione.  
  
## Abilitazione della modalità offline  
 Nella procedura seguente viene aggiunta una casella di controllo al form per consentire all'utente di attivare la modalità offline. L'applicazione indica che è attiva la modalità offline impostando la proprietà `static`<xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A?displayProperty=fullName> su `true`. Lo stato offline viene archiviato sul disco rigido locale nel percorso indicato dalla proprietà <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=fullName>. Ciò significa che lo stato offline viene archiviato in base all'utente e all'applicazione.  
  
 In modalità offline, tutte le richieste dei servizi delle applicazioni client recuperano i dati dalla cache locale anziché tentare di accedere ai servizi. Nella configurazione predefinita, i dati locali includono la password crittografata dell'utente, per consentire all'utente di effettuare l'accesso mentre l'applicazione è in modalità offline. Per altre informazioni, vedere [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md).  
  
#### Per abilitare la modalità offline nell'applicazione  
  
1.  In **Esplora soluzioni**, nel progetto ClientAppServicesDemo, selezionare Form1, quindi scegliere **Visualizza &#124; Finestra di progettazione** dal menu principale di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
2.  Nella finestra di progettazione aggiungere un controllo <xref:System.Windows.Forms.CheckBox> al form.  
  
3.  Nella finestra **Proprietà** specificare il valore `workOfflineCheckBox` per **\(Name\)** e il valore **&Non in linea** per **Text**.  
  
4.  Nella finestra **Proprietà** fare clic sul pulsante **Eventi**.  
  
5.  Selezionare l'evento <xref:System.Windows.Forms.CheckBox.CheckedChanged>, quindi premere INVIO per generare un gestore eventi.  
  
6.  Sostituire il metodo generato con il codice seguente.  
  
     Questo codice aggiorna il valore <xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A> e riconvalida l'utente automaticamente quando ritorna in modalità online. Il metodo <xref:System.Web.ClientServices.ClientFormsIdentity.RevalidateUser%2A?displayProperty=fullName> usa le credenziali memorizzate nella cache in modo che l'utente non debba eseguire l'accesso in modo esplicito. Se il servizio di autenticazione non è disponibile, viene visualizzato un messaggio di avviso e l'applicazione rimane in modalità offline.  
  
    > [!NOTE]
    >  Il metodo <xref:System.Web.ClientServices.ClientFormsIdentity.RevalidateUser%2A> viene fornito solo per praticità e poiché non restituisce un valore non può indicare se la riconvalida non è riuscita. La riconvalida può non riuscire, ad esempio, se le credenziali utente sono state modificato nel server. In questo caso, è necessario includere il codice che convalida in modo esplicito gli utenti dopo l'esito negativo di una chiamata al servizio. Per altre informazioni, vedere la sezione Accesso alle impostazioni Web descritta in precedenza in questa procedura dettagliata.  
  
     Dopo la riconvalida, questo codice salva tutte le modifiche apportate alle impostazioni Web locali chiamando il metodo `SaveSettings` aggiunto in precedenza. Recupera quindi tutti i nuovi valori nel server chiamando il metodo <xref:System.Configuration.ApplicationSettingsBase.Reload%2A> della classe `Settings` del progetto \(alla quale si accede come `Properties.Settings.Default` in C\# e come `My.Settings` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\).  
  
     [!code-csharp[ClientApplicationServices#080](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#080)]
     [!code-vb[ClientApplicationServices#080](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#080)]  
  
7.  Aggiungere il codice seguente alla fine del metodo `Form1_Load` per assicurarsi che la casella di controllo visualizzi lo stato di connessione corrente.  
  
     [!code-csharp[ClientApplicationServices#014](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#014)]
     [!code-vb[ClientApplicationServices#014](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#014)]  
  
 Questo completa l'applicazione di esempio. Per testare la funzionalità offline, eseguire l'applicazione, accedere come employee o manager e quindi selezionare **Offline**. Modificare il valore nella casella di testo, quindi chiudere l'applicazione e riavviarla. Prima di effettuare l'accesso, fare clic con il pulsante destro del mouse sull'icona di Server di sviluppo ASP.NET nell'area di notifica della barra delle applicazioni, quindi scegliere **Arresta**. Eseguire l'accesso normalmente. Anche quando il server non è in esecuzione, è comunque possibile eseguire l'accesso. Modificare il valore della casella di testo e riavviare per visualizzare il valore modificato.  
  
## Riepilogo  
 In questa procedura dettagliata è stato descritto come abilitare e usare i servizi delle applicazioni client in un'applicazione Windows Form. Dopo avere configurato un server di prova, è stato aggiunto il codice all'applicazione per autenticare gli utenti e recuperare i ruoli utente e le impostazioni dell'applicazione dal server. È stato inoltre descritto come abilitare la modalità offline per consentire all'applicazione di usare una cache di dati locale anziché i servizi remoti quando la connessione non è disponibile.  
  
## Passaggi successivi  
 In un'applicazione reale si accederà ai dati di molti utenti da un server remoto che non sempre potrebbe essere disponibile o che potrebbe arrestarsi senza preavviso. Per rendere affidabile l'applicazione, è necessario reagire in maniera appropriata quando il servizio non è disponibile. Questa procedura dettagliata include blocchi try\/catch che consentono di rilevare un'eccezione <xref:System.Net.WebException> e visualizzare un messaggio di errore quando il servizio non è disponibile. Nel codice di produzione può essere opportuno gestire questa situazione passando alla modalità offline, uscendo dall'applicazione o negando l'accesso a funzionalità specifiche.  
  
 Per aumentare la sicurezza dell'applicazione, assicurarsi di testare completamente l'applicazione e il server prima della distribuzione.  
  
## Vedere anche  
 [Servizi applicazioni client](../../../docs/framework/common-client-technologies/client-application-services.md)   
 [Cenni preliminari sui servizi delle applicazioni client](../../../docs/framework/common-client-technologies/client-application-services-overview.md)   
 [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)   
 [ASP.NET Web Site Administration Tool](../Topic/ASP.NET%20Web%20Site%20Administration%20Tool.md)   
 [Creating and Configuring the Application Services Database for SQL Server](../Topic/Creating%20and%20Configuring%20the%20Application%20Services%20Database%20for%20SQL%20Server.md)   
 [Walkthrough: Using ASP.NET Application Services](../Topic/Walkthrough:%20Using%20ASP.NET%20Application%20Services.md)