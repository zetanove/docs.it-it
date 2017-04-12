---
title: 'Procedura: Leggere un valore da una chiave del Registro di sistema in Visual Basic | Microsoft Docs'
ms.custom: 
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
- registry keys, determining if a value exists in
- My.Computer.Registry object, examples
- registry, determining if values exist
- registry keys, reading from
- registry, reading
ms.assetid: 775d0a57-68c9-464e-8949-9a39bd29cc64
caps.latest.revision: 31
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e68cde6d56d4de584861b8bcf29e072a5fc18928
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-a-value-from-a-registry-key-in-visual-basic"></a>Procedura: leggere un valore da una chiave del Registro di sistema in Visual Basic
Il metodo `GetValue` dell'oggetto `My.Computer.Registry` può essere usato per leggere i valori nel Registro di sistema di Windows.  
  
 Se la chiave, "Software\MyApp" nell'esempio seguente, non esiste, viene generata un'eccezione. Se `ValueName`,  "Name" nell'esempio seguente, non esiste, viene restituito `Nothing`.  
  
 Il metodo `GetValue` può essere usato anche per determinare se esiste un determinato valore in una chiave del Registro di sistema specifica.  
  
 Quando il codice legge il Registro di sistema da un'applicazione Web, l'utente corrente viene determinato tramite l'autenticazione e la rappresentazione implementata nell'applicazione Web.  
  
### <a name="to-read-a-value-from-a-registry-key"></a>Per leggere un valore da una chiave del Registro di sistema  
  
-   Usare il metodo `GetValue` (specificando il percorso e il nome) per leggere un valore dalla chiave del Registro di sistema. L'esempio seguente legge il valore `Name` da `HKEY_CURRENT_USER\Software\MyApp` e lo visualizza in una finestra di messaggio.  
  
     [!code-vb[VbResourceTasks#4](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-read-a-value-from-a-registry-key_1.vb)]  
  
 Questo esempio di codice è disponibile anche come frammento di codice IntelliSense. Nello strumento di selezione dei frammenti di codice il frammento si trova in **Sistema operativo Windows > Registro di sistema**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
### <a name="to-determine-whether-a-value-exists-in-a-registry-key"></a>Per determinare se esiste un valore in una chiave del Registro di sistema  
  
-   Usare il metodo `GetValue` per recuperare il valore. Il codice seguente controlla se il valore esiste e restituisce un messaggio se il valore non esiste.  
  
     [!code-vb[VbResourceTasks#12](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-read-a-value-from-a-registry-key_2.vb)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Nel Registro di sistema sono contenute chiavi di primo livello, o radice, usate per memorizzare i dati. Ad esempio, la chiave radice HKEY_LOCAL_MACHINE è usata per memorizzare le impostazioni a livello di computer usate da tutti gli utenti, mentre la chiave HKEY_CURRENT_USER viene usata per memorizzare i dati specifici di un singolo utente.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   L'utente non ha le autorizzazioni per la lettura delle chiavi del Registro di sistema (<xref:System.Security.SecurityException>).  
  
-   Il nome della chiave supera il limite di 255 caratteri (<xref:System.ArgumentException>).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Per eseguire questo processo, l'assembly richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.RegistryPermission>. Se viene eseguito in un contesto parzialmente attendibile, il processo potrebbe generare un'eccezione a causa di privilegi insufficienti. Allo stesso modo, l'utente deve disporre degli ACL corretti per la creazione o la scrittura nelle impostazioni. Ad esempio, un'applicazione locale che ha l'autorizzazione di sicurezza dall'accesso di codice potrebbe non avere l'autorizzazione del sistema operativo. Per altre informazioni, vedere [Code Access Security Basics](https://msdn.microsoft.com/library/33tceax8) (Nozioni di base sulla sicurezza dell'accesso di codice).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 <xref:Microsoft.Win32.RegistryHive>   
 [Lettura e scrittura nel Registro di sistema](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
