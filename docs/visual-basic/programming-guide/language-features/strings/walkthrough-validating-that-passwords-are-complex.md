---
title: "Walkthrough: Validating That Passwords Are Complex (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "String data type, validation"
ms.assetid: 5d9a918f-6c1f-41a3-a019-b5c2b8ce0381
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Validating That Passwords Are Complex (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Questo metodo verifica se sono presenti determinate caratteristiche di password complessa e aggiorna un parametro di tipo stringa con informazioni sui controlli che la password non supera.  
  
 Le password vengono utilizzate in un sistema protetto per autorizzare un utente.  Per gli utenti non autorizzati, tuttavia, deve essere difficile indovinare una password.  Gli intrusi possono utilizzare un programma di *attacco con dizionario* che scorre tutte le parole di un dizionario, o di molti dizionari in lingue diverse, verificando se una delle parole funziona come password utente.  Password vulnerabili come "Americani" o "Mustang" sono facili da indovinare.  Password più complesse, quali "?Ale'L1N3vaFiNdMeyeP@sSWerd\!", verranno indovinate con molta più fatica.  In un sistema protetto con password è essenziale verificare che gli utenti scelgano password complesse.  
  
 Una password complessa contiene una combinazione di caratteri maiuscoli, minuscoli, numerici e speciali, e non è una parola.  Nell'esempio seguente viene mostrato come verificare la complessità di una password.  
  
## Esempio  
  
### Codice  
 [!code-vb[VbVbcnRegEx#1](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/VisualBasic/walkthrough-validating-that-passwords-are-complex_1.vb)]  
  
## Compilazione del codice  
 Chiama questo metodo passando la stringa che contiene la password.  
  
 L'esempio presenta i seguenti requisiti:  
  
-   Accesso ai membri dello spazio dei nomi <xref:System.Text.RegularExpressions>.  Aggiungere un'istruzione `Imports` se i nomi dei membri all'interno del codice non sono specificati in modo completo.  Per ulteriori informazioni, vedere [Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
## Sicurezza  
 Se si sta spostando una password su una rete, è necessario utilizzare un metodo sicuro per trasferire i dati.  Per ulteriori informazioni, vedere [ASP.NET Web Application Security](../Topic/ASP.NET%20Web%20Application%20Security.md).  
  
 È possibile migliorare la precisione della funzione `ValidatePassword` aggiungendo dei controlli di complessità supplementari:  
  
-   Confrontare la password e le sue sottostringhe con il nome e l'identificativo dell'utente e un dizionario definito dall'applicazione.  Inoltre, considerare i caratteri visivamente simili come equivalenti quando si esegue il confronto.  Ad esempio, considerare le lettere "l" ed "e" come equivalenti ai numeri "1" e "3".  
  
-   Se viene utilizzato un solo carattere maiuscolo, accertarsi che non sia il primo carattere della password.  
  
-   Verificare che gli ultimi due caratteri della password siano delle lettere.  
  
-   Non consentire l'utilizzo di password in cui tutti i simboli sono stati immessi dalla prima riga della tastiera.  
  
## Vedere anche  
 <xref:System.Text.RegularExpressions.Regex>   
 [ASP.NET Web Application Security](../Topic/ASP.NET%20Web%20Application%20Security.md)