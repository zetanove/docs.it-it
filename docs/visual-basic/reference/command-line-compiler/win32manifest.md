---
title: /win32manifest (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- /win32manifest compiler option [Visual Basic]
- win32manifest compiler option [Visual Basic]
- -win32manifest compiler option [Visual Basic]
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b07d5816e5bb80a95e608fa7214a2db48ebac0dc
ms.lasthandoff: 03/13/2017

---
# <a name="win32manifest-visual-basic"></a>/win32manifest (Visual Basic)
Identifica un file manifesto dell'applicazione Win32 definito dall'utente da incorporare nel file eseguibile di tipo PE di un progetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/win32manifest: fileName  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`fileName`|Il percorso del file manifesto personalizzato.|  
  
## <a name="remarks"></a>Note  
 Per impostazione predefinita, il compilatore Visual Basic consente di incorporare un manifesto dell'applicazione che specifica un livello di esecuzione richiesto di asInvoker. Crea il manifesto nella stessa cartella in cui viene compilato il file eseguibile, in genere la cartella bin\Debug o bin\Release quando si utilizza Visual Studio. Se si desidera fornire un manifesto personalizzato, ad esempio per specificare un livello di esecuzione richiesto di highestAvailable o requireAdministrator, utilizzare questa opzione per specificare il nome del file.  
  
> [!NOTE]
>  Questa opzione e [/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) opzione si escludono a vicenda. Se si tenta di utilizzare entrambe le opzioni nella stessa riga di comando, si otterrà un errore di compilazione.  
  
 Un'applicazione che non ha alcuna applicazione manifesto che specifica che un livello di esecuzione sarà soggetto alla virtualizzazione di file/registro di sistema nella funzionalità controllo Account utente in Windows Vista. Per ulteriori informazioni sulla virtualizzazione, vedere [distribuzione ClickOnce in Windows Vista](https://docs.microsoft.com/visualstudio/deployment/clickonce-deployment-on-windows-vista).  
  
 L'applicazione sarà sottoposto a virtualizzazione se viene soddisfatta una delle seguenti condizioni:  
  
1.  Utilizzare il `/nowin32manifest` opzione e non fornisce un manifesto in una successiva istruzione di compilazione o come parte di un file di risorse di Windows (con estensione res) utilizzando il `/win32resource` (opzione).  
  
2.  Fornire un manifesto personalizzato che non specifica un livello di esecuzione richiesto.  
  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]Crea un file manifesto predefinito e archiviarlo nella directory di debug e release insieme al file eseguibile. È possibile visualizzare o modificare il file app. manifest predefinito facendo clic su **visualizzare le impostazioni di controllo dell'account utente** sul **applicazione** scheda in Progettazione progetti. Per ulteriori informazioni, vedere [pagina applicazione, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
 È possibile fornire il manifesto dell'applicazione come passaggio post-compilazione personalizzato o come parte di un file di risorse Win32 usando il `/nowin32manifest` (opzione). Utilizzare la stessa opzione se si desidera che l'applicazione sia sottoposto a virtualizzazione di file o del Registro di sistema in Windows Vista. Ciò impedirà il compilatore di creare e incorporare un manifesto predefinito nel file PE.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato il manifesto predefinito che il compilatore Visual Basic inserisce in un file PE.  
  
> [!NOTE]
>  Il compilatore inserisce un nome dell'applicazione standard MyApplication. app nel manifesto XML. Si tratta di una soluzione per consentire alle applicazioni per l'esecuzione in Windows Server 2003 Service Pack 3.  
  
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
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/nowin32manifest (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nowin32manifest.md)
