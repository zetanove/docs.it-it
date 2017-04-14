---
title: "How to: Validate Application Settings | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "validating application settings"
  - "application settings, Windows Forms"
  - "application settings, validating"
ms.assetid: 9f145ada-4267-436a-aa4c-c4dcffd0afb7
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# How to: Validate Application Settings
In questo argomento viene spiegato come convalidare le impostazioni dell'applicazione prima dell'operazione che le rende persistenti.  
  
 Poiché le impostazioni dell'applicazione sono fortemente tipizzate, esiste un buon margine di certezza che non sia possibile per gli utenti assegnare dati del tipo errato a una determinata impostazione.  È tuttavia sempre possibile che si tenti di assegnare un valore che non rientra nei limiti accettabili, ad esempio una data di nascita nel futuro.  La classe <xref:System.Configuration.ApplicationSettingsBase>, classe padre di tutte le classi delle impostazioni dell'applicazione, espone quattro eventi per il controllo di tali limiti.  La gestione di tali eventi consente di inserire tutto il codice di convalida in un'unica posizione invece di distribuirlo in tutto il progetto.  
  
 L'evento da utilizzare dipende dal momento in cui è necessario convalidare le impostazioni, come descritto nella tabella riportata di seguito.  
  
|Evento|Occorrenza e utilizzo|  
|------------|---------------------------|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingsLoaded>|Si verifica dopo il caricamento iniziale di un gruppo di proprietà delle impostazioni.<br /><br /> Utilizzare l'evento per convalidare i valori iniziali dell'intero gruppo di proprietà prima che vengano utilizzati nell'applicazione.|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingChanging>|Si verifica prima che il valore di una singola proprietà di impostazioni venga modificato.<br /><br /> Utilizzare l'evento per convalidare una singola proprietà prima che venga modificata.  Fornisce riscontro immediato agli utenti relativamente ad azioni e scelte effettuate.|  
|<xref:System.Configuration.ApplicationSettingsBase.PropertyChanged>|Si verifica dopo che il valore di una singola proprietà di impostazioni venga modificato.<br /><br /> Utilizzare l'evento per convalidare una singola proprietà dopo la modifica.  L'evento è utilizzato di rado per la convalida, a meno che non sia necessario un processo di convalida asincrono di lunga durata.|  
|<xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>|Si verifica prima dell'archiviazione del gruppo di proprietà delle impostazioni.<br /><br /> Utilizzare l'evento per convalidare i valori dell'intero gruppo di proprietà prima che vengano resi persistenti su disco.|  
  
 Normalmente non si utilizzano tutti gli eventi sopra indicati nella stessa applicazione a fini di convalida.  Spesso, ad esempio, è possibile soddisfare tutti i requisiti di convalida gestendo solo l'evento <xref:System.Configuration.ApplicationSettingsBase.SettingChanging>.  
  
 Un gestore eventi esegue in genere una delle azioni seguenti quando rileva un valore non valido:  
  
-   Fornisce automaticamente un valore sicuramente corretto, ad esempio quello predefinito.  
  
-   Chiede informazioni all'utente del codice server.  
  
-   Per gli eventi generati prima delle azioni associate, quali <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> e <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>, utilizza l'argomento <xref:System.ComponentModel.CancelEventArgs> per annullare l'operazione.  
  
 Per ulteriori informazioni sulla gestione degli eventi, vedere [Event Handlers Overview](../../../../docs/framework/winforms/event-handlers-overview-windows-forms.md).  
  
 Nelle procedure riportate di seguito viene illustrato come verificare la validità di una data di nascita con l'evento <xref:System.Configuration.ApplicationSettingsBase.SettingChanging> o <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>.  Le procedure presuppongono che le impostazioni dell'applicazione siano già state create. Nell'esempio vengono eseguiti controlli dei limiti relativamente all'impostazione denominata `DateOfBirth`.  Per ulteriori informazioni sulla creazione di impostazioni, vedere [How to: Create Application Settings](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md).  
  
### Per ottenere l'oggetto delle impostazioni dell'applicazione  
  
