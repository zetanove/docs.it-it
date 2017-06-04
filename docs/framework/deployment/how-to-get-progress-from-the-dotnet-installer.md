---
title: "Procedura: ottenere lo stato di avanzamento dal programma d&#39;installazione di .NET Framework 4.5 | Microsoft Docs"
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
  - ".NET Framework, installazione"
  - "informazioni sullo stato, programma di installazione di .NET Framework"
ms.assetid: 0a1a3ba3-7e46-4df2-afd3-f3a8237e1c4f
caps.latest.revision: 30
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 30
---
# Procedura: ottenere lo stato di avanzamento dal programma d&#39;installazione di .NET Framework 4.5
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] è un runtime ridistribuibile.  Se si sviluppano applicazioni per questa versione di .NET Framework, è possibile includere \(a catena\) l'installazione di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] come un componente prerequisito nell'impostazione dell'applicazione.  Per offrire un'esperienza d'installazione personalizzata o unificata, si consiglia di avviare l'installazione di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] in modo invisibile all'utente, tenendone traccia visualizzando lo stato di avanzamento dell'installazione.  Per abilitare la gestione invisibile, l'impostazione [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] \(che può essere controllata\) definisce un protocollo, utilizzando un segmento mappato in memoria di I\/O \(MMIO\) per comunicare con l'installazione \(osservatore o concatenatore\).  Questo protocollo definisce una modalità per il concatenatore per ottenere lo stato di avanzamento, i risultati dettagliati, per rispondere a i messaggi e per annullare l'installazione di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  
  
-   **Chiamata**.  Per chiamare il processo di installazione [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] e ricevere informazioni sullo stato di avanzamento della sezione MMIO, il programma di installazione deve eseguire le operazioni seguenti:  
  
    1.  Chiamare [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] programma ridistribuibile:  
  
        ```  
        dotNetFx45_Full_x86_x64.exe /q /norestart /pipe section-name  
        ```  
  
         dove *section name* è il nome che si desidera utilizzare per identificare l'applicazione. l'installazione di .NET Framework, legge e scrive in modo asincrono nella sezione MIMO, quindi potrebbe essere utile usare eventi e messaggi in quell'intervallo di tempo.  Nell'esempio, il processo di installazione di .NET Framework viene creato da un costruttore che alloca la sezione MMIO \(`TheSectionName`\) e definisce un evento \(`TheEventName`\):  
  
        ```  
        Server():ChainerSample::MmioChainer(L"TheSectionName", L"TheEventName")  
        ```  
  
         Sostituire tali nomi con quelli univoci per il programma di installazione.  
  
    2.  Leggere dalla sezione MMIO.  In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], le operazioni di download e installazione sono simultanee: una parte di .NET Framework potrebbe stare installando mentre un'altra sta scaricando.  Di conseguenza, lo stato di avanzamento viene restituito \(ovvero, scritto\) alla sezione MMIO come due numeri \(`m_downloadSoFar` e `m_installSoFar`\)crescenti da 0 a 255.  Quando viene scritto 255 e .NET Framework esce, l'installazione è completa.  
  
-   **Codici di uscita**.  I seguenti codici di uscita dal comando, per il richiamo del programma ridistribuibile [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], indicano se l'installazione è riuscita o meno:  
  
    -   0 \- Installazione completata correttamente.  
  
    -   3010 \- Installazione completata; il riavvio del sistema è obbligatorio.  
  
    -   1602 – L'installazione è stata annullata.  
  
    -   Tutti gli altri codici \- L'installazione ha rilevato errori; per ulteriori dettagli, esaminare i file di log creati in% temp%.  
  
-   **Annulla installazione**.  È possibile annullare l'installazione in qualsiasi momento tramite il metodo `Abort` per impostare i flag `m_downloadAbort` e `m_ installAbort` nella sezione MMIO.  
  
## Esempio di concatenatore  
 L'esempio di Concatenatore lanciato in automatico, traccia l'istallazione di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] mentre visualizza lo stato di avanzamento.  L'esempio è analogo a quello del Concatenatore previsto da .NET Framework 4.  Tuttavia, in aggiunta, si può evitare il riavvio del sistema elaborando una finestra di messaggio per chiudere le applicazioni .NET Framework 4.  Per informazioni sulla finestra di messaggio, vedere [Riduzione dei riavvii del sistema durante le installazioni di .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md).  L'esempio può essere utilizzato con il programma di installazione di .NET Framework 4; in tale scenario, il messaggio non viene inviato semplicemente.  
  
