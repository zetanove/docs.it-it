---
title: "More Secure File and Data Access in Windows Forms | Microsoft Docs"
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
  - "security [Windows Forms], file access"
  - "registry [Windows Forms]"
  - "data access [Windows Forms]"
  - "database access (Windows Forms security)"
  - "data [Windows Forms], secure access"
  - "file access [Windows Forms]"
  - "security [Windows Forms], data access"
ms.assetid: 3cd3e55b-2f5e-40dd-835d-f50f7ce08967
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# More Secure File and Data Access in Windows Forms
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] usa le autorizzazioni per proteggere le risorse e i dati.  Il fatto che l'applicazione possa leggere o scrivere dati dipende dalle autorizzazioni concesse all'applicazione.  Quando l'applicazione viene eseguita in un ambiente parzialmente attendibile, è possibile che non si riesca ad accedere ai dati oppure potrebbe essere necessario modificare la modalità di accesso ai dati.  
  
 Quando si rileva una restrizione di sicurezza, sono disponibili due opzioni: dichiarare l'autorizzazione \(supponendo che sia stata concessa all'applicazione\) o usare una versione della funzionalità scritta per operare in caso di attendibilità parziale.  Le sezioni seguenti illustrano come usare il file, il database e l'accesso al Registro di sistema da applicazioni in esecuzione in un ambiente parzialmente attendibile.  
  
> [!NOTE]
>  Per impostazione predefinita, gli strumenti che generano distribuzioni [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] configurano queste distribuzioni in modo che richiedano l'attendibilità totale ai computer su cui sono in esecuzione.  Se si desiderano i vantaggi in termini di sicurezza derivanti dall'esecuzione con l'attendibilità parziale, è necessario cambiare questa impostazione predefinita in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o in uno degli strumenti di [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] \(Mage.exe o MageUI.exe\).  Per altre informazioni sulla sicurezza di Windows Form e su come determinare il livello di attendibilità appropriato per l'applicazione, vedere [Security in Windows Forms Overview](../../../docs/framework/winforms/security-in-windows-forms-overview.md).  
  
## Accesso ai file  
 La classe <xref:System.Security.Permissions.FileIOPermission> controlla l'accesso a file e cartelle in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  Per impostazione predefinita, il sistema di sicurezza non concede <xref:System.Security.Permissions.FileIOPermission> agli ambienti con attendibilità parziale, ad esempio la Intranet locale e le aree Internet.  Un'applicazione che richiede l'accesso ai file può comunque funzionare in questi ambienti se si modifica la progettazione dell'applicazione o si usano metodi diversi per accedere ai file.  Per impostazione predefinita, all'area Intranet locale viene concesso il diritto di accesso agli stessi siti e alle stesse directory, di riconnettersi al sito di origine e di leggere dalla directory di installazione.  Per impostazione predefinita, all'area Internet è concesso solo il diritto di riconnettersi al sito di origine.  
  
### File specificati dall'utente  
 Se non sono disponibili autorizzazioni di accesso ai file, è possibile chiedere all'utente di fornire informazioni specifiche sui file usando la classe <xref:System.Windows.Forms.OpenFileDialog> o <xref:System.Windows.Forms.SaveFileDialog>.  Questa interazione utente fornisce una discreta garanzia che l'applicazione non possa caricare file riservati o sovrascrivere file importanti in modo intenzionalmente dannoso.  I metodi <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> e <xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A> forniscono l'accesso ai file in lettura e scrittura aprendo il flusso di file per il file specificato dall'utente.  I metodi consentono anche di proteggere il file dell'utente nascondendo il percorso del file.  
  
> [!NOTE]
>  Queste autorizzazioni variano a seconda del fatto che l'applicazione sia nell'area Internet o nell'area Intranet.  Le applicazioni dell'area Internet possono usare solo <xref:System.Windows.Forms.OpenFileDialog>, mentre le applicazioni Intranet hanno un'autorizzazione senza restrizioni per le finestre di dialogo per la gestione dei file.  
  
 La classe <xref:System.Security.Permissions.FileDialogPermission> specifica il tipo di finestra di dialogo per la gestione dei file che può essere usato dall'applicazione.  La seguente tabella mostra il valore di cui è necessario disporre per usare ogni classe <xref:System.Windows.Forms.FileDialog>.  
  
