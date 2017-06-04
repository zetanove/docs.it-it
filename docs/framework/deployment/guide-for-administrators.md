---
title: "Guida alla distribuzione di .NET Framework per amministratori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "guida dell'amministratore, distribuzione di .NET Framework"
  - "distribuzione [.NET Framework], guida dell'amministratore"
ms.assetid: bee14036-0436-44e8-89f5-4bc61317977a
caps.latest.revision: 40
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 38
---
# Guida alla distribuzione di .NET Framework per amministratori
In questo articolo dettagliato vengono descritte le modalità in cui un amministratore di sistema può distribuire [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e le relative dipendenze di sistema attraverso una rete usando Microsoft System Center Configuration Manager.  L'articolo presuppone che tutti i computer client di destinazione soddisfino i requisiti minimi per .NET Framework.  Per un elenco di requisiti software e hardware per l'installazione di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md).  
  
> [!NOTE]
>  Il software a cui si fa riferimento nel presente documento, inclusi, in via esemplificativa, [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], System Center Configuration Manager e Active Directory sono soggette alle condizioni di licenza.  Queste istruzioni presuppongono che tali condizioni di licenza siano state riviste e accettate dai licenziatari del software  e non derogano ad alcuna condizione di tali contratti di licenza.  
>   
>  Per informazioni sul supporto per .NET Framework, consultare [Criteri relativi al ciclo di vita del supporto Microsoft .NET Framework](http://go.microsoft.com/fwlink/?LinkId=196607) nel sito Web del supporto tecnico Microsoft.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
 [Processo di distribuzione](#the_deployment_process)   
 [Distribuzione di .NET Framework](#deploying_in_a_test_environment)  
 [Creare una raccolta](#creating_a_collection)  
 [Creare un pacchetto e un programma](#creating_a_package)  
 [Selezionare un punto di distribuzione](#select_dist_point)  
 [Distribuire il pacchetto](#deploying_package)  
 [Risorse](#resources)  
 [Risoluzione dei problemi](#troubleshooting)  
  
<a name="the_deployment_process"></a>   
## Processo di distribuzione  
 Se si dispone dell'infrastruttura di supporto sul posto, è possibile usare System Center Configuration Manager 2012 per distribuire il pacchetto ridistribuibile di .NET Framework sui computer della rete.  La creazione dell'infrastruttura include la creazione e la definizione di cinque aree primarie: raccolte, un pacchetto e un programma per il software, punti di distribuzione e distribuzioni.  
  
-   **Raccolte**: rappresentano gruppi di risorse di Configuration Manager, ad esempio utenti, gruppi di utenti o computer, ai quali viene distribuito .NET Framework.  Per altre informazioni, vedere [Raccolte in Configuration Manager](http://technet.microsoft.com/library/gg682169.aspx) nella libreria della documentazione per Configuration Manager.  
  
-   **Pacchetti e programmi**: in genere rappresentano le applicazioni software da installare in un computer client, ma possono anche contenere singoli file, aggiornamenti o persino singoli comandi.  Per altre informazioni, vedere [Pacchetti e programmi in Configuration Manager](http://technet.microsoft.com/library/gg699369.aspx) nella libreria della documentazione per Configuration Manager.  
  
-   **Punti di distribuzione**: ruoli del sistema di siti di Configuration Manager nei quali sono archiviati i file richiesti per l'esecuzione del software nei computer client.  Quando il client di Configuration Manager riceve ed elabora una distribuzione software, contatta un punto di distribuzione per scaricare il contenuto associato al software e avviare il processo di installazione.  Per altre informazioni, vedere [Introduzione alla gestione dei contenuti in Configuration Manager](http://technet.microsoft.com/library/gg682083.aspx) nella libreria della documentazione per Configuration Manager.  
  
-   **Distribuzioni**: indicano ai membri validi della raccolta di destinazione specificata di installare il pacchetto.  Per altre informazioni, vedere [Come distribuire le applicazioni in Configuration Manager](http://technet.microsoft.com/library/gg682082.aspx) nella libreria della documentazione per Configuration Manager.  
  
> [!IMPORTANT]
>  Le procedure descritte in questo argomento includono impostazioni standard per creare e distribuire un pacchetto e un programma e potrebbero non illustrare tutte le impostazioni possibili.  Per altre informazioni sulle opzioni di distribuzione di Configuration Manager, vedere la [Libreria della documentazione per Configuration Manager](http://technet.microsoft.com/library/gg682041.aspx).  
  
<a name="deploying_in_a_test_environment"></a>   
## Distribuzione di .NET Framework  
 È possibile usare System Center Configuration Manager 2012 per distribuire un'installazione invisibile all'utente di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] in cui gli utenti non interagiscono con il processo di installazione.  Attenersi ai passaggi riportati di seguito.  
  
1.  [Creare una raccolta](#creating_a_collection).  
  
2.  [Creare un pacchetto e un programma per il pacchetto ridistribuibile di .NET Framework](#creating_a_package).  
  
3.  [Selezionare un punto di distribuzione](#select_dist_point).  
  
4.  [Distribuire il pacchetto](#deploying_package).  
  
<a name="creating_a_collection"></a>   
### Creare una raccolta  
 In questo passaggio selezionare i computer in cui verrà distribuito il pacchetto e il programma e raggrupparli in una raccolta dispositivi.  Per creare una raccolta in Configuration Manager, è possibile usare le regole di appartenenza dirette \(dove vengono specificati manualmente i membri della raccolta\) oppure regole di query \(dove Configuration Manager determina i membri della raccolta in base ai criteri specificati\).  Per altre informazioni sulle regole di appartenenza, incluse query e regole dirette, vedere [Introduzione alle raccolte in Configuration Manager](http://technet.microsoft.com/library/gg682177.aspx) nella libreria della documentazione per Configuration Manager.  
  
 Per creare una raccolta:  
  
1.  Nella console di Configuration Manager scegliere **Asset e conformità**.  
  
2.  Nell'area di lavoro **Asset e conformità** scegliere **Raccolte dispositivi**.  
  
3.  Nella scheda **Pagina iniziale** scegliere **Crea raccolta dispositivi** nel gruppo di **Crea**.  
  
4.  Nella pagina **Generale** della **Creazione guidata raccolta dispositivi** digitare un nome per la raccolta.  
  
5.  Scegliere **Sfoglia** per specificare una raccolta di limitazione.  
  
6.  Nella pagina **Regole di appartenenza** scegliere **Aggiungi regola**, quindi scegliere **Regola diretta** per aprire **Creazione guidata regola di appartenenza diretta**.  Scegliere **Avanti**.  
  
7.  Nella pagina **Cerca risorse** scegliere **Risorsa di sistema** nell'elenco **Classe di risorse**.  Nell'elenco **Nome attributo** scegliere **Nome**.  Nel campo **Valore** immettere `%`, quindi scegliere **Avanti**.  
  
8.  Nella pagina **Seleziona risorse** selezionare la casella di controllo per ogni computer in cui si desidera distribuire .NET Framework.  Scegliere **Avanti**, quindi completare la procedura guidata.  
  
9. Nella pagina **Regole di appartenenza** della **Creazione guidata raccolta dispositivi** scegliere **Avanti**, quindi completare la procedura guidata.  
  
 Per altre informazioni sulle raccolte, vedere [Raccolte in Configuration Manager](http://technet.microsoft.com/library/bb693730.aspx) nella libreria della documentazione per Configuration Manager.  
  
<a name="creating_a_package"></a>   
### Creare un pacchetto e un programma per il pacchetto ridistribuibile di .NET Framework  
 Nei passaggi riportati di seguito viene creato manualmente un pacchetto per il pacchetto ridistribuibile di .NET Framework.  Il pacchetto contiene i parametri specificati per l'installazione di .NET Framework e il percorso dal quale il pacchetto verrà distribuito ai computer di destinazione.  
  
 Per creare un pacchetto:  
  
1.  Nella console di Configuration Manager scegliere **Raccolta software**.  
  
2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi scegliere **Pacchetti**.  
  
3.  Nella scheda **Pagina iniziale** scegliere **Crea pacchetto** nel gruppo **Crea**.  
  
4.  Nella pagina **Pacchetto** della **Creazione guidata pacchetto e programma** immettere le informazioni riportate di seguito:  
  
    -   Nome: `.NET Framework 4.5`  
  
    -   Produttore: `Microsoft`  
  
    -   Lingua.  `Inglese (Stati Uniti)`  
  
5.  Scegliere **Questo pacchetto contiene file di origine**, quindi **Sfoglia** per selezionare la cartella locale o di rete che contiene i file di installazione di .NET Framework.  Una volta selezionata la cartella, scegliere **OK**, quindi **Avanti**.  
  
6.  Nella pagina **Tipo di programma** della procedura guidata, scegliere **Programma standard**, quindi **Avanti**.  
  
7.  Nella pagina **Programma** della **Creazione guidata pacchetto e programma** immettere le informazioni riportate di seguito:  
  
    1.  **Nome:** `.NET Framework 4.5`  
  
    2.  **Riga di comando:** `dotNetFx45_Full_x86_x64.exe /q /norestart /ChainingPackage ADMINDEPLOYMENT` \(le opzioni della riga di comando sono descritte nella tabella dopo questi passaggi\)  
  
    3.  **Esegui:** scegliere **Nascosto**.  
  
    4.  **Requisiti per esecuzione programma:** scegliere l'opzione che specifica che il programma può essere eseguito indipendentemente dal fatto che un utente sia connesso.  
  
8.  Nella pagina **Requisiti** scegliere **Avanti** per accettare i valori predefiniti, quindi completare la procedura guidata.  
  
 Nella tabella seguente vengono descritte le opzioni della riga di comando specificate nel passaggio 7.  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/q**|Imposta la modalità non interattiva.  Nessun input utente viene richiesto e nessun output viene visualizzato.|  
|**\/norestart**|Impedisce il riavvio automatico del programma di installazione.  Se si usa questa opzione, il riavvio del computer deve essere gestito da Configuration Manager.|  
|**\/chainingpackage** *PackageName*|Specifica il nome del pacchetto che esegue il concatenamento.  Questa informazione viene riportata insieme alle altre informazioni sulla sessione di installazione per gli utenti che hanno eseguito la registrazione al programma [Analisi utilizzo software](http://go.microsoft.com/fwlink/p/?LinkId=248244).  Se il nome del pacchetto include spazi, usare le virgolette doppie come delimitatori, ad esempio: **\/chainingpackage "Chaining Product"**.|  
  
 Questi passaggi creano un pacchetto denominato .NET Framework 4.5.  Viene distribuita automaticamente un'installazione invisibile all'utente di .NET Framework 4.5.  In un'installazione invisibile all'utente, gli utenti non interagiscono con il processo d'installazione e l'applicazione di concatenamento deve acquisire il codice restituito e gestire il riavvio; vedere la pagina in cui è descritto come [Ottenere informazioni sullo stato di avanzamento da un pacchetto d'installazione](http://go.microsoft.com/fwlink/?LinkId=179606) nella libreria MSDN.  
  
<a name="select_dist_point"></a>   
### Selezionare un punto di distribuzione  
 Per distribuire il pacchetto e il programma da un server ai computer client, è innanzitutto necessario specificare un sistema di siti come punto di distribuzione e distribuire il pacchetto al punto di distribuzione.  
  
 Usare i passaggi seguenti per selezionare un punto di distribuzione per il pacchetto di .NET Framework 4.5 creato nella sezione precedente:  
  
1.  Nella console di Configuration Manager scegliere **Raccolta software**.  
  
2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi scegliere **Pacchetti**.  
  
3.  Dall'elenco di pacchetti, selezionare il pacchetto **.NET Framework 4.5** creato nella sezione precedente.  
  
4.  Nella scheda **Pagina iniziale** scegliere **Distribuisci contenuto** nel gruppo **Distribuzione**.  
  
5.  Nella scheda **Generale** della **Distribuzione guidata contenuto** scegliere **Avanti**.  
  
6.  Nella pagina **Destinazione contenuto** della procedura guidata scegliere **Aggiungi**, quindi **Punto di distribuzione**.  
  
7.  Nella finestra di dialogo **Aggiungi punti di distribuzione** selezionare i punti di distribuzione che ospiteranno il pacchetto e il programma, quindi scegliere **OK**.  
  
8.  Completare la procedura guidata.  
  
 Il pacchetto contiene tutte le informazioni necessarie per distribuire automaticamente .NET Framework 4.5.  Prima di distribuire il pacchetto e il programma, verificare che sia installato nel punto di distribuzione. Vedere la sezione "Monitoraggio del contenuto" nella pagina [Operazioni e manutenzione per la gestione dei contenuti in Configuration Manager](http://technet.microsoft.com/library/gg712694.aspx#BKMK_MonitorContent) nella libreria della documentazione per Configuration Manager.  
  
<a name="deploying_package"></a>   
### Distribuire il pacchetto  
 Per distribuire il pacchetto e il programma di .NET Framework 4.5:  
  
1.  Nella console di Configuration Manager scegliere **Raccolta software**.  
  
2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi scegliere **Pacchetti**.  
  
3.  Dall'elenco di pacchetti selezionare il pacchetto creato e denominato **.NET Framework 4.5**.  
  
4.  Nella scheda **Pagina iniziale** scegliere **Distribuisci** nel gruppo **Distribuzione**.  
  
5.  Nella pagina di **Generale** della **Distribuzione guidata del software** scegliere **Sfoglia**, quindi selezionare la raccolta creata precedentemente.  Scegliere **Avanti**.  
  
6.  Nella pagina **Contenuto** della procedura guidata, verificare che il punto da cui si desidera distribuire il software sia visualizzato, quindi scegliere **Avanti**.  
  
7.  Nella pagina **Impostazioni di distribuzione** della procedura guidata, verificare che **Azione** sia impostato su **Installa** e **Scopo** su **Obbligatorio**.  Ciò garantisce che l'installazione del pacchetto software sarà obbligatoria sui computer di destinazione.  Scegliere **Avanti**.  
  
8.  Nella pagina **Pianificazione** della procedura guidata specificare quando si desidera installare .NET Framework.  È possibile scegliere **Nuovo** per assegnare una fase di installazione o specificare che il software dovrà essere installato quando l'utente accede o si disconnette o non appena possibile.  Scegliere **Avanti**.  
  
9. Nella pagina di **Esperienza utente** della procedura guidata, usare i valori predefiniti e scegliere **Avanti**.  
  
    > [!WARNING]
    >  Nell'ambiente di produzione potrebbero essere impostati criteri che richiedono selezioni diverse per la pianificazione dell'assegnazione.  Per informazioni su queste opzioni, vedere [Proprietà dei nomi degli annunci: scheda Pianificazione](http://technet.microsoft.com/library/bb694016.aspx) nella libreria TechNet.  
  
10. Nella pagina di **Punti di distribuzione** della procedura guidata usare i valori predefiniti e scegliere **Avanti**.  
  
11. Completare la procedura guidata.  È possibile monitorare lo stato di avanzamento della distribuzione nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**.  
  
 Il pacchetto verrà ora distribuito alla raccolta di destinazione e l'installazione invisibile all'utente di .NET Framework 4.5 avrà inizio.  Per informazioni sui codici di errore di installazione di .NET Framework 4.5, vedere la sezione [Codici restituiti](#return_codes) più avanti in questo argomento.  
  
<a name="resources"></a>   
## Risorse  
 Per altre informazioni riguardanti l'infrastruttura per testare la distribuzione del pacchetto ridistribuibile di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], vedere le risorse seguenti.  
  
 **Active Directory, DNS, DHCP:**  
  
-   [Servizi di dominio Active Directory per Windows Server 2008](http://technet.microsoft.com/library/dd378891.aspx)  
  
-   [Guida dettagliata di Windows Server 2008 per DNS in piccole reti](http://www.microsoft.com/download/details.aspx?id=17157)  
  
-   [Server DNS](http://technet.microsoft.com/library/cc732997.aspx)  
  
-   [Server DHCP](http://technet.microsoft.com/library/cc896553.aspx)  
  
 **SQL Server 2008:**  
  
-   [Installazione di SQL Server 2008 \(video di SQL Server\)](http://technet.microsoft.com/library/dd299415.aspx)  
  
-   [Panoramica della sicurezza di SQL Server 2008 per gli amministratori di database](http://download.microsoft.com/download/a/c/d/acd8e043-d69b-4f09-bc9e-4168b65aaa71/SQL2008SecurityOverviewforAdmins.docx)  
  
 **System Center Configuration Manager 2012 \(punto di gestione, punto di distribuzione\):**  
  
-   [Amministrazione dei siti con System Center 2012 Configuration Manager](http://technet.microsoft.com/library/gg681983.aspx)  
  
-   [Pianificazione e distribuzione del sito singolo di Gestione configurazione](http://technet.microsoft.com/library/bb680961.aspx)  
  
 **Client System Center Configuration Manager 2012 per computer Windows:**  
  
-   [Distribuzione dei client per System Center 2012 Configuration Manager](http://technet.microsoft.com/library/gg699391.aspx)  
  
<a name="troubleshooting"></a>   
## Risoluzione dei problemi  
  
### Percorsi dei file di log  
 Durante l'installazione di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] vengono generati i seguenti file di log:  
  
 %temp%\\Microsoft .NET Framework 4.5\*.txt                                 
 %temp%\\Microsoft .NET Framework 4.5\*.html  
  
 È possibile usare lo [strumento di raccolta dei log](http://www.microsoft.com/download/details.aspx?id=12493) per raccogliere i file di log di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e creare un file di archivio \(.cab\) compresso che riduce le dimensioni dei file.  
  
<a name="return_codes"></a>   
### Codici restituiti  
 Nella tabella seguente vengono elencati i codici più comuni restituiti dal programma di installazione ridistribuibile di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  I codici restituiti sono gli stessi per tutte le versioni del programma di installazione.  
  
 Per collegamenti a informazioni dettagliate, vedere la sezione successiva, [Scaricare i codici di errore](#additional_error_codes).  
  
|Codice restituito|Descrizione|  
|-----------------------|-----------------|  
|0|Installazione completata.|  
|1602|Installazione annullata dall'utente.|  
|1603|Errore irreversibile durante l'installazione.|  
|1641|Riavvio necessario per completare l'installazione.  Questo messaggio indica l'esito positivo dell'operazione.|  
|3010|Riavvio necessario per completare l'installazione.  Questo messaggio indica l'esito positivo dell'operazione.|  
|5100|Il computer dell'utente non soddisfa i requisiti di sistema.|  
  
<a name="additional_error_codes"></a>   
### Scaricare i codici di errore  
  
-   [Codici di errore del Servizio trasferimento intelligente in background \(BITS\)](http://msdn.microsoft.com/library/aa362823.aspx)  
  
-   [Codici di errore del moniker URL](http://msdn.microsoft.com/library/ms775145.aspx)  
  
-   [Codici di errore WinHttp](http://msdn.microsoft.com/library/aa383770.aspx)  
  
 Altri codici di errore:  
  
-   [Codici di errore di Windows Installer](http://msdn.microsoft.com/library/aa368542.aspx)  
  
-   [Codici di risultato dell'Agente di Windows Update](http://technet.microsoft.com/library/cc720442.aspx)  
  
## Vedere anche  
 [Guida alla distribuzione per gli sviluppatori](../../../docs/framework/deployment/deployment-guide-for-developers.md)   
 [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md)