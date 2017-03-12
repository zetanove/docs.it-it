---
title: "/win32manifest (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/win32manifest compiler option [Visual Basic]"
  - "win32manifest compiler option [Visual Basic]"
  - "-win32manifest compiler option [Visual Basic]"
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# /win32manifest (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Identifica un file manifesto dell'applicazione Win32 definito dall'utente da incorporare nel file eseguibile di tipo PE di un progetto.  
  
## Sintassi  
  
```  
/win32manifest: fileName  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`fileName`|Percorso del file manifesto personalizzato.|  
  
## Note  
 Per impostazione predefinita, il compilatore Visual Basic incorpora un manifesto di applicazione che specifica un livello di esecuzione obbligatorio asInvoker.  Crea il manifesto nella stessa cartella nella quale è compilato il file eseguibile, in genere la cartella bin\\Debug o bin\\Release quando si utilizza Visual Studio.  Se si desidera fornire un manifesto personalizzato, ad esempio per specificare un livello di esecuzione obbligatorio highestAvailable o requireAdministrator, utilizzare questa opzione per specificare il nome del file.  
  
> [!NOTE]
>  Questa opzione e l'opzione [\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) si escludono a vicenda.  Se si tenta di utilizzare entrambe le opzioni nella stessa riga di comando, si otterrà un errore di compilazione.  
  
 Un'applicazione che non ha nessun manifesto di applicazione che specifica un livello di esecuzione obbligatorio sarà soggetto alla virtualizzazione di file\/Registro di sistema nella funzionalità Controllo account utente in Windows Vista.  Per ulteriori informazioni sulla virtualizzazione, vedere [ClickOnce Deployment on Windows Vista](/visual-studio/deployment/clickonce-deployment-on-windows-vista).  
  
 L'applicazione sarà soggetta a virtualizzazione se si verifica una delle seguenti condizioni:  
  
1.  Si utilizza l'opzione `/nowin32manifest` e non si fornisce un manifesto in una successiva istruzione di compilazione o come parte di file di risorse Windows \(.res\) utilizzando l'opzione `/win32resource`.  
  
2.  Si fornisce un manifesto personalizzato che non specifica un livello di esecuzione obbligatorio.  
  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] crea un file .manifesto predefinito e lo archivia nelle directory Debug e Release insieme al file eseguibile.  È possibile visualizzare o modificare il file app.manifest predefinito facendo clic su **Visualizza impostazioni di controllo dell'account utente** nella scheda **Applicazione** di Progettazione progetti. Per ulteriori informazioni, vedere [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic).  
  
 È possibile fornire il manifesto di applicazione come passaggio post\-compilazione personalizzato o come parte di un file di risorse Win32 utilizzando l'opzione `/nowin32manifest`.  Utilizzare la stessa opzione se si desidera che l'applicazione sia soggetta alla virtualizzazione di file o Registro di sistema in Windows Vista.  Ciò impedirà il compilatore dal creare e incorporare un manifesto predefinito nel file di tipo PE.  
  
## Esempio  
 Nell'esempio seguente viene illustrato il manifesto predefinito che il compilatore del Visual Basic inserisce in un file PE.  
  
> [!NOTE]
>  Il compilatore inserisce un nome standard dell'applicazione MyApplication.app nel manifesto XML.  Si tratta di una soluzione alternativa per consentire alle applicazioni di essere eseguite in Windows Server 2003 Service Pack 3.  
  
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
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/nowin32manifest](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)