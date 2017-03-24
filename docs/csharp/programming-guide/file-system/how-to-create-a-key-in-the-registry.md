---
title: "Procedura: creare una chiave nel Registro di sistema (Visual C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "chiavi, creazione nel registro di sistema"
  - "chiavi del Registro di sistema, creazione [C#]"
  - "Registro di sistema, aggiunta di chiavi e valori [C#]"
ms.assetid: 8fa475b0-e01f-483a-9327-fd03488fdf5d
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Procedura: creare una chiave nel Registro di sistema (Visual C#)
Nell'esempio riportato di seguito viene aggiunta la coppia di valori "Name" e "Isabella" al Registro di sistema dell'utente corrente, nella chiave "Names".  
  
## Esempio  
  
```  
Microsoft.Win32.RegistryKey key;  
key = Microsoft.Win32.Registry.CurrentUser.CreateSubKey("Names");  
key.SetValue("Name", "Isabella");  
key.Close();  
```  
  
## Compilazione del codice  
  
-   Copiare il codice e incollarlo nel metodo `Main` di un'applicazione console.  
  
-   Sostituire il parametro `Names` con il nome di una chiave esistente direttamente nel nodo HKEY\_CURRENT\_USER del Registro di sistema.  
  
-   Sostituire il parametro `Nam`e con il nome di un valore esistente direttamente nel nodo Names.  
  
## Programmazione efficiente  
 Esaminare la struttura del Registro di sistema per individuare un percorso adatto per la chiave.  È possibile ad esempio aprire la chiave Software dell'utente corrente e creare una chiave con il nome della propria società,  quindi aggiungere i valori del Registro di sistema alla chiave della società.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è null.  
  
-   L'utente non dispone di autorizzazioni per la creazione delle chiavi del Registro di sistema.  
  
-   Il nome della chiave supera il limite di 255 caratteri.  
  
-   La chiave è chiusa.  
  
-   La chiave del Registro di sistema è di sola lettura.  
  
## Sicurezza di .NET Framework  
 È più sicuro scrivere i dati nella cartella dell'utente, ovvero `Microsoft.Win32.Registry.CurrentUser`, anziché nel computer locale, ovvero `Microsoft.Win32.Registry.LocalMachine`.  
  
 Quando si crea un valore del Registro di sistema, è necessario decidere come procedere nel caso in cui tale valore esista già.  È possibile che un altro processo, forse dannoso, abbia già creato il valore e possa accedervi.  I dati collocati nel valore del Registro di sistema sono disponibili per altri processi.  Per evitare che ciò accada, utilizzare il metodo `Overload:Microsoft.Win32.RegistryKey.GetValue`,  che restituisce null se la chiave non esiste già.  
  
 Archiviare come testo nel Registro di sistema informazioni riservate, quali le password, può presentare dei rischi, anche se la chiave del Registro di sistema è protetta da elenchi di controllo di accesso \(ACL, Access Control List\).  
  
## Vedere anche  
 <xref:System.IO?displayProperty=fullName>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)   
 [Leggere, scrivere ed eliminare dal Registro di sistema con C\#](http://www.codeproject.com/Articles/3389/Read-write-and-delete-from-registry-with-C)