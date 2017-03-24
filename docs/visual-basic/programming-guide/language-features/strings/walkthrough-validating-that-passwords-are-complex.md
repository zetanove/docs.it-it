---
title: "Convalida della complessità delle password (Visual Basic) | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- String data type, validation
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
caps.latest.revision: 17
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: e899900d60bddb83fb640abcc7f11f333c1af870
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-validating-that-passwords-are-complex-visual-basic"></a>Procedura dettagliata: verifica della complessità delle password (Visual Basic)
Questo metodo controlla alcune caratteristiche di password complesse e aggiorna un parametro di stringa con informazioni sui controlli che la password non riesce.  
  
 Le password è utilizzabile in un sistema sicuro per autorizzare un utente. Tuttavia, le password devono essere difficile per gli utenti non autorizzati di indovinare. Gli utenti malintenzionati possono utilizzare un *attacco con dizionario* programma che esegue l'iterazione attraverso tutte le parole in un dizionario (o più dizionari in lingue diverse), verifica se una delle parole funziona come password dell'utente. Password vulnerabili, ad esempio "Yankees" o "Mustang sono facili" può essere individuata rapidamente. Password più complesse, ad esempio "? È 'L1N3vaFiNdMeyeP@sSWerd! ", molto meno probabilità di essere individuato. Un sistema protetto da password è necessario assicurarsi che gli utenti scelgano password complesse.  
  
 Una password complessa è complessa (contenente una combinazione di caratteri maiuscoli, minuscoli, numerici e speciali) e non è una parola. In questo esempio viene illustrato come verificare la complessità.  
  
## <a name="example"></a>Esempio  
  
### <a name="code"></a>Codice  
 [!code-vb[VbVbcnRegEx n.&1;](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/VisualBasic/walkthrough-validating-that-passwords-are-complex_1.vb)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Chiamare questo metodo passando la stringa che contiene la password.  
  
 L'esempio presenta i requisiti seguenti:  
  
-   Accesso ai membri del <xref:System.Text.RegularExpressions>dello spazio dei nomi.</xref:System.Text.RegularExpressions> Aggiungere un `Imports` istruzione se non sono completamente qualifica i nomi dei membri nel codice. Per altre informazioni, vedere [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
## <a name="security"></a>Sicurezza  
 Se si sta spostando la password attraverso una rete, è necessario utilizzare un metodo sicuro per il trasferimento dei dati. Per ulteriori informazioni, vedere [ASP.NET Web Application Security](https://msdn.microsoft.com/library/330a99hc).  
  
 È possibile migliorare l'accuratezza del `ValidatePassword` funzione mediante l'aggiunta di controlli di complessità supplementari:  
  
-   Confrontare la password e le sue sottostringhe con il nome dell'utente, identificatore utente e un dizionario definito dall'applicazione. Inoltre, gestiscono caratteri visivamente simili come equivalenti quando si esegue il confronto. Ad esempio, considerare le lettere "l" e "e" come equivalenti ai numeri "1" e "3".  
  
-   Se è presente un solo carattere maiuscolo, assicurarsi che non è primo carattere della password.  
  
-   Assicurarsi che gli ultimi due caratteri della password sono caratteri lettera.  
  
-   Non consentire password nel quale sono inseriti tutti i simboli dalla prima riga della tastiera.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Text.RegularExpressions.Regex></xref:System.Text.RegularExpressions.Regex>   
 [Protezione delle applicazioni Web ASP.NET](https://msdn.microsoft.com/library/330a99hc)