> [!WARNING]
>  È necessario eseguire l'esempio come amministratore.  
  
 È possibile scaricare la soluzione Visual Studio completa per [Esempio di Concatenatore .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=231345) dalla raccolta di Esempi di MSDN.  
  
 Nelle sezioni seguenti vengono descritti i file significativi per questo esempio: MMIOChainer.h, ChainingdotNet4.cpp e IProgressObserver.h.  
  
#### MmIoChainer.h  
  
-   Il file MMIOChainer.h \(vedere [codice completo](http://go.microsoft.com/fwlink/?LinkId=231369)\)contiene la definizione della struttura dati e la classe di base dalla quale deve essere derivata la classe del concatenatore.  Il [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] estende la struttura dati di MMIO, per gestire tali dati si necessita del programma di installazione [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Le modifiche alla struttura MMIO sono compatibili con versioni precedenti, come i concatenatori di .NET Framework 4 possono funzionare con installato .NET Framework 4.5, senza richiedere la ricompilazione.  Tuttavia, questo scenario non supporta la funzionalità per ridurre il numero di riavvii del sistema.  
  
     Il campo della versione consente di identificare le revisioni alla struttura e al formato di messaggi.  L'installazione di .NET Framework determina la versione dell'interfaccia del concatenatore, chiamando la funzione `VirtualQuery`, che determinare la dimensione del file di mapping.  Se la dimensione è abbastanza grande per contenere il campo della versione, l'installazione di .NET Framework utilizza il valore specificato.  Se il file di mapping è troppo piccolo per contenere il campo della versione, come avviene nel caso di .NET Framework 4, il processo di installazione assume che la versione sia la 0 \(4\).  Se il concatenatore non supporta la versione del messaggio che l'installazione di .NET Framework desidera inviare, si presuppone che l'installazione di .NET Framework ignori la risposta.  
  
     La struttura dei dati MMIO è definita come segue.  
  
    ```cpp  
    // MMIO data structure for interprocess communication  
        struct MmioDataStructure  
        {  
            bool m_downloadFinished;               // Is download complete?  
            bool m_installFinished;                // Is installation complete?  
            bool m_downloadAbort;                  // Set to cause downloader to abort.  
            bool m_installAbort;                   // Set to cause installer to abort.  
            HRESULT m_hrDownloadFinished;          // Resulting HRESULT for download.  
            HRESULT m_hrInstallFinished;           // Resulting HRESULT for installation.  
            HRESULT m_hrInternalError;  
            WCHAR m_szCurrentItemStep[MAX_PATH];  
            unsigned char m_downloadSoFar;         // Download progress 0-255 (0-100% done).   
            unsigned char m_installSoFar;          // Installation progress 0-255 (0-100% done).  
            WCHAR m_szEventName[MAX_PATH];         // Event that chainer creates and chainee opens to sync communications.  
  
            BYTE m_version;                        // Version of the data structure, set by chainer:  
                                                   // 0x0: .NET Framework 4   
                                                   // 0x1: .NET Framework 4.5  
  
            DWORD m_messageCode;                   // Current message sent by the chainee; 0 if no message is active.  
            DWORD m_messageResponse;               // Chainer's response to current message; 0 if not yet handled.  
            DWORD m_messageDataLength;             // Length of the m_messageData field, in bytes.  
            BYTE m_messageData[1];                 // Variable-length buffer; content depends on m_messageCode.  
        };  
  
    ```  
  
-   La struttura dei dati `MmioDataStructure` non deve essere utilizzata direttamente; invece utilizzare la classe `MmioChainer` per implementare il concatenatore.  Derivano dalla classe `MmioChainer` per concatenare [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] ridistribuibile.  
  
#### IprogressObserver.h  
  
-   Il file IProgressObserver.h implementa un osservatore di stato di avanzamento \([vedere il codice completo](http://go.microsoft.com/fwlink/?LinkId=231370)\).  Questo osservatore riceve notifica dello stato di avanzamento di download e installazione \(specificato come un unsigned `char` 0\-255, indicando 1%\-100% operazione completata\).  L'osservatore è inoltre notificato, quando l'elemento concatenato invia un messaggio l'osservatore deve inviare una risposta.  
  
    ```cpp  
        class IProgressObserver  
        {  
        public:  
            virtual void OnProgress(unsigned char) = 0; // 0 - 255:  255 == 100%  
            virtual void Finished(HRESULT) = 0;         // Called when operation is complete    
            virtual DWORD Send(DWORD dwMessage, LPVOID pData, DWORD dwDataLength) = 0; // Called when a message is sent  
        };  
  
    ```  
  
#### ChainingdotNet4.cpp  
  
-   Il file [ChainingdotNet4.5.cpp](http://go.microsoft.com/fwlink/?LinkId=231368) implementa la classe `Server`, derivata dalla classe `MmioChainer` ed esegue l'override dei metodi appropriati per visualizzare le informazioni di progresso.  Il MmioChainer crea una sezione con il nome specificato ed inizializza il concatenatore con il nome dell'evento specificato.  Il nome dell'evento viene salvato nella struttura dei dati mappata.  È necessario rendere la sezione e i nomi degli eventi univoci.  La classe `Server` nel codice seguente avvia il programma di installazione specificato, monitora lo stato di avanzamento e restituisce un codice di uscita.  
  
    ```cpp  
    class Server : public ChainerSample::MmioChainer, public ChainerSample::IProgressObserver  
    {  
    public:  
        …………….  
        Server():ChainerSample::MmioChainer(L"TheSectionName", L"TheEventName") //customize for your event names  
        {}  
  
    ```  
  
     L'installazione è avviata dal metodo principale.  
  
    ```cpp  
    // Main entry point for program  
    int __cdecl main(int argc, _In_count_(argc) char **_argv)  
    {  
        int result = 0;  
        CString args;  
        if (argc > 1)  
        {  
            args = CString(_argv[1]);  
        }  
  
        if (IsNetFx4Present(NETFX45_RC_REVISION))  
        {  
            printf(".NET Framework 4.5 is already installed");  
        }  
        else  
        {  
            result = Server().Launch(args);  
        }  
  
        return result;  
    }  
  
    ```  
  
-   Prima di avviare l'installazione, il concatenatore per verificare se [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] è già installato chiamando `IsNetFx4Present`:  
  
    ```cpp  
    ///  Checks for presence of the .NET Framework 4.  
    ///    A value of 0 for dwMinimumRelease indicates a check for the .NET Framework 4 full  
    ///    Any other value indicates a check for a specific compatible release of the .NET Framework 4.  
    #define NETFX40_FULL_REVISION 0  
    // TODO: Replace with released revision number  
    #define NETFX45_RC_REVISION MAKELONG(50309, 5)   // .NET Framework 4.5   
    bool IsNetFx4Present(DWORD dwMinimumRelease)  
    {  
        DWORD dwError = ERROR_SUCCESS;  
        HKEY hKey = NULL;  
        DWORD dwData = 0;  
        DWORD dwType = 0;  
        DWORD dwSize = sizeof(dwData);  
  
        dwError = ::RegOpenKeyExW(HKEY_LOCAL_MACHINE, L"SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full", 0, KEY_READ, &hKey);  
        if (ERROR_SUCCESS == dwError)  
        {  
            dwError = ::RegQueryValueExW(hKey, L"Release", 0, &dwType, (LPBYTE)&dwData, &dwSize);  
  
            if ((ERROR_SUCCESS == dwError) && (REG_DWORD != dwType))  
            {  
                dwError = ERROR_INVALID_DATA;  
            }  
            else if (ERROR_FILE_NOT_FOUND == dwError)  
            {  
                // Release value was not found, let's check for 4.0.  
                dwError = ::RegQueryValueExW(hKey, L"Install", 0, &dwType, (LPBYTE)&dwData, &dwSize);  
  
                // Install = (REG_DWORD)1;  
                if ((ERROR_SUCCESS == dwError) && (REG_DWORD == dwType) && (dwData == 1))  
                {  
                    // treat 4.0 as Release = 0  
                    dwData = 0;  
                }  
                else  
                {  
                    dwError = ERROR_INVALID_DATA;  
                }  
            }  
        }  
  
        if (hKey != NULL)  
        {  
            ::RegCloseKey(hKey);  
        }  
  
        return ((ERROR_SUCCESS == dwError) && (dwData >= dwMinimumRelease));  
    }  
  
    ```  
  
-   È possibile modificare il percorso del file eseguibile \(Setup.exe, nell'esempio\) con il metodo `Launch` per indicare la posizione corretta, o determinare la posizione personalizzando il codice.  La classe base `MmioChainer` fornisce un metodo bloccante `Run()` che la classe derivata chiama.  
  
    ```cpp  
  
    bool Launch(const CString& args)  
    {  
    CString cmdline = L"dotNetFx45_Full_x86_x64.exe -pipe TheSectionName " + args; // Customize with name and location of setup .exe that you want to run  
    STARTUPINFO si = {0};  
    si.cb = sizeof(si);  
    PROCESS_INFORMATION pi = {0};  
  
    // Launch the Setup.exe that installs the .NET Framework 4.5  
    BOOL bLaunchedSetup = ::CreateProcess(NULL,   
     cmdline.GetBuffer(),  
     NULL, NULL, FALSE, 0, NULL, NULL,   
     &si,  
     &pi);  
  
    // If successful   
    if (bLaunchedSetup != 0)  
    {  
    IProgressObserver& observer = dynamic_cast<IProgressObserver&>(*this);  
    Run(pi.hProcess, observer);  
  
    ……………………..   
    return (bLaunchedSetup != 0);  
    }  
  
    ```  
  
-   Il metodo `Send` intercetta e elabora i messaggi.  In questa versione di .NET Framework, l'unico messaggio supportato è il messaggio di chiusura dell'applicazione.  
  
    ```cpp  
            // SendMessage  
            //  
            // Send a message and wait for the response.  
            // dwMessage: Message to send  
            // pData: The buffer to copy the data to  
            // dwDataLength: Initially a pointer to the size of pBuffer.  Upon successful call, the number of bytes copied to pBuffer.  
            //--------------------------------------------------------------  
        virtual DWORD Send(DWORD dwMessage, LPVOID pData, DWORD dwDataLength)  
        {  
            DWORD dwResult = 0;  
            printf("recieved message: %d\n", dwMessage);  
            // Handle message  
            switch (dwMessage)  
            {  
            case MMIO_CLOSE_APPS:  
                {  
                    printf("    applications are holding files in use:\n");  
                    IronMan::MmioCloseApplications* applications = reinterpret_cast<IronMan::MmioCloseApplications*>(pData);  
                    for(DWORD i = 0; i < applications->m_dwApplicationsSize; i++)  
                    {  
                        printf("      %ls (%d)\n", applications->m_applications[i].m_szName, applications->m_applications[i].m_dwPid);  
                    }  
  
                    printf("    should appliations be closed? (Y)es, (N)o, (R)efresh : ");  
                    while (dwResult == 0)  
                    {  
                        switch (toupper(getwchar()))  
                        {  
                        case 'Y':  
                            dwResult = IDYES;  // Close apps  
                            break;  
                        case 'N':  
                            dwResult = IDNO;  
                            break;  
                        case 'R':  
                            dwResult = IDRETRY;  
                            break;  
                        }  
                    }  
                    printf("\n");  
                    break;  
                }  
            default:  
                break;  
            }  
            printf("  response: %d\n  ", dwResult);  
            return dwResult;  
        }  
    };  
  
    ```  
  
-   Lo stato di avanzamento è unsigned `char` compreso tra 0 \(0%\) e 255 \(100%\).  
  
    ```cpp  
    private: // IProgressObserver  
        virtual void OnProgress(unsigned char ubProgressSoFar)  
        {…………  
       }  
  
    ```  
  
-   L'HRESULT viene passato al metodo `Finished`.  
  
    ```cpp  
    virtual void Finished(HRESULT hr)  
    {  
    // This HRESULT is communicated over MMIO and may be different than process  
    // Exit code of the Chainee Setup.exe itself  
    printf("\r\nFinished HRESULT: 0x%08X\r\n", hr);  
    }  
  
    ```  
  
    > [!IMPORTANT]
    >  [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] ridistribuibile in genere scrive molti messaggi dello stato di avanzamento e un messaggio singolo che indica il completamento \(dal lato del concatenatore\).  Legge anche in modo asincrono, cercando record `Abort`.  Se viene ricevuto un record `Abort`, annulla l'installazione e scrive un record finale con E\_ABORT, si comporta allo stesso modo con i dati in seguito all'interruzione di un'installazione e viene fatto il rollback delle operazioni di impostazione.  
  
 Un server tipico crea casualmente un nome del file MMIO, crea il file \(come mostrato nell'esempio di codice precedente `Server::CreateSection`\), e avvia il codice ridistribuibile tramite il metodo `CreateProcess` passando il nome della pipe con l'opzione `-pipe someFileSectionName`.  Il server deve implementare `OnProgress`, `Send`e i metodi `Finished` con il codice specifico dall'interfaccia utente di un'applicazione.  
  
## Vedere anche  
 [Guida alla distribuzione per gli sviluppatori](../../../docs/framework/deployment/deployment-guide-for-developers.md)   
 [Distribuzione](../../../docs/framework/deployment/net-framework-and-applications.md)