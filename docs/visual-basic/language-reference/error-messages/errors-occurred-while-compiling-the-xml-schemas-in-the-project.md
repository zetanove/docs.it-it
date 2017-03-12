---
title: "Errors occurred while compiling the XML schemas in the project | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36810"
  - "vbc36810"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36810"
ms.assetid: 9323b5d2-ba14-4e49-91f1-9ad647162144
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Errors occurred while compiling the XML schemas in the project
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Errori durante la compilazione degli schemi XML nel progetto.Per questo motivo IntelliSense XML non è disponibile.  
  
 È presente un errore in uno schema XSD \(XML Schema Definition\) incluso nel progetto.  Tale errore si verifica quando si aggiunge un file di schema XSD \(.xsd\) che è in conflitto con l'insieme dello schema XSD esistente per il progetto.  
  
 **ID errore:**  BC36810  
  
### Per correggere l'errore  
  
-   Nella finestra **Elenco errori** fare doppio clic sull'avviso.  Verrà visualizzata la posizione nel file XSD che costituisce l'origine dell'avviso.  Correggere l'errore nello schema XSD.  
  
-   Assicurarsi che tutti i file di schema XSD obbligatori \(con estensione xsd\) siano inclusi nel progetto.  Potrebbe essere necessario scegliere **Mostra tutti i file** dal menu **Progetto** per visualizzare i file xsd in **Esplora soluzioni**.  Fare clic con il pulsante destro del mouse su un file xsd, quindi fare clic su **Includi nel progetto** per includere il file nel progetto.  
  
-   Se si utilizza la procedura guidata XML in schema, l'errore può verificarsi quando si esegue più volte l'inferenza di schemi dalla stessa origine.  In tal caso, è possibile rimuovere i file di schema XSD esistenti dal progetto, aggiungere un nuovo modello di elementi di XML in schema, quindi fornire alla procedura guidata XML in schema tutte le origini XML applicabili per il progetto.  
  
-   Se non viene identificato alcun errore nello schema XSD, il compilatore XML non dispone di sufficienti informazioni per fornire un messaggio di errore dettagliato.  Si potrebbero ottenere informazioni più dettagliate sull'errore se si assicura che gli spazi dei nomi XML per i file xsd inclusi nella progetto corrispondano agli spazi dei nomi XML identificati per il linguaggio XML Schema impostato in Visual Studio.  
  
## Vedere anche  
 [Finestra Elenco errori](/visual-studio/ide/reference/error-list-window)   
 [XML IntelliSense in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)