---
title: "Additional Security Considerations in Windows Forms | Microsoft Docs"
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
  - "Windows API, secure calls"
  - "Windows Forms, secure calls to Windows API"
  - "Windows API, calling"
  - "APIs, calling"
  - "security [Windows Forms]"
  - "Windows API, Windows Forms security settings"
  - "API calls, Windows Forms security settings"
  - "security [Windows Forms], calling APIs"
  - "Clipboard, securing access"
ms.assetid: 15abda8b-0527-47c7-aedb-77ab595f2bf1
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Additional Security Considerations in Windows Forms
Le impostazioni di sicurezza di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] possono far sì che si verifichino delle differenze tra l'esecuzione dell'applicazione in un ambiente parzialmente attendibile e quella sul computer locale.  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] impedisce l'accesso ad alcune risorse locali critiche, ad esempio file system, rete e API non gestite.  Le impostazioni di sicurezza influiscono sulla possibilità di chiamare l'API Win32 Microsoft o altre API che non possono essere verificate dal sistema di sicurezza.  La sicurezza influisce anche su altri aspetti dell'applicazione, inclusi l'accesso ai file e ai dati nonché le operazioni di stampa.  Per ulteriori informazioni sull'accesso ai file e ai dati in un ambiente parzialmente attendibile, vedere [More Secure File and Data Access in Windows Forms](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md).  Per ulteriori informazioni sulla stampa in un ambiente parzialmente attendibile, vedere [More Secure Printing in Windows Forms](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md).  
  
 Nelle sezioni riportate di seguito viene illustrato come utilizzare gli Appunti, modificare le finestre e chiamare l'API Win32 da applicazioni in esecuzione in un ambiente parzialmente attendibile.  
  
## Accesso agli Appunti  
 La classe <xref:System.Security.Permissions.UIPermission> consente di controllare l'accesso agli Appunti, mentre il valore di enumerazione <xref:System.Security.Permissions.UIPermissionClipboard> associato indica il livello di accesso.  Nella tabella che segue sono riportati i possibili livelli di autorizzazione.  
  
|Valore UIPermissionClipboard|Descrizione|  
|----------------------------------|-----------------|  
|<xref:System.Security.Permissions.UIPermissionClipboard>|È possibile utilizzare gli Appunti senza limitazioni.|  
|<xref:System.Security.Permissions.UIPermissionClipboard>|È possibile utilizzare gli Appunti con alcune limitazioni.  Per la possibilità di inserire dati negli Appunti \(tramite le operazioni dei comandi Copia o Taglia\) non esiste alcuna limitazione.  I controlli intrinseci che accettano l'operazione Incolla, ad esempio una casella di testo, possono accettare i dati degli Appunti, ma i controlli utente non possono leggere a livello di codice dagli Appunti.|  
|<xref:System.Security.Permissions.UIPermissionClipboard>|Non è possibile utilizzare gli Appunti.|  
  
 Per impostazione predefinita, all'area Intranet locale viene concesso il diritto di accesso <xref:System.Security.Permissions.UIPermissionClipboard> e all'area Internet il diritto di accesso <xref:System.Security.Permissions.UIPermissionClipboard>.  L'applicazione è quindi in grado di copiare i dati negli Appunti, ma non può incollare o leggere dagli Appunti a livello di codice.  Queste limitazioni impediscono ai programmi non full trust di leggere il contenuto copiato negli Appunti da un'altra applicazione.  Se l'applicazione richiede un accesso completo agli Appunti ma non si dispone delle autorizzazioni richieste, sarà necessario aumentare le autorizzazioni dell'applicazione.  Per ulteriori informazioni sull'aumento delle autorizzazioni, vedere [Amministrazione generale dei criteri di sicurezza](http://msdn.microsoft.com/it-it/5121fe35-f0e3-402c-94ab-4f35b0a87b4b).  
  
## Modifica delle finestre  
 La classe <xref:System.Security.Permissions.UIPermission> consente inoltre di controllare le autorizzazioni per la modifica delle finestre e l'esecuzione di altre azioni correlate all'interfaccia utente, mentre il valore di enumerazione <xref:System.Security.Permissions.UIPermissionWindow> associato indica il livello di accesso.  Nella tabella che segue sono riportati i possibili livelli di autorizzazione.  
  
 Per impostazione predefinita, all'area Intranet locale viene concesso il diritto di accesso <xref:System.Security.Permissions.UIPermissionWindow> e all'area Internet il diritto di accesso <xref:System.Security.Permissions.UIPermissionWindow>.  Nell'area Internet, quindi, l'applicazione può eseguire la maggior parte delle azioni relative alle finestre e all'interfaccia utente, ma l'aspetto della finestra verrà modificato.  La finestra modificata visualizza una notifica alla prima esecuzione, contiene testo modificato della barra del titolo e richiede un pulsante di chiusura sulla barra del titolo.  Il suggerimento e la barra del titolo indicano all'utente che l'applicazione è in esecuzione con attendibilità parziale.  
  