-   Ottenere un riferimento all'oggetto delle impostazioni dell'applicazione \(l'istanza wrapper\) eseguendo una delle operazioni seguenti:  
  
    -   Se le impostazioni sono state create con la finestra di dialogo Impostazioni applicazione di Visual Studio nella **finestra delle proprietà**, recuperare l'oggetto delle impostazioni predefinito generato per il linguaggio utilizzato mediante l'espressione seguente.  
  
        ```csharp  
        Configuration.Settings.Default   
        ```  
  
        ```vb  
        MySettings.Default   
        ```  
  
         In alternativa  
  
    -   Se è stato utilizzato Visual Basic e le impostazioni dell'applicazione sono state create con Progettazione progetti, recuperare le impostazioni utilizzando l'oggetto [Oggetto My.Settings](../../../../ocs/visual-basic/language-reference/objects/my-settings-object.md).  
  
         In alternativa  
  
    -   Se le impostazioni sono state create mediante derivazione diretta dalla classe <xref:System.Configuration.ApplicationSettingsBase>, è necessario creare manualmente un'istanza della classe.  
  
        ```csharp  
        MyCustomSettings settings = new MyCustomSettings();  
        ```  
  
        ```vb  
        Dim Settings as New MyCustomSettings()  
        ```  
  
 Le procedure seguenti presuppongono che l'oggetto delle impostazioni dell'applicazione sia stato ottenuto completando l'ultima operazione in questa procedura.  
  
### Per convalidare impostazioni dell'applicazione quando un'impostazione subisce una modifica  
  
1.  Se si utilizza C\#, nel form o nell'evento `Load` del controllo aggiungere un gestore eventi per l'evento <xref:System.Configuration.ApplicationSettingsBase.SettingChanging>.  
  
     In alternativa  
  
     Se si utilizza Visual Basic, dichiarare la variabile `Settings` con la parola chiave `WithEvents`.  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        settings.SettingChanging += new SettingChangingEventHandler(MyCustomSettings_SettingChanging);  
    }  
    ```  
  
    ```vb  
    Public Sub Form1_Load(sender as Object, e as EventArgs)  
        AddHandler settings.SettingChanging, AddressOf MyCustomSettings_SettingChanging  
    End Sub   
    ```  
  
2.  Definire il gestore eventi e scrivere al suo interno il codice per eseguire la verifica dei limiti sulla data di nascita.  
  
    ```csharp  
    private void MyCustomSettings_SettingChanging(Object sender, SettingChangingEventArgs e)  
    {  
        if (e.SettingName.Equals("DateOfBirth")) {  
            Date newDate = (Date)e.NewValue;  
            If (newDate > Date.Now) {  
                e.Cancel = true;  
                // Inform the user.  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub MyCustomSettings_SettingChanging(sender as Object, e as SettingChangingEventArgs) Handles Settings.SettingChanging  
        If (e.SettingName.Equals("DateOfBirth")) Then  
            Dim NewDate as Date = CType(e.NewValue, Date)  
            If (NewDate > Date.Now) Then  
                e.Cancel = True  
                ' Inform the user.  
            End If  
        End If  
    End Sub  
    ```  
  
### Per convalidare impostazioni dell'applicazione quando si verifica un salvataggio  
  
1.  Nel form o nell'evento  `Load` del controllo aggiungere un gestore eventi per l'evento <xref:System.Configuration.ApplicationSettingsBase.SettingsSaving>.  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        settings.SettingsSaving += new SettingsSavingEventHandler(MyCustomSettings_SettingsSaving);  
    }  
    ```  
  
    ```vb  
    Public Sub Form1_Load(Sender as Object, e as EventArgs)  
        AddHandler settings.SettingsSaving, AddressOf MyCustomSettings_SettingsSaving  
    End Sub  
    ```  
  
2.  Definire il gestore eventi e scrivere al suo interno il codice per eseguire la verifica dei limiti sulla data di nascita.  
  
    ```csharp  
    private void MyCustomSettings_SettingsSaving(Object sender, SettingsSavingEventArgs e)  
    {  
        if (this["DateOfBirth"] > Date.Now) {  
            e.Cancel = true;  
        }  
    }  
    ```  
  
    ```vb  
    Private Sub MyCustomSettings_SettingsSaving(Sender as Object, e as SettingsSavingEventArgs)  
        If (Me["DateOfBirth"] > Date.Now) Then  
            e.Cancel = True  
        End If  
    End Sub  
    ```  
  
## Vedere anche  
 [Creating Event Handlers in Windows Forms](../../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [How to: Create Application Settings](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)