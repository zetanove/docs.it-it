---
title: "Variable &#39;&lt;variablename&gt;&#39; is used before it has been assigned a value | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42104"
  - "BC42104"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42104"
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Variable &#39;&lt;variablename&gt;&#39; is used before it has been assigned a value
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La variabile '\<nomevariabile\>' viene utilizzata prima che le sia stato assegnato un valore.Potrebbe verificarsi un'eccezione di riferimento null in fase di esecuzione.  
  
 Per ogni applicazione esiste almeno un percorso possibile attraverso il codice che permette di effettuare la lettura di una variabile prima che le venga assegnato qualunque valore.  
  
 Se non è mai stato assegnato alcun valore a una variabile, essa utilizza il valore predefinito per il suo tipo di dati.  Per un tipo di dati di riferimento, tale valore corrisponde a [Nothing](../../../visual-basic/language-reference/nothing.md).  In alcune circostanze, la lettura di una variabile di riferimento con valore `Nothing` può generare un'eccezione <xref:System.NullReferenceException>.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42104  
  
### Per correggere l'errore  
  
-   Verificare la logica del flusso di controllo e accertarsi che la variabile abbia un valore valido prima che il controllo venga passato a qualsiasi istruzione che la leggerà.  
  
-   Un metodo per essere certi che la variabile abbia sempre un valore valido consiste nell'inizializzarla come parte della relativa dichiarazione.  Per ulteriori informazioni, vedere "Inizializzazione" in [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md).  
  
## Vedere anche  
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Dichiarazione di variabili](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Risoluzione dei problemi relativi alle variabili](../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)