|Valore UIPermissionWindow|Descrizione|  
|-------------------------------|-----------------|  
|<xref:System.Security.Permissions.UIPermissionWindow>|Gli utenti possono utilizzare tutte le finestre e gli eventi di input utente senza restrizioni.|  
|<xref:System.Security.Permissions.UIPermissionWindow>|Gli utenti possono utilizzare per il disegno soltanto le finestre protette di primo livello e le sottofinestre sicure e possono utilizzare soltanto gli eventi di input dell'interfaccia utente all'interno di tali finestre e sottofinestre.  Le finestre sicure sono chiaramente contrassegnate e prevedono alcune limitazioni sulle dimensioni minima e massima.  Tali limitazioni impediscono attacchi di spoofing potenzialmente dannosi, ad esempio l'imitazione delle schermate di accesso del sistema o del desktop, nonché l'accesso a livello di codice alle finestre padre, la chiamate alle API relative allo stato attivo e l'utilizzo del controllo <xref:System.Windows.Forms.ToolTip>.|  
|<xref:System.Security.Permissions.UIPermissionWindow>|Gli utenti possono utilizzare per il disegno soltanto le sottofinestre sicure e possono utilizzare soltanto gli eventi di input dell'interfaccia utente all'interno di tali sottofinestre.  Un esempio di sottofinestra sicura è costituito da un controllo all'interno di un browser.|  
|<xref:System.Security.Permissions.UIPermissionWindow>|Gli utenti non possono utilizzare alcuna finestra o evento di interfaccia.  Non è possibile utilizzare alcuna interfaccia utente.|  
  
 Ciascun livello di autorizzazione identificato dall'enumerazione <xref:System.Security.Permissions.UIPermissionWindow> consente meno azioni rispetto al livello superiore.  Nelle tabelle riportate di seguito sono indicate le azioni limitate dai valori <xref:System.Security.Permissions.UIPermissionWindow> e <xref:System.Security.Permissions.UIPermissionWindow>.  Per conoscere esattamente le autorizzazioni richieste per ciascun membro, fare riferimento all'argomento relativo a tale membro nella documentazione sulla libreria di classi di .NET Framework.  
  
 Nella tabella seguente sono elencate le azioni impedite dall'autorizzazione <xref:System.Security.Permissions.UIPermissionWindow>.  
  
|Componente|Azioni limitate|  
|----------------|---------------------|  
|<xref:System.Windows.Forms.Application>|-   Impostazione della proprietà <xref:System.Windows.Forms.Application.SafeTopLevelCaptionFormat%2A>.|  
|<xref:System.Windows.Forms.Control>|-   Recupero della proprietà <xref:System.Windows.Forms.Control.Parent%2A>.<br />-   Impostazione della proprietà `Region`.<br />-   Chiamata al metodo <xref:System.Windows.Forms.Control.FindForm%2A> , <xref:System.Windows.Forms.Control.Focus%2A>, <xref:System.Windows.Forms.Control.FromChildHandle%2A>, <xref:System.Windows.Forms.Control.FromHandle%2A>, <xref:System.Windows.Forms.Control.PreProcessMessage%2A>, <xref:System.Windows.Forms.Control.ReflectMessage%2A>, o <xref:System.Windows.Forms.Control.SetTopLevel%2A>.<br />-   Chiamata al metodo <xref:System.Windows.Forms.Control.GetChildAtPoint%2A> se il controllo restituito non è figlio del controllo chiamante.<br />-   Modifica dello stato attivo del controllo all'interno di un controllo contenitore.|  
|<xref:System.Windows.Forms.Cursor>|-   Impostazione della proprietà <xref:System.Windows.Forms.Cursor.Clip%2A>.<br />-   Chiamata al metodo <xref:System.Windows.Forms.Control.Hide%2A>.|  
|<xref:System.Windows.Forms.DataGrid>|-   Chiamata al metodo <xref:System.Windows.Forms.ContainerControl.ProcessTabKey%2A>.|  
|<xref:System.Windows.Forms.Form>|-   Recupero della proprietà <xref:System.Windows.Forms.Form.ActiveForm%2A> o <xref:System.Windows.Forms.Form.MdiParent%2A>.<br />-   Impostazione della proprietà <xref:System.Windows.Forms.Form.ControlBox%2A>, <xref:System.Windows.Forms.Form.ShowInTaskbar%2A> o <xref:System.Windows.Forms.Form.TopMost%2A>.<br />-   Impostazione della proprietà <xref:System.Windows.Forms.Form.Opacity%2A> su un valore inferiore al 50%.<br />-   Impostazione della proprietà <xref:System.Windows.Forms.Form.WindowState%2A> su <xref:System.Windows.Forms.FormWindowState> a livello di codice.<br />-   Chiamata al metodo <xref:System.Windows.Forms.Form.Activate%2A>.<br />-   Utilizzo dei valori di enumerazione <xref:System.Windows.Forms.FormBorderStyle>, <xref:System.Windows.Forms.FormBorderStyle> e <xref:System.Windows.Forms.FormBorderStyle> <xref:System.Windows.Forms.FormBorderStyle>.|  
|<xref:System.Windows.Forms.NotifyIcon>|-   L'utilizzo del componente <xref:System.Windows.Forms.NotifyIcon> è completamente limitato.|  
  
 Il valore <xref:System.Security.Permissions.UIPermissionWindow> limita le azioni elencate nella tabella riportata di seguito, oltre alle limitazioni definite dal valore <xref:System.Security.Permissions.UIPermissionWindow>.  
  
