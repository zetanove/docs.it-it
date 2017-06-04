---
title: Prompt dei comandi per gli sviluppatori per Visual Studio | Documenti di Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- command prompt, Windows SDK
- Visual Studio command prompt
- command prompt, Visual Studio
- SDK command prompt
- tools [.NET Framework], setting environment variables
- environment variables, setting for tools
- developer command prompt
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
caps.latest.revision: 45
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 6138fab11f30fdee646768ce807fbdba57fcabb3
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="developer-command-prompt-for-visual-studio"></a>Prompt dei comandi per gli sviluppatori per Visual Studio
Il prompt dei comandi per gli sviluppatori per Visual Studio imposta automaticamente le variabili di ambiente che consentono di usare facilmente gli strumenti di .NET Framework. Il prompt dei comandi per gli sviluppatori viene installato con le versioni complete o della Community di Visual Studio. Non viene installato con le versioni Express di Visual Studio.  
  
<a name="find"></a>   
## <a name="searching-for-the-command-prompt-on-your-machine"></a>Ricerca del prompt dei comandi nel computer  
 Si potrebbero notare più prompt dei comandi, in base alla versione di Visual Studio e agli SDK aggiuntivi installati. Ad esempio, le versioni a 64 bit di Visual Studio forniscono prompt dei comandi sia a 32 bit che a 64 bit. Le versioni a 32 bit e a 64 bit della maggior parte degli strumenti sono identiche; tuttavia, alcuni strumenti apportano modifiche specifiche per gli ambienti a 32 bit e a 64 bit. Se i passaggi seguenti non funzionano, è possibile provare [Individuazione manuale dei file nel computer](#alternative) o [Esecuzione del prompt dei comandi dall'interno di Visual Studio](#visualstudio).  
  
 **In Windows 10**  
  
1.  Aprire il menu **Start** premendo il tasto del ![logo Windows](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") sulla tastiera.  
  
2.  Nel menu **Start** immettere `dev`. Verrà visualizzato un elenco di app installate che corrispondono ai criteri di ricerca. Se si sta cercando un prompt dei comandi diverso, provare a immettere un termine di ricerca diverso, ad esempio `prompt`.  
  
3.  Scegliere **Prompt dei comandi per gli sviluppatori** (o il prompt dei comandi che si vuole usare).  
  
 **In Windows 8.1**  
  
1.  Aprire la schermata **Start** premendo il tasto del ![logo Windows](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") sulla tastiera.  
  
2.  Nella schermata **Start** premere `CTRL + TAB` per aprire l'elenco **App** e quindi immettere `V`. Verrà visualizzato un elenco che include tutti i prompt dei comandi di Visual Studio installati.  
  
3.  Scegliere **Prompt dei comandi per gli sviluppatori** (o il prompt dei comandi che si vuole usare).  
  
 **In Windows 8**  
  
1.  Aprire la schermata **Start** premendo il tasto del ![logo Windows](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") sulla tastiera.  
  
2.  Nella schermata **Start** premere il tasto del ![logo Windows](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") `+ Z`.  
  
3.  Scegliere l'icona **Visualizzazione App** nella parte inferiore della schermata e quindi immettere `V`. Verrà visualizzato un elenco che include tutti i prompt dei comandi di Visual Studio installati.  
  
4.  Scegliere **Prompt dei comandi per gli sviluppatori** (o il prompt dei comandi che si vuole usare).  
  
 **In Windows 7**  
  
1.  Scegliere **Start**, espandere **Tutti i programmi** e quindi espandere **Microsoft Visual Studio**.  
  
2.  A seconda della versione di Visual Studio installata, scegliere **Strumenti di Visual Studio**, **Prompt dei comandi di Visual Studio** o il prompt dei comandi che si vuole usare.  
  
 Se è installato [Windows SDK](http://msdn.microsoft.com/windows/desktop/aa904949) o [Windows Phone SDK](https://dev.windowsphone.com/downloadsdk), è possibile visualizzare prompt dei comandi aggiuntivi per le architetture ARM, x86 o x64. Consultare la documentazione dei diversi strumenti per determinare quale versione del prompt dei comandi usare.  
  
<a name="alternative"></a>   
## <a name="manually-locating-the-files-on-your-machine"></a>Individuazione manuale dei file nel computer  
  In genere, i collegamenti per i prompt dei comandi installati verranno posizionati nella cartella **Menu Start** per Visual Studio, ad esempio in C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Visual Studio 2015\Visual Studio Tools.    Tuttavia, se per qualche motivo la ricerca del prompt dei comandi non produce i risultati previsti, è possibile provare a trovare manualmente il collegamento nel computer.   Provare a cercare il nome del file del prompt dei comandi, ad esempio VsDevCmd.bat o passare alla cartella strumenti, ad esempio C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools (il percorso cambierà a seconda del percorso di installazione e della versione di Visual Studio).  
  
<a name="visualstudio"></a>   
## <a name="running-command-prompt-from-inside-visual-studio"></a>Esecuzione del prompt dei comandi dall'interno di Visual Studio  
 Per semplificare l'accesso, è possibile aggiungere il prompt dei comandi per gli sviluppatori Visual Studio o qualsiasi altro prompt dei comandi al menu Strumenti in Visual Studio aggiungendolo all'elenco di strumenti esterni. Di seguito è illustrata la procedura per eseguire questa operazione:  
  
1.  Aprire Visual Studio.  
  
2.  Selezionare il menu **Strumenti** e scegliere **Strumenti esterni...**.  
  
3.  Nella finestra di dialogo **Strumenti esterni** scegliere il pulsante **Aggiungi**. Verrà visualizzata una nuova voce.  
  
4.  Immettere un **titolo** per la nuova voce di menu, ad esempio `Command Prompt`.  
  
5.  Nel campo **Comando** specificare il file che si vuole avviare, ad esempio `%comspec%` o `C:\Windows\System32\cmd.exe` .  
  
6.  Nel campo **Argomenti** specificare dove trovare il prompt dei comandi specifico da usare, ad esempio `/k "C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\VsDevCmd.bat"` (verrà avviato il prompt dei comandi per sviluppatori installato con [!INCLUDE[vs_dev14](../../../includes/vs-dev14-md.md)]). Questo valore deve essere modificato in base al percorso di installazione e alla versione di Visual Studio.  
  
7.  Scegliere un valore per il campo **Directory iniziale**, ad esempio **Directory di progetto**.  
  
8.  Fare clic sul pulsante **OK** .  
  
 Successivamente, viene aggiunta la nuova voce di menu ed è possibile accedere al prompt dei comandi dal menu **Strumenti**.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti](../../../docs/framework/tools/index.md)   
 [Gestione di strumenti esterni](/visualstudio/ide/managing-external-tools)
