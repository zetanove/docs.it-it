---
title: Lettura e scrittura nel Registro di sistema mediante lo spazio dei nomi Microsoft.Win32 (Visual Basic) | Documentazione Microsoft
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
- registry, Visual Basic
ms.assetid: 4a0dcce0-c27b-4199-baa8-ee4528da6a56
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2243630d940035046aae9a4c50bcdba3c15f7210
ms.lasthandoff: 03/13/2017

---
# <a name="reading-from-and-writing-to-the-registry-using-the-microsoftwin32-namespace-visual-basic"></a>Lettura e scrittura nel Registro di sistema mediante lo spazio dei nomi Microsoft.Win32 (Visual Basic)
Sebbene `My.Computer.Registry` dovrebbe soddisfare le esigenze di base della programmazione con il Registro di sistema, è possibile usare anche le classi <xref:Microsoft.Win32.Registry> e <xref:Microsoft.Win32.RegistryKey> nello spazio dei nomi <xref:Microsoft.Win32> di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
## <a name="keys-in-the-registry-class"></a>Chiavi nella classe Registry  
 La classe <xref:Microsoft.Win32.Registry> include le chiavi di base del Registro di sistema che è possibile usare per accedere alle sottochiavi e ai relativi valori. Le chiavi di base sono di sola lettura. La tabella seguente elenca e descrive le sette chiavi esposte dalla classe <xref:Microsoft.Win32.Registry>.  
  
|**Key**|**Descrizione**|  
|-------------|---------------------|  
|<xref:Microsoft.Win32.Registry.ClassesRoot>|Definisce i tipi di documento e le relative proprietà.|  
|<xref:Microsoft.Win32.Registry.CurrentConfig>|Contiene informazioni non specifiche dell'utente sulla configurazione hardware.|  
|<xref:Microsoft.Win32.Registry.CurrentUser>|Contiene informazioni sulle preferenze dell'utente corrente, ad esempio le variabili di ambiente.|  
|<xref:Microsoft.Win32.Registry.DynData>|Contiene i dati dinamici del Registro di sistema, ad esempio quelli usati dai driver delle periferiche virtuali.|  
|<xref:Microsoft.Win32.Registry.LocalMachine>|Contiene cinque sottochiavi (Hardware, SAM, Security, Software e System) in cui sono disponibili i dati di configurazione relativi al computer locale.|  
|<xref:Microsoft.Win32.Registry.PerformanceData>|Contiene informazioni sulle prestazioni per i componenti software.|  
|<xref:Microsoft.Win32.Registry.Users>|Contiene informazioni sulle preferenze predefinite degli utenti.|  
  
> [!IMPORTANT]
>  È più sicuro scrivere i dati sull'utente corrente (<xref:Microsoft.Win32.Registry.CurrentUser>) che sul computer locale (<xref:Microsoft.Win32.Registry.LocalMachine>). Quando la chiave che si sta creando è stata precedentemente creata da un altro processo, probabilmente dannoso, si verifica una condizione comunemente definita "squatting". Per evitare che si verifichi tale situazione, usare un metodo, ad esempio <xref:Microsoft.Win32.RegistryKey.GetValue%2A>, che restituisce `Nothing` se la chiave non esiste già.  
  
## <a name="reading-a-value-from-the-registry"></a>Lettura di un valore dal Registro di sistema  
 Il codice seguente illustra come leggere una stringa da HKEY_CURRENT_USER.  
  
 [!code-vb[VbResourceTasks#20](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/reading-from-and-writing-to-the-registry-using-the-microsoft-win32-namespace_1.vb)]  
  
 Il codice seguente legge, incrementa e quindi scrive una stringa in HKEY_CURRENT_USER.  
  
 [!code-vb[VbResourceTasks#21](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/reading-from-and-writing-to-the-registry-using-the-microsoft-win32-namespace_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.SystemException>   
 <xref:System.ApplicationException>   
 <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>   
 [Istruzione Try...Catch...Finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Lettura e scrittura nel Registro di sistema](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)   
 [Sicurezza e Registro di sistema](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)