|Componente|Azioni limitate|  
|----------------|---------------------|  
|<xref:System.Windows.Forms.CommonDialog>|-   Visualizzazione di una finestra di dialogo derivata dalla classe <xref:System.Windows.Forms.CommonDialog>.|  
|<xref:System.Windows.Forms.Control>|-   Chiamata al metodo <xref:System.Windows.Forms.Control.CreateGraphics%2A>.<br />-   Impostazione della proprietà <xref:System.Windows.Forms.Control.Cursor%2A>.|  
|<xref:System.Windows.Forms.Control.Cursor%2A>|-   Impostazione della proprietà <xref:System.Windows.Forms.Cursor.Current%2A>.|  
|<xref:System.Windows.Forms.MessageBox>|-   Chiamata al metodo <xref:System.Windows.Forms.Form.Show%2A>.|  
  
### Hosting di controlli di terze parti  
 Un altro tipo di manipolazione delle finestre può verificarsi se i form ospitano controlli di terze parti.  Per controllo di terze parti si intende qualsiasi controllo <xref:System.Windows.Forms.UserControl> personalizzato non sviluppato né compilato personalmente.  Sebbene lo scenario di hosting sia difficile da sfruttare, in teoria è possibile che la superficie di rendering di un controllo di terze parti si espanda per coprire l'intera area del form.  Questo controllo potrebbe quindi riprodurre una finestra di dialogo critica e richiedere agli utenti informazioni quali le combinazioni di nome utente\/password o i numeri di conto corrente.  
  
 Per limitare questo rischio potenziale, utilizzare controlli di terze parti solo di fornitori attendibili.  Se si utilizzano controlli di terze parti scaricati da una fonte non verificabile, si consiglia di esaminare il codice sorgente per rilevare potenziali attacchi alla sicurezza.  Dopo aver verificato che il codice sorgente non è dannoso, è necessario compilare personalmente l'assembly per assicurarsi che il codice sorgente corrisponda all'assembly.  
  
## Chiamate all'API Win32  
 Se il progetto dell'applicazione richiede la chiamata a una funzione dell'API Win32, si accede al codice non gestito.  In questo caso, non è possibile determinare le azioni del codice relative alla finestra o al sistema operativo quando si utilizzano valori o chiamate all'API Win32.  La classe <xref:System.Security.Permissions.SecurityPermission> e il valore <xref:System.Security.Permissions.SecurityPermissionFlag> dell'enumerazione <xref:System.Security.Permissions.SecurityPermissionFlag> consentono di controllare l'accesso al codice non gestito.  Un'applicazione può accedere al codice non gestito solo se dispone dell'autorizzazione <xref:System.Security.Permissions.SecurityPermissionFlag>.  Per impostazione predefinita, soltanto le applicazioni eseguite localmente possono effettuare chiamate al codice non gestito.  
  
 Alcuni membri di Windows Form forniscono un tipo di accesso non gestito che richiede l'autorizzazione <xref:System.Security.Permissions.SecurityPermissionFlag>.  Nella tabella riportata di seguito sono elencati i membri nello spazio dei nomi <xref:System.Windows.Forms> che richiedono tale autorizzazione.  Per ulteriori informazioni sulle autorizzazioni richieste per un membro, fare riferimento alla documentazione sulla libreria di classi di .NET Framework.  
  