|Classe|Valore di accesso necessario|  
|------------|----------------------------------|  
|<xref:System.Windows.Forms.OpenFileDialog>|<xref:System.Security.Permissions.FileDialogPermissionAccess>|  
|<xref:System.Windows.Forms.SaveFileDialog>|<xref:System.Security.Permissions.FileDialogPermissionAccess>|  
  
> [!NOTE]
>  L'autorizzazione specifica viene richiesta solo dopo che il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> viene effettivamente chiamato.  
  
 L'autorizzazione per visualizzare una finestra di dialogo per la gestione dei file non concede all'applicazione l'accesso completo a tutti i membri delle classi <xref:System.Windows.Forms.FileDialog>, <xref:System.Windows.Forms.OpenFileDialog>e <xref:System.Windows.Forms.SaveFileDialog>.  Per le autorizzazioni esattamente necessarie per chiamare ogni metodo, vedere l'argomento di riferimento per tale metodo nella documentazione della libreria di classi di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Il seguente esempio di codice usa il metodo <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> per aprire un file specificato dall'utente in un controllo <xref:System.Windows.Forms.RichTextBox>.  L'esempio richiede <xref:System.Security.Permissions.FileDialogPermission> e il valore dell'enumerazione <xref:System.Security.Permissions.FileDialogPermissionAttribute.Open%2A> associata.  L'esempio illustra come gestire <xref:System.Security.SecurityException> per determinare se disabilitare la funzionalità di salvataggio.  Questo esempio richiede che <xref:System.Windows.Forms.Form> disponga di un controllo <xref:System.Windows.Forms.Button> denominato `ButtonOpen` e di un controllo <xref:System.Windows.Forms.RichTextBox> denominato `RtfBoxMain`.  
  
> [!NOTE]
>  La logica di programmazione per la funzionalità di salvataggio non è illustrata nell'esempio.  
  
```vb  
Private Sub ButtonOpen_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles ButtonOpen.Click   
  
    Dim editingFileName as String = ""  
    Dim saveAllowed As Boolean = True  
  
    ' Displays the OpenFileDialog.  
    If (OpenFileDialog1.ShowDialog() = DialogResult.OK) Then  
        Dim userStream as System.IO.Stream  
        Try   
            ' Opens the file stream for the file selected by the user.  
            userStream =OpenFileDialog1.OpenFile()   
            Me.RtfBoxMain.LoadFile(userStream, _  
                RichTextBoxStreamType.PlainText)  
        Finally  
            userStream.Close()  
        End Try  
  
        ' Tries to get the file name selected by the user.  
        ' Failure means that the application does not have  
        ' unrestricted permission to the file.  
        Try   
            editingFileName = OpenFileDialog1.FileName  
        Catch ex As Exception  
            If TypeOf ex Is System.Security.SecurityException Then   
                ' The application does not have unrestricted permission   
                ' to the file so the save feature will be disabled.  
                saveAllowed = False   
            Else   
                Throw ex  
            End If  
        End Try  
    End If  
End Sub  
  
```  
  
```csharp  
private void ButtonOpen_Click(object sender, System.EventArgs e)   
{  
    String editingFileName = "";  
    Boolean saveAllowed = true;  
  
    // Displays the OpenFileDialog.  
    if (openFileDialog1.ShowDialog() == DialogResult.OK)   
    {  
        // Opens the file stream for the file selected by the user.  
        using (System.IO.Stream userStream = openFileDialog1.OpenFile())   
        {  
            this.RtfBoxMain.LoadFile(userStream,  
                RichTextBoxStreamType.PlainText);  
            userStream.Close();  
        }  
  
        // Tries to get the file name selected by the user.  
        // Failure means that the application does not have  
        // unrestricted permission to the file.  
        try   
        {  
            editingFileName = openFileDialog1.FileName;  
        }   
        catch (Exception ex)   
        {  
            if (ex is System.Security.SecurityException)   
            {  
                // The application does not have unrestricted permission   
                // to the file so the save feature will be disabled.  
                saveAllowed = false;   
            }   
            else   
            {  
                throw ex;  
            }  
        }  
    }  
}  
```  
  
