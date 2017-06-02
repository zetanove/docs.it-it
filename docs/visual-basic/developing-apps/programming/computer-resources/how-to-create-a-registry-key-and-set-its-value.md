---
title: 'Procedura: Creare una chiave del Registro di sistema e impostarne il valore in Visual Basic | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- RegistryKey.CreateSubKey
- RegistryKey.SetValue
dev_langs:
- VB
helpviewer_keywords:
- registry keys, creating
- registry, adding values
- registry, adding keys
- registry keys, setting values
- examples [Visual Basic], registry
ms.assetid: d3e40f74-c283-480c-ab18-e5e9052cd814
caps.latest.revision: 30
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 28a01911dc715483aee8191972387781a6f1933e
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="how-to-create-a-registry-key-and-set-its-value-in-visual-basic"></a>Procedura: creare una chiave del Registro di sistema e impostarne il valore in Visual Basic
Il metodo `CreateSubKey` dell'oggetto `My.Computer.Registry` consente di creare una chiave del Registro di sistema.  
  
## <a name="procedure"></a>Routine  
  
#### <a name="to-create-a-registry-key"></a>Per creare una chiave del Registro di sistema  
  
-   Usare il metodo `CreateSubKey` specificando l'hive in cui inserire la chiave, nonché il nome della chiave. Per il parametro `Subkey` non esiste distinzione tra maiuscole e minuscole. Nell'esempio che segue viene creata la chiave del Registro di sistema `MyTestKey` in HKEY_CURRENT_USER.  
  
     [!code-vb[VbResourceTasks#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_1.vb)]  
  
#### <a name="to-create-a-registry-key-and-set-a-value-in-it"></a>Per creare una chiave del Registro di sistema e impostarne il valore  
  
1.  Usare il metodo `CreateSubkey` specificando l'hive in cui inserire la chiave, nonché il nome della chiave. Nell'esempio che segue viene creata la chiave del Registro di sistema `MyTestKey` in HKEY_CURRENT_USER.  
  
     [!code-vb[VbResourceTasks#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_1.vb)]  
  
2.  Impostare il valore con il metodo `SetValue`. In questo esempio viene impostato il valore stringa. "MyTestKeyValue" su "This is a test value".  
  
     [!code-vb[VbResourceTasks#14](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_2.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio che segue viene creata la chiave del Registro di sistema `MyTestKey` in HKEY_CURRENT_USER e il valore stringa `MyTestKeyValue` viene impostato su `This is a test value`.  
  
 [!code-vb[VbResourceTasks#15](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-create-a-registry-key-and-set-its-value_3.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Esaminare la struttura del Registro di sistema per individuare un percorso adatto per la chiave. Può essere ad esempio necessario aprire la chiave HKEY_CURRENT_USER\Software dell'utente corrente e creare una chiave con il nome della società, quindi aggiungere i valori del Registro di sistema alla chiave della società stessa.  
  
 Durante la lettura del Registro di sistema da un'applicazione Web, l'utente corrente dipende dall'autenticazione e dalla rappresentazione implementate nell'applicazione Web.  
  
 È più sicuro scrivere i dati nella cartella dell'utente (<xref:Microsoft.Win32.Registry.CurrentUser>) anziché nel computer locale (<xref:Microsoft.Win32.Registry.LocalMachine>).  
  
 Quando si crea un valore del Registro di sistema, è necessario decidere come procedere nel caso in cui tale valore esista già. È possibile che un altro processo, forse dannoso, abbia già creato il valore e possa accedervi. I dati inseriti nel valore del Registro di sistema sono disponibili per altri processi. Per evitare che ciò accada, usare il metodo <xref:Microsoft.Win32.RegistryKey.GetValue%2A>. Restituisce `Nothing` se la chiave non esiste.  
  
 Archiviare come testo nel Registro di sistema informazioni riservate, quali le password, può presentare dei rischi, anche se la chiave del Registro di sistema è protetta da elenchi di controllo di accesso (ACL, Access Control List).  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   L'utente non è autorizzato a creare le chiavi del Registro di sistema (<xref:System.Security.SecurityException>).  
  
-   Il nome della chiave supera il limite di 255 caratteri (<xref:System.ArgumentException>).  
  
-   La chiave è chiusa (<xref:System.IO.IOException>).  
  
-   La chiave del Registro di sistema è di sola lettura (<xref:System.UnauthorizedAccessException>).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Per eseguire questo processo, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.RegistryPermission>. Se viene eseguito in un contesto parzialmente attendibile, il processo potrebbe generare un'eccezione a causa di privilegi insufficienti. Allo stesso modo, l'utente deve disporre degli ACL corretti per la creazione o la scrittura nelle impostazioni. Ad esempio, un'applicazione locale che ha l'autorizzazione di sicurezza dall'accesso di codice potrebbe non avere l'autorizzazione del sistema operativo. Per altre informazioni, vedere [Code Access Security Basics](https://msdn.microsoft.com/library/33tceax8) (Nozioni di base sulla sicurezza dell'accesso di codice).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy.CurrentUser%2A>   
 <xref:Microsoft.Win32.RegistryKey.CreateSubKey%2A>   
 [Lettura e scrittura nel Registro di sistema](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)   
 [Nozioni fondamentali sulla sicurezza per l’accesso al codice](https://msdn.microsoft.com/library/33tceax8)
