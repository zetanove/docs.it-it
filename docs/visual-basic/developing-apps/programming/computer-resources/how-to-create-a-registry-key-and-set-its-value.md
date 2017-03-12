---
title: "How to: Create a Registry Key and Set Its Value in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "RegistryKey.CreateSubKey"
  - "RegistryKey.SetValue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "registry keys, creating"
  - "registry, adding values"
  - "registry, adding keys"
  - "registry keys, setting values"
  - "examples [Visual Basic], registry"
ms.assetid: d3e40f74-c283-480c-ab18-e5e9052cd814
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# How to: Create a Registry Key and Set Its Value in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il metodo `CreateSubKey` dell'oggetto `My.Computer.Registry` consente di creare una chiave del Registro di sistema.  
  
## Procedura  
  
#### Per creare una chiave del Registro di sistema  
  
-   Utilizzare il metodo `CreateSubKey` specificando l'hive in cui inserire la chiave, nonché il nome della chiave.  Per il parametro `Subkey` non viene effettuata distinzione tra maiuscole e minuscole.  Nell'esempio che segue viene creata la chiave del Registro di sistema `MyTestKey` al di sotto di HKEY\_CURRENT\_USER.  
  
     [!code-vb[VbResourceTasks#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-create-a-registry_1.vb)]  
  
#### Per creare una chiave del Registro di sistema e impostare un valore al suo interno  
  
1.  Utilizzare il metodo `CreateSubkey` specificando l'hive in cui inserire la chiave, nonché il nome della chiave.  Nell'esempio che segue viene creata la chiave del Registro di sistema `MyTestKey` al di sotto di HKEY\_CURRENT\_USER.  
  
     [!code-vb[VbResourceTasks#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-create-a-registry_1.vb)]  
  
2.  Impostare il valore con il metodo `SetValue`.  Nell'esempio che segue viene impostato il valore stringa    MyTestKeyValue" su "This is a test value".  
  
     [!code-vb[VbResourceTasks#14](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-create-a-registry_2.vb)]  
  
## Esempio  
 Nell'esempio che segue viene creata la chiave del Registro di sistema `MyTestKey` al di sotto di HKEY\_CURRENT\_USER, quindi viene impostato il valore stringa `MyTestKeyValue` su `This is a test value`.  
  
 [!code-vb[VbResourceTasks#15](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-create-a-registry_3.vb)]  
  
## Programmazione efficiente  
 Esaminare la struttura del Registro di sistema per individuare un percorso adatto per la chiave.  È ad esempio possibile aprire la chiave HKEY\_CURRENT\_USER\\Software dell'utente corrente e creare una chiave con il nome della società,  quindi aggiungere i valori del Registro di sistema alla chiave della società.  
  
 Durante la lettura del Registro di sistema da un'applicazione Web, l'utente corrente dipende dall'autenticazione e dalla rappresentazione implementate nell'applicazione Web.  
  
 È più sicuro scrivere i dati nella cartella dell'utente \(<xref:Microsoft.Win32.Registry.CurrentUser>\) anziché nel computer locale \(<xref:Microsoft.Win32.Registry.LocalMachine>\).  
  
 Quando si crea un valore del Registro di sistema, è necessario decidere come procedere nel caso in cui tale valore esista già.  È possibile che un altro processo, forse dannoso, abbia già creato il valore e possa accedervi.  I dati collocati nel valore del Registro di sistema sono disponibili per altri processi.  Per evitare tale situazione, utilizzare il metodo <xref:Microsoft.Win32.RegistryKey.GetValue%2A>.  che restituisce `Nothing` se la chiave non esiste già.  
  
 Memorizzare come testo nel Registro di sistema informazioni riservate, quali le password, può presentare dei rischi, anche se la chiave del  Registro di sistema è protetta da elenchi di controllo di accesso \(ACL, Access Control List\).  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è `Nothing` \(<xref:System.ArgumentNullException>\).  
  
-   L'utente non dispone di autorizzazioni per la creazione delle chiavi del Registro di sistema \(<xref:System.Security.SecurityException>\).  
  
-   Il nome della chiave supera il limite di 255 caratteri \(<xref:System.ArgumentException>\).  
  
-   La chiave è chiusa \(<xref:System.IO.IOException>\).  
  
-   La chiave del Registro di sistema è di sola lettura \(<xref:System.UnauthorizedAccessException>\).  
  
## Sicurezza di .NET Framework  
 Per eseguire questo processo, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.RegistryPermission>.  Se viene eseguito in un contesto ad affidabilità parziale, il processo può generare un'eccezione a causa dell'insufficienza di privilegi.  Allo stesso modo, l'utente deve disporre degli ACL corretti per la creazione o la scrittura nelle impostazioni.  Un'applicazione locale che dispone dell'autorizzazione di sicurezza per l'accesso di codice potrebbe ad esempio non disporre dell'autorizzazione del sistema operativo.  Per ulteriori informazioni, vedere [Code Access Security Basics](../Topic/Code%20Access%20Security%20Basics.md).  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy.CurrentUser%2A>   
 <xref:Microsoft.Win32.RegistryKey.CreateSubKey%2A>   
 [Reading from and Writing to the Registry](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)   
 [Code Access Security Basics](../Topic/Code%20Access%20Security%20Basics.md)