> [!NOTE]
>  In [!INCLUDE[csprcs](../../../includes/csprcs-md.md)], assicurarsi di aggiungere il codice per abilitare il gestore eventi.  Usando il codice dell'esempio precedente, il seguente codice mostra come abilitare il gestore eventi.`this.ButtonOpen.Click += newSystem.Windows.Forms.EventHandler(this.ButtonOpen_Click);`  
  
### Altri file  
 Talvolta sarà necessario leggere o scrivere in file non specificati dall'utente, ad esempio quando si devono rendere persistenti le impostazioni dell'applicazione.  Nelle aree Internet e Intranet locale, l'applicazione non disporrà delle autorizzazioni per archiviare i dati in un file locale.  Tuttavia, l'applicazione potrà archiviare dati nello spazio di memorizzazione isolato.  Lo spazio di memorizzazione isolato è un raggruppamento dati astratto, non un percorso di archiviazione specifico, contenente uno o più file dello spazio di memorizzazione isolato, denominati archivi, che includono i percorsi di directory in cui sono effettivamente memorizzati i dati.  Non sono necessarie autorizzazioni di accesso ai file, ad esempio <xref:System.Security.Permissions.FileIOPermission>. La classe <xref:System.Security.Permissions.IsolatedStoragePermission> controlla invece le autorizzazioni per lo spazio di memorizzazione isolato.  Per impostazione predefinita, le applicazioni eseguite nelle aree Internet e Intranet locale possono archiviare i dati usando lo spazio di memorizzazione isolato. Tuttavia, le impostazioni come la quota disco possono variare.  Per altre informazioni sullo spazio di memorizzazione isolato, vedere [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md).  
  
 L'esempio seguente usa lo spazio di memorizzazione isolato per scrivere dati in un file contenuto in un archivio.  L'esempio richiede <xref:System.Security.Permissions.IsolatedStorageFilePermission> e il valore dell'enumerazione <xref:System.Security.Permissions.IsolatedStorageContainment>.  L'esempio illustra come leggere e scrivere alcuni valori delle proprietà del controllo <xref:System.Windows.Forms.Button> in un file nello spazio di memorizzazione isolato.  La funzione `Read` verrà chiamata dopo l'avvio dell'applicazione e la funzione `Write` verrà chiamata prima della chiusura dell'applicazione.  L'esempio richiede che le funzioni `Read` e `Write` esistano come membri di un oggetto <xref:System.Windows.Forms.Form> contenente un controllo <xref:System.Windows.Forms.Button>denominato `MainButton`.  
  
