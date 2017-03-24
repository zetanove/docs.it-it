---
title: "/win32manifest (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/win32manifest"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/win32manifest compiler option [C#]"
  - "win32manifest compiler option [C#]"
  - "-win32manifest compiler option [C#]"
ms.assetid: 9460ea1b-6c9f-44b8-8f73-301b30a01de1
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# /win32manifest (C# Compiler Options)
Utilizzare l'opzione **\/win32manifest** per specificare un file manifesto dell'applicazione Win32 definito dall'utente da incorporare nel file eseguibile di tipo PE di un progetto.  
  
## Sintassi  
  
```  
/win32manifest: filename  
```  
  
## Argomenti  
 `filename`  
 Nome e percorso del file manifesto personalizzato.  
  
## Note  
 Per impostazione predefinita, il compilatore [!INCLUDE[csharp_current_short](../../../csharp/language-reference/compiler-options/includes/csharp-current-short-md.md)] incorpora un manifesto di applicazione che specifica un livello di esecuzione obbligatorio di "asInvoker". Crea il manifesto nella stessa cartella nella quale è compilato l'eseguibile, in genere la cartella bin\\Debug o bin\\Release quando si utilizza Visual Studio.  Se si desidera fornire un manifesto personalizzato, ad esempio per specificare un livello di esecuzione obbligatorio "highestAvailable" o "requireAdministrator", utilizzare questa opzione per specificare il nome del file.  
  
> [!NOTE]
>  Questa opzione e l'opzione [\/win32res \(Import a Win32 Resource File\)](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md) si escludono a vicenda.  Se si tenta di utilizzare entrambe le opzioni nella stessa riga di comando, si otterrà un errore di compilazione.  
  
 Un'applicazione che non ha nessun manifesto di applicazione che specifica un livello di esecuzione obbligatorio sarà soggetto alla virtualizzazione di file\/Registro di sistema nella funzionalità Controllo account utente in Windows Vista.  Per ulteriori informazioni sulla virtualizzazione, vedere [Storia dello Sviluppatore Windows Vista: Requisiti di Sviluppo delle Applicazioni di Windows Vista per il Controllo dell'Account Utente \(UAC\)](http://go.microsoft.com/fwlink/?LinkId=95452).  
  
 L'applicazione sarà soggetta a virtualizzazione se si verifica una delle seguenti condizioni:  
  
-   Si utilizza l'opzione **\/nowin32manifest** e non si fornisce un manifesto in una successiva istruzione di compilazione o come parte di file di risorse Windows \(.res\) utilizzando l'opzione **\/win32res**.  
  
-   Si fornisce un manifesto personalizzato che non specifica un livello di esecuzione obbligatorio.  
  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] crea un file .manifesto predefinito e lo archivia nelle directory Debug e Release insieme al file eseguibile.  È possibile aggiungere un manifesto personalizzato creandone uno in qualsiasi editor di testo e aggiungendolo quindi al progetto.  In alternativa, è possibile fare clic con il pulsante destro del mouse sull'icona **Progetto** in **Esplora soluzioni**, fare clic su **Aggiungi nuovo elemento** e quindi su **File manifesto applicazione**.  Dopo avere aggiunto il file manifesto nuovo o esistente, verrà visualizzato nell'elenco a discesa **Manifesto**.  Per ulteriori informazioni, vedere [Applicazione \(pagina\), Creazione progetti \(C\#\)](/visual-studio/ide/reference/application-page-project-designer-csharp).  
  
 È possibile fornire il manifesto di applicazione come passaggio post\-compilazione personalizzato o come parte di un file di risorse Win32 utilizzando l'opzione [\/nowin32manifest \(No Win32 Manifest\)](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md).  Utilizzare la stessa opzione se si desidera che l'applicazione sia soggetta alla virtualizzazione di file o Registro di sistema in Windows Vista.  In questo modo il compilatore non creerà né incorporerà un manifesto predefinito nel file di tipo PE.  
  
## Esempio  
 Nell'esempio seguente viene illustrato il manifesto predefinito che il compilatore di Visual C\# inserisce in un file PE.  
  
> [!NOTE]
>  Il compilatore inserisce un nome standard dell'applicazione "MyApplication.app" nell'xml.  Si tratta di una soluzione alternativa per consentire alle applicazioni di essere eseguite in Windows Server 2003 Service Pack 3.  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [\/nowin32manifest \(No Win32 Manifest\)](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)