|Componente|Membro|  
|----------------|------------|  
|<xref:System.Windows.Forms.Application>|-   Metodo <xref:System.Windows.Forms.Application.AddMessageFilter%2A><br />-   Proprietà <xref:System.Windows.Forms.Application.CurrentInputLanguage%2A><br />-   Metodo `Exit`<br />-   Metodo <xref:System.Windows.Forms.Application.ExitThread%2A><br />-   Evento <xref:System.Windows.Forms.Application.ThreadException>|  
|<xref:System.Windows.Forms.CommonDialog>|-   Metodo <xref:System.Windows.Forms.CommonDialog.HookProc%2A><br />-   Metodo <xref:System.Windows.Forms.CommonDialog.OwnerWndProc%2A><br />-   Metodo <xref:System.Windows.Forms.CommonDialog.Reset%2A><br />-   Metodo <xref:System.Windows.Forms.CommonDialog.RunDialog%2A>|  
|<xref:System.Windows.Forms.Control>|-   Metodo <xref:System.Windows.Forms.Control.CreateParams%2A><br />-   Metodo <xref:System.Windows.Forms.Control.DefWndProc%2A><br />-   Metodo <xref:System.Windows.Forms.Control.DestroyHandle%2A><br />-   Metodo <xref:System.Windows.Forms.Control.WndProc%2A>|  
|<xref:System.Windows.Forms.Help>|-   Metodi <xref:System.Windows.Forms.Help.ShowHelp%2A><br />-   Metodo <xref:System.Windows.Forms.Help.ShowHelpIndex%2A>|  
|<xref:System.Windows.Forms.NativeWindow>|-   Classe <xref:System.Windows.Forms.NativeWindow>|  
|<xref:System.Windows.Forms.Screen>|-   Metodo <xref:System.Windows.Forms.Screen.FromHandle%2A>|  
|<xref:System.Windows.Forms.SendKeys>|-   Metodo <xref:System.Windows.Forms.SendKeys.Send%2A><br />-   Metodo <xref:System.Windows.Forms.SendKeys.SendWait%2A>|  
  
 Se non dispone dell'autorizzazione per effettuare chiamate al codice non gestito, l'applicazione deve richiedere l'autorizzazione <xref:System.Security.Permissions.SecurityPermissionFlag>. In caso contrario, è necessario prendere in considerazione modi alternativi di implementazione delle funzionalità. In molti casi, Windows Form fornisce un'alternativa gestita alle funzioni dell'API Win32.  Se non esistono alternative e l'applicazione richiede l'accesso al codice non gestito, sarà necessario aumentare le autorizzazioni dell'applicazione.  
  
 L'autorizzazione a chiamare il codice non gestito consente di eseguire praticamente qualsiasi operazione nell'applicazione.  Per questo motivo, questo tipo di autorizzazione deve essere concesso solo alle applicazioni che provengono da un'origine attendibile.  In alternativa, a seconda dell'applicazione, la parte di funzionalità dell'applicazione che effettua la chiamata al codice non gestito potrebbe essere resa facoltativa oppure attivata soltanto nell'ambiente con attendibilità totale.  Per ulteriori informazioni sulle autorizzazioni pericolose, vedere [Autorizzazioni pericolose e amministrazione dei criteri](../../../docs/framework/misc/dangerous-permissions-and-policy-administration.md).  Per ulteriori informazioni sull'elevazione delle autorizzazioni, vedere [NIB: General Security Policy Administration](http://msdn.microsoft.com/it-it/5121fe35-f0e3-402c-94ab-4f35b0a87b4b).  
  
## Vedere anche  
 [More Secure File and Data Access in Windows Forms](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)   
 [More Secure Printing in Windows Forms](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)   
 [Security in Windows Forms Overview](../../../docs/framework/winforms/security-in-windows-forms-overview.md)   
 [Windows Forms Security](../../../docs/framework/winforms/windows-forms-security.md)   
 [Protezione di applicazioni ClickOnce](../Topic/Securing%20ClickOnce%20Applications.md)