```vb  
' Reads the button options from the isolated storage. Uses Default values   
' for the button if the options file does not exist.  
Public Sub Read()   
    Dim isoStore As System.IO.IsolatedStorage.IsolatedStorageFile = _  
        System.IO.IsolatedStorage.IsolatedStorageFile. _   
        GetUserStoreForDomain()  
  
    Dim filename As String = "options.txt"  
    Try  
        ' Checks to see if the options.txt file exists.  
        If (isoStore.GetFileNames(filename).GetLength(0) <> 0) Then  
  
            ' Opens the file because it exists.  
            Dim isos As New System.IO.IsolatedStorage.IsolatedStorageFileStream _   
                 (filename, IO.FileMode.Open,isoStore)  
            Dim reader as System.IO.StreamReader  
            Try   
                reader = new System.IO.StreamReader(isos)  
  
                ' Reads the values stored.  
                Dim converter As System.ComponentModel.TypeConverter  
                converter = System.ComponentModel.TypeDescriptor.GetConverter _   
                    (GetType(Color))  
  
                Me.MainButton.BackColor = _   
                        CType(converter.ConvertFromString _   
                         (reader.ReadLine()), Color)  
                me.MainButton.ForeColor = _  
                        CType(converter.ConvertFromString _   
                         (reader.ReadLine()), Color)  
  
                converter = System.ComponentModel.TypeDescriptor.GetConverter _   
                    (GetType(Font))  
                me.MainButton.Font = _  
                        CType(converter.ConvertFromString _   
                         (reader.ReadLine()), Font)  
  
            Catch ex As Exception  
                Debug.WriteLine("Cannot read options " + _  
                    ex.ToString())  
            Finally  
                reader.Close()  
            End Try  
        End If  
  
    Catch ex As Exception  
        Debug.WriteLine("Cannot read options " + ex.ToString())  
    End Try  
End Sub  
  
' Writes the button options to the isolated storage.  
Public Sub Write()   
    Dim isoStore As System.IO.IsolatedStorage.IsolatedStorageFile = _  
        System.IO.IsolatedStorage.IsolatedStorageFile. _   
        GetUserStoreForDomain()  
  
    Dim filename As String = "options.txt"  
    Try   
        ' Checks if the file exists, and if it does, tries to delete it.  
        If (isoStore.GetFileNames(filename).GetLength(0) <> 0) Then  
            isoStore.DeleteFile(filename)  
        End If  
    Catch ex As Exception  
        Debug.WriteLine("Cannot delete file " + ex.ToString())  
    End Try  
  
    ' Creates the options.txt file and writes the button options to it.  
    Dim writer as System.IO.StreamWriter  
    Try   
        Dim isos As New System.IO.IsolatedStorage.IsolatedStorageFileStream _   
             (filename, IO.FileMode.CreateNew, isoStore)  
  
        writer = New System.IO.StreamWriter(isos)  
        Dim converter As System.ComponentModel.TypeConverter  
  
        converter = System.ComponentModel.TypeDescriptor.GetConverter _   
           (GetType(Color))  
        writer.WriteLine(converter.ConvertToString( _  
            Me.MainButton.BackColor))  
        writer.WriteLine(converter.ConvertToString( _  
            Me.MainButton.ForeColor))  
  
        converter = System.ComponentModel TypeDescriptor.GetConverter _   
           (GetType(Font))  
        writer.WriteLine(converter.ConvertToString( _  
            Me.MainButton.Font))  
  
    Catch ex as Exception  
        Debug.WriteLine("Cannot write options " + ex.ToString())  
  
    Finally  
        writer.Close()  
    End Try  
End Sub  
  
```  
  
```csharp  
// Reads the button options from the isolated storage. Uses default values   
// for the button if the options file does not exist.  
public void Read()   
{  
    System.IO.IsolatedStorage.IsolatedStorageFile isoStore =   
        System.IO.IsolatedStorage.IsolatedStorageFile.  
        GetUserStoreForDomain();  
  
    string filename = "options.txt";  
    try  
    {  
        // Checks to see if the options.txt file exists.  
        if (isoStore.GetFileNames(filename).GetLength(0) != 0)   
        {  
            // Opens the file because it exists.  
            System.IO.IsolatedStorage.IsolatedStorageFileStream isos =   
                new System.IO.IsolatedStorage.IsolatedStorageFileStream  
                    (filename, System.IO.FileMode.Open,isoStore);  
            System.IO.StreamReader reader = null;  
            try   
            {  
                reader = new System.IO.StreamReader(isos);  
  
                // Reads the values stored.  
                TypeConverter converter ;  
                converter = TypeDescriptor.GetConverter(typeof(Color));  
  
                this.MainButton.BackColor =   
                 (Color)(converter.ConvertFromString(reader.ReadLine()));  
                this.MainButton.ForeColor =   
                 (Color)(converter.ConvertFromString(reader.ReadLine()));  
  
                converter = TypeDescriptor.GetConverter(typeof(Font));  
                this.MainButton.Font =   
                  (Font)(converter.ConvertFromString(reader.ReadLine()));  
            }  
            catch (Exception ex)  
            {   
                System.Diagnostics.Debug.WriteLine  
                     ("Cannot read options " + ex.ToString());  
            }  
            finally  
            {  
                reader.Close();  
            }  
        }  
    }   
    catch (Exception ex)   
    {  
        System.Diagnostics.Debug.WriteLine  
            ("Cannot read options " + ex.ToString());  
    }  
}  
  
// Writes the button options to the isolated storage.  
public void Write()   
{  
    System.IO.IsolatedStorage.IsolatedStorageFile isoStore =   
        System.IO.IsolatedStorage.IsolatedStorageFile.  
        GetUserStoreForDomain();  
  
    string filename = "options.txt";  
    try   
    {  
        // Checks if the file exists and, if it does, tries to delete it.  
        if (isoStore.GetFileNames(filename).GetLength(0) != 0)   
        {  
            isoStore.DeleteFile(filename);  
        }  
    }  
    catch (Exception ex)   
    {  
        System.Diagnostics.Debug.WriteLine  
            ("Cannot delete file " + ex.ToString());  
    }  
  
    // Creates the options file and writes the button options to it.  
    System.IO.StreamWriter writer = null;  
    try   
    {  
        System.IO.IsolatedStorage.IsolatedStorageFileStream isos = new   
            System.IO.IsolatedStorage.IsolatedStorageFileStream(filename,   
            System.IO.FileMode.CreateNew,isoStore);  
  
        writer = new System.IO.StreamWriter(isos);  
        TypeConverter converter ;  
  
        converter = TypeDescriptor.GetConverter(typeof(Color));  
        writer.WriteLine(converter.ConvertToString(  
            this.MainButton.BackColor));  
        writer.WriteLine(converter.ConvertToString(  
            this.MainButton.ForeColor));  
  
        converter = TypeDescriptor.GetConverter(typeof(Font));  
        writer.WriteLine(converter.ConvertToString(  
            this.MainButton.Font));  
  
    }  
    catch (Exception ex)  
    {   
        System.Diagnostics.Debug.WriteLine  
           ("Cannot write options " + ex.ToString());  
    }  
    finally  
    {  
        writer.Close();  
    }  
}  
```  
  
