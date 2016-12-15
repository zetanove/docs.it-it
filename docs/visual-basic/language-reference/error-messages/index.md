---
title: "Error Messages (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "errors [Visual Basic]"
  - "error messages"
  - "trappable errors"
  - "errors [Visual Basic], trappable"
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Error Messages (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando si scrivono, le compilazioni, o si esegue un'applicazione Visual Basic, i seguenti tipi di errori possono verificarsi:  
  
1.  Errori in fase di progettazione, che si verificano quando si scrive un'applicazione in Visual Studio.  
  
2.  Errori in fase di compilazione, che si verificano quando si compila un'applicazione in Visual Studio o da un prompt dei comandi.  
  
3.  Errori di runtime, che si verificano quando si esegue un'applicazione in Visual Studio o come file eseguibile autonomo.  
  
 Per informazioni sulla risoluzione di un errore specifico, vedere [Additional Resources for Visual Basic Programmers](../../../visual-basic/getting-started/additional-resources.md).  
  
## Errori di runtime  
 Se un'applicazione Visual Basic tenta di eseguire un'azione che il sistema non può eseguire, si verifica un errore di runtime e genera [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] un oggetto `Exception`.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] può generare errori personalizzati di ogni tipo di dati, inclusi gli oggetti `Exception`, tramite l'istruzione `Throw`.  Un'applicazione può identificare l'errore per visualizzare il numero errore e il messaggio di un'eccezione intercettata.  Se non viene rilevato alcun errore, l'applicazione termina.  
  
 Il codice può intercettare e analizzare errori di runtime.  Se si include il codice che produce l'errore in un blocco `Try`, è possibile rilevare qualsiasi errore generato all'interno di un blocco corrispondente `Catch`.  Per informazioni su come intercettare errori in fase di esecuzione e rispondere a essi nel codice, vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## Errori in fase di compilazione  
 Se il compilatore Visual Basic si verifica un problema nel codice, un errore in fase di compilazione si verifica.  Nell'editor di codice, è possibile identificare facilmente la riga di codice ha causato l'errore poiché una sottolineatura ondulata sotto la riga di codice.  Il messaggio di errore viene visualizzato se si punta la linea ondulata o si apre **Elenco errori**, che mostra anche altri messaggi.  
  
 Se un identificatore è una linea ondulata e una sottolineatura breve sotto il carattere all'estrema destra, è possibile generare uno stub per una classe, un costruttore, un metodo, una proprietà, un campo o un'enumerazione.  Per ulteriori informazioni, vedere [Generazione dall'utilizzo](/visual-cpp/misc/generate-from-usage).  
  
 Risolvere gli avvisi dal compilatore Visual Basic, è possibile scrivere il codice che viene eseguito più velocemente e ha meno bug.  Questi avvisi identificano il codice che potrebbero generare errori quando l'applicazione viene eseguita.  Ad esempio, il compilatore segnala se si tenta di richiamare un membro di una variabile oggetto non assegnata, viene restituito da una funzione senza impostare il valore restituito, o per eseguire un blocco `Try` con errori nella logica per intercettare eccezioni.  Per ulteriori informazioni sugli avvisi, inclusi come attivarli e chiuderlo, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).