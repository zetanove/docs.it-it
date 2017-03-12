---
title: "/bugreport | Microsoft Docs"
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
  - "-bugreport compiler option [Visual Basic]"
  - "bugreport compiler option [Visual Basic]"
  - "/bugreport compiler option [Visual Basic]"
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# /bugreport
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Crea un file utilizzabile quando si genera un report sui bug.  
  
## Sintassi  
  
```  
/bugreport:file  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`file`|Obbligatorio.  Nome del file che conterrà il report sui bug.  Racchiudere il nome del file tra virgolette \(" "\) se contiene uno spazio.|  
  
## Note  
 Le informazioni riportati di seguito vengono aggiunte a `file`:  
  
-   Una copia di tutti i file di codice sorgente della compilazione.  
  
-   Un elenco delle opzioni del compilatore utilizzate nella compilazione.  
  
-   Informazioni sulla versione del compilatore in uso, su Common Language Runtime e sul sistema operativo.  
  
-   Eventuale output del compilatore.  
  
-   Una descrizione del problema, richiesta mediante un messaggio.  
  
-   Una descrizione, richiesta mediante un messaggio, delle possibili modalità di correzione del problema.  
  
 Poiché in `file` viene inserita una copia di tutti i file di codice sorgente, è possibile riprodurre il presunto errore di codice nel programma più breve.  
  
> [!IMPORTANT]
>  L'opzione `/bugreport` genera un file che contiene informazioni potenzialmente riservate,  tra cui ora corrente, versione del compilatore, versione di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] versione del sistema operativo, nome utente, argomenti della riga di comando con cui viene eseguito il compilatore, codice sorgente e formato binario di qualsiasi assembly a cui si fa riferimento.  A questa opzione è possibile accedere specificando le opzioni della riga di comando nel file Web.config per una compilazione sul lato server di un'applicazione [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp-md.md)].  Per evitare questa operazione, modificare il file Machine.config per non consentire agli utenti di eseguire operazioni di compilazione sul server.  
  
 Se questa opzione viene utilizzata con `/errorreport:prompt`, `/errorreport:queue` o `/errorreport:send` e nell'applicazione viene rilevato un errore interno del compilatore, le informazioni contenute in `file` verranno inviate a Microsoft Corporation.  Tali informazioni consentiranno al personale del supporto tecnico Microsoft di identificare la causa dell'errore e di apportare eventuali migliorie alla versione successiva di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Per impostazione predefinita, non vengono inviate informazioni a Microsoft.  Tuttavia, durante la compilazione di un'applicazione con `/errorreport:queue`, la cui attivazione è predefinita, i report degli errori vengono raccolti automaticamente nell'applicazione.  Di conseguenza, all'accesso dell'amministratore, viene visualizzata una finestra popup dal sistema di segnalazione degli errori, che consente all'amministratore stesso di inoltrare a Microsoft i report degli errori generati dopo l'accesso.  
  
> [!NOTE]
>  L'opzione `/bugreport` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Nell'esempio riportato di seguito viene compilato `T2.vb` e tutte le informazioni di segnalazione bug vengono inserite nel file `Problem.txt`.  
  
```  
vbc /bugreport:problem.txt t2.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/debug](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [\/errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Elemento trustLevel per securityPolicy \(schema delle impostazioni ASP.NET\)](http://msdn.microsoft.com/it-it/729ab04c-03da-4ee5-86b1-be9d08a09369)