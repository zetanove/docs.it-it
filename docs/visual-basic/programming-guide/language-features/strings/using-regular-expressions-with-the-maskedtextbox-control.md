---
title: "Using Regular Expressions with the MaskedTextBox Control in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "strings [Visual Basic], regular expressions"
  - "strings [Visual Basic], masked edit"
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Using Regular Expressions with the MaskedTextBox Control in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo esempio viene illustrato come convertire espressioni regolari semplici da utilizzare con il controllo <xref:System.Windows.Forms.MaskedTextBox>.  
  
## Descrizione del linguaggio di definizione della maschera  
 Il linguaggio di definizione della maschera <xref:System.Windows.Forms.MaskedTextBox> standard è basato su quello utilizzato dal controllo `Masked Edit` in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 6.0 e dovrebbe essere noto agli utenti che eseguono la migrazione da questa piattaforma.  
  
 La proprietà <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> del controllo <xref:System.Windows.Forms.MaskedTextBox> specifica la maschera di input da utilizzare.  È necessario che la maschera sia composta da una stringa di uno o più elementi di definizione della maschera inclusi nella seguente tabella.  
  
|Elemento di definizione della maschera|Descrizione|Elemento di espressione regolare|  
|--------------------------------------------|-----------------|--------------------------------------|  
|0|Qualsiasi cifra tra 0 e 9.  Immissione obbligatoria.|\\d|  
|9|Cifra o spazio.  Immissione facoltativa.|\[ \\d\]?|  
|\#|Cifra o spazio.  Immissione facoltativa.  Se nella maschera questa posizione viene lasciata vuota, il rendering verrà eseguito come spazio.  Sono consentiti i segni più \(\+\) e meno \(\-\).|\[ \\d\+\-\]?|  
|L|Carattere alfabetico ASCII.  Immissione obbligatoria.|\[a\-zA\-Z\]|  
|?|Carattere alfabetico ASCII.  Immissione facoltativa.|\[a\-zA\-Z\]?|  
|&|Character  Immissione obbligatoria.|\[\\p{Ll}\\p{Lu}\\p{Lt}\\p{Lm}\\p{Lo}\]|  
|C|Character  Immissione facoltativa.|\[\\p{Ll}\\p{Lu}\\p{Lt}\\p{Lm}\\p{Lo}\]?|  
|A|Alfanumerico.  Immissione facoltativa.|\\W|  
|.|Segnaposto decimale appropriato per le impostazioni cultura.|Non disponibile.|  
|,|Segnaposto delle migliaia appropriato per le impostazioni cultura.|Non disponibile.|  
|:|Separatore dell'ora appropriato per le impostazioni cultura.|Non disponibile.|  
|\/|Separatore della data appropriato per le impostazioni cultura.|Non disponibile.|  
|$|Simbolo di valuta appropriato per le impostazioni cultura.|Non disponibile.|  
|\<|Converte tutti i caratteri successivi in lettere minuscole.|Non disponibile.|  
|\>|Converte tutti i caratteri successivi in lettere maiuscole.|Non disponibile.|  
|&#124;|Annulla la precedente attivazione o disattivazione del tasto MAIUSC.|Non disponibile.|  
|\\|Esegue l'escape di un carattere della maschera e lo trasforma in un valore letterale.    \\\\" è la sequenza di escape per una barra rovesciata.|\\|  
|Tutti gli altri caratteri.|Valori letterali.  Tutti gli elementi che non appartengono alla definizione di maschera verranno visualizzati come tali nell'oggetto <xref:System.Windows.Forms.MaskedTextBox>.|Tutti gli altri caratteri.|  
  
 I simboli dei decimali \(.\), delle migliaia \(,\), dell'ora \(:\), della data \(\/\) e della valuta \($\) vengono predefiniti in base alle impostazioni cultura dell'applicazione.  Per imporre la visualizzazione dei simboli di altre impostazioni cultura, è possibile utilizzare la proprietà <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A>.  
  
## Espressioni regolari e maschere  
 Sebbene sia possibile utilizzare espressioni regolari e maschere per convalidare l'input dell'utente, le due operazioni non sono del tutto equivalenti.  Le espressioni regolari possono esprimere modelli più complessi rispetto alle maschere, ma queste ultime possono esprimere le stesse informazioni in modo più succinto e in formato più adeguato alla lingua.  
  
 Nella seguente tabella vengono confrontate quattro espressioni regolari e le maschere equivalenti.  
  
|Espressione regolare|Maschera|Note|  
|--------------------------|--------------|----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|Il carattere `/` nella maschera è un separatore di data logico e verrà visualizzato dall'utente come separatore di data appropriato per le impostazioni cultura correnti dell'applicazione.|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|Data \(giorno, abbreviazione del mese, anno\) nel formato utilizzato negli Stati Uniti, in cui le tre lettere di abbreviazione del mese vengono visualizzate con l'iniziale maiuscola seguita da due minuscole.|  
|`(\(\d{3}\)-)?  \d{3}-d{4}`|`(999)-000-0000`|Numero telefonico degli Stati Uniti, prefisso facoltativo.  Se l'utente non desidera immettere i caratteri facoltativi, può immettere spazi o posizionare il puntatore del mouse direttamente nella posizione della maschera rappresentata dal primo 0.|  
|`$\d{6}.00`|`$999,999.00`|Valore della valuta compreso nell'intervallo tra 0 e 999999.  I caratteri della valuta, delle migliaia e dei decimali verranno sostituiti in fase di esecuzione dagli equivalenti specifici per le impostazioni cultura.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>   
 <xref:System.Windows.Forms.MaskedTextBox>   
 [Validating Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)   
 [Controllo MaskedTextBox](../Topic/MaskedTextBox%20Control%20\(Windows%20Forms\).md)