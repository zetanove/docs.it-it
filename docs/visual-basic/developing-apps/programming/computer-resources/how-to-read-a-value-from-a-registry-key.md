---
title: "How to: Read a Value from a Registry Key in Visual Basic | Microsoft Docs"
ms.custom: ""
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
  - "registry keys, determining if a value exists in"
  - "My.Computer.Registry object, examples"
  - "registry, determining if values exist"
  - "registry keys, reading from"
  - "registry, reading"
ms.assetid: 775d0a57-68c9-464e-8949-9a39bd29cc64
caps.latest.revision: 31
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 31
---
# How to: Read a Value from a Registry Key in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il metodo `GetValue` dell'oggetto `My.Computer.Registry` consente di leggere valori nel Registro di sistema di Windows.  
  
 Se la chiave, “software \\MyApp„ nell' esempio seguente, non esiste, viene generata un'eccezione.  Se `ValueName`, “nome„ nell' esempio seguente, non esiste, `Nothing` viene restituito.  
  
 Il metodo di `GetValue` può essere utilizzato per determinare se un valore specificato è presente in una chiave specifica del Registro di sistema.  
  
 Quando il codice viene letto il Registro di sistema da un'applicazione Web, l'utente corrente è determinato dall' autenticazione e dalla rappresentazione che viene implementata nell' applicazione Web.  
  
### Per leggere un valore da una chiave del Registro di sistema  
  
-   Utilizzare il metodo `GetValue`, specificando il percorso e il nome, per leggere un valore dalla chiave del Registro di sistema.  Nell'esempio che segue il valore `Name` viene letto da `HKEY_CURRENT_USER\Software\MyApp` e visualizzato in una finestra di messaggio.  
  
     [!code-vb[VbResourceTasks#4](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-read-a-value-from_1.vb)]  
  
 Questo esempio di codice è inoltre disponibile come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice si trova in **Sistema operativo Windows \> Registro di sistema**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
### Per determinare se un valore è presente in una chiave del Registro di sistema  
  
-   Utilizzare il metodo `GetValue` per recuperare il valore.  I controlli di codice se il valore è presente e restituisce un messaggio in caso contrario.  
  
     [!code-vb[VbResourceTasks#12](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-read-a-value-from_2.vb)]  
  
## Programmazione efficiente  
 Il Registro di sistema contiene le chiavi di primo livello che vengono utilizzate per l'archiviazione dei dati.  La chiave di primo livello HKEY\_LOCAL\_MACHINE viene ad esempio utilizzata per archiviare le impostazioni a livello di computer impiegate da tutti gli utenti, mentre HKEY\_CURRENT\_USER viene utilizzata per l'archiviazione dei dati specifici di un singolo utente.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   L'utente non dispone di autorizzazioni per la lettura dalle chiavi del Registro di sistema \(<xref:System.Security.SecurityException>\).  
  
-   Il nome della chiave supera il limite di 255 caratteri \(<xref:System.ArgumentException>\).  
  
## Sicurezza di .NET Framework  
 Per eseguire questo processo, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.RegistryPermission>.  Se viene eseguito in un contesto ad affidabilità parziale, il processo può generare un'eccezione a causa dell'insufficienza di privilegi.  Allo stesso modo, l'utente deve disporre degli ACL corretti per la creazione o la scrittura nelle impostazioni.  Un'applicazione locale che dispone dell'autorizzazione di sicurezza per l'accesso di codice potrebbe ad esempio non disporre dell'autorizzazione del sistema operativo.  Per ulteriori informazioni, vedere [Code Access Security Basics](../Topic/Code%20Access%20Security%20Basics.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 <xref:Microsoft.Win32.RegistryHive>   
 [Reading from and Writing to the Registry](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)