## Accesso a database  
 Le autorizzazioni necessarie per accedere a un database variano in base al provider del database. Tuttavia, solo le applicazioni in esecuzione con le autorizzazioni appropriate possono accedere a un database tramite una connessione dati.  Per altre informazioni sulle autorizzazioni necessarie per accedere a un database, vedere [Sicurezza dall'accesso di codice e ADO.NET](../../../docs/framework/data/adonet/code-access-security.md).  
  
 Se non è possibile accedere direttamente a un database, perché si desidera che l'applicazione venga eseguita con attendibilità parziale, è possibile usare un servizio Web come alternativa per accedere ai dati.  Un servizio Web è un componente software accessibile a livello di codice in una rete.  Con i servizi Web, le applicazioni possono condividere dati tra le aree dei gruppi di codice.  Per impostazione predefinita, alle applicazioni nelle aree Internet e Intranet locale viene concesso il diritto di accedere ai relativi siti di origine. Questo consente a tali applicazioni di chiamare un servizio Web ospitato nello stesso server.  Per altre informazioni, vedere [Servizi Web in ASP.NET AJAX](http://msdn.microsoft.com/it-it/8290e543-7eff-47a4-aace-681f3c07229b) o [Windows Communication Foundation](http://msdn.microsoft.com/library/ms735119.aspx).  
  
## Accesso al Registro di sistema  
 La classe <xref:System.Security.Permissions.RegistryPermission> controlla l'accesso al Registro di sistema del sistema operativo.  Per impostazione predefinita, solo le applicazioni in esecuzione in locale possono accedere al Registro di sistema.  <xref:System.Security.Permissions.RegistryPermission> concede a un'applicazione solo il diritto di provare ad accedere al Registro di sistema. Non garantisce l'accesso, perché il sistema operativo continua ad applicare la sicurezza al Registro di sistema.  
  
 Poiché non è possibile accedere al Registro di sistema con l'attendibilità parziale, potrebbe essere necessario trovare altri metodi di archiviazione dei dati.  Quando si archiviano le impostazioni dell'applicazione, usare lo spazio di memorizzazione isolato invece del Registro di sistema.  Lo spazio di memorizzazione isolato può essere usato anche per archiviare altri file specifici dell'applicazione.  È anche possibile archiviare informazioni di applicazioni globali relative al server o al sito di origine, perché, per impostazione predefinita, a un'applicazione viene concesso il diritto di accedere al sito di origine.  
  
## Vedere anche  
 [More Secure Printing in Windows Forms](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)   
 [Additional Security Considerations in Windows Forms](../../../docs/framework/winforms/additional-security-considerations-in-windows-forms.md)   
 [Security in Windows Forms Overview](../../../docs/framework/winforms/security-in-windows-forms-overview.md)   
 [Windows Forms Security](../../../docs/framework/winforms/windows-forms-security.md)   
 [Mage.exe \(Strumento per la generazione e la modifica di manifesti\)](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md)   
 [MageUI.exe \(Manifest Generation and Editing Tool, Graphical Client\)](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)