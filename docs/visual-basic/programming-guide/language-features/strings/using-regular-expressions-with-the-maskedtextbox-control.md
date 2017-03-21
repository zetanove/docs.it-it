---
title: Utilizzo di espressioni regolari con il controllo MaskedTextBox in Visual Basic | Documenti di Microsoft
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
- strings [Visual Basic], regular expressions
- strings [Visual Basic], masked edit
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
caps.latest.revision: 10
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
ms.openlocfilehash: 15d8f131aa834321fcf7e8ca633929385c666e6a
ms.lasthandoff: 03/13/2017

---
# <a name="using-regular-expressions-with-the-maskedtextbox-control-in-visual-basic"></a>Utilizzo di espressioni regolari con il controllo MaskedTextBox in Visual Basic
In questo esempio viene illustrato come convertire espressioni regolari semplici da utilizzare con il <xref:System.Windows.Forms.MaskedTextBox>controllo.</xref:System.Windows.Forms.MaskedTextBox>  
  
## <a name="description-of-the-masking-language"></a>Descrizione del linguaggio per la  
 Lo standard <xref:System.Windows.Forms.MaskedTextBox>mascheramento language è basato su quello utilizzato per il `Masked Edit` del controllo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 6.0 e dovrebbe essere noto agli utenti di eseguire la migrazione da questa piattaforma.</xref:System.Windows.Forms.MaskedTextBox>  
  
 Il <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>di proprietà di <xref:System.Windows.Forms.MaskedTextBox>controllo specifica la maschera di input da utilizzare.</xref:System.Windows.Forms.MaskedTextBox> </xref:System.Windows.Forms.MaskedTextBox.Mask%2A> La maschera deve essere una stringa composta da uno o più elementi di maschera dalla tabella seguente.  
  
|Elemento|Descrizione|Elemento dell'espressione regolare|  
|---------------------|-----------------|--------------------------------|  
|0|Qualsiasi cifra singola compreso tra 0 e 9. Valore obbligatorio.|\d|  
|9|Numero o spazio. Voce facoltativa.|[ \d]?|  
|#|Numero o spazio. Voce facoltativa. Se questa posizione viene lasciata vuota nella maschera, verrà visualizzata come spazio. Segno più (+) e meno (-) sono consentiti i segni.|[ \d+-]?|  
|L|Lettera ASCII. Valore obbligatorio.|[a-zA-Z]|  
|?|Lettera ASCII. Voce facoltativa.|[a-zA-Z]?|  
|&|Carattere. Valore obbligatorio.|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo]}|  
|C|Carattere. Voce facoltativa.|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]?|  
|A|Carattere alfanumerico. Voce facoltativa.|\W|  
|.|Segnaposto decimale appropriato per la lingua.|Non disponibile.|  
|,|Segnaposto appropriato per la lingua migliaia.|Non disponibile.|  
|:|Separatore dell'ora appropriato per la lingua.|Non disponibile.|  
|/|Separatore di data appropriato per la lingua.|Non disponibile.|  
|$|Simbolo di valuta appropriato per la lingua.|Non disponibile.|  
|\<|Converte tutti i caratteri che seguono in lettere minuscole.|Non disponibile.|  
|>|Converte tutti i caratteri che seguono in lettere maiuscole.|Non disponibile.|  
|&#124;|Annulla un turno precedente backup oppure spostare verso il basso.|Non disponibile.|  
|\|Esegue l'escape di un carattere di maschera, trasformandolo in un valore letterale. "\\\\" è la sequenza di escape per una barra rovesciata.|\|  
|Tutti gli altri caratteri.|Valori letterali. Tutti gli elementi di maschera non verranno visualizzati come tali all'interno di <xref:System.Windows.Forms.MaskedTextBox>.</xref:System.Windows.Forms.MaskedTextBox>|Tutti gli altri caratteri.|  
  
 Decimale (.), migliaia (,), tempi (:), data (/) e predefinito di simboli di valuta ($) per i simboli, come definito dalle impostazioni cultura dell'applicazione. È possibile forzare la visualizzazione di simboli per un'altra lingua tramite il <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A>proprietà.</xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A>  
  
## <a name="regular-expressions-and-masks"></a>Espressioni regolari e maschere  
 Sebbene sia possibile utilizzare espressioni regolari e maschere per convalidare l'input dell'utente, non sono completamente equivalenti. Espressioni regolari possono esprimere modelli più complessi rispetto alle maschere, ma possono esprimere le stesse informazioni più conciso e in un formato alla lingua.  
  
 Nella tabella seguente confronta quattro espressioni regolari e la maschera equivalente per ognuna.  
  
|Espressione regolare|Maschera|Note|  
|------------------------|----------|-----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|Il `/` carattere nella maschera è un separatore di data logica e verrà visualizzato all'utente come separatore di data appropriato per impostazioni cultura correnti dell'applicazione.|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|Data in formato di Stati Uniti in cui viene visualizzata l'abbreviazione del mese di tre lettere con l'iniziale maiuscola seguita da due lettere minuscole (giorno, abbreviazione del mese e anno).|  
|`(\(\d{3}\)-)?\d{3}-d{4}`|`(999)-000-0000`|Numero di telefono degli Stati Uniti, prefisso facoltativo. Se l'utente non desidera immettere i caratteri facoltativi, è possibile immettere spazi o posizionare il puntatore del mouse direttamente nella posizione della maschera rappresentata dal primo 0.|  
|`$\d{6}.00`|`$999,999.00`|Un valore di valuta compreso tra 0 e 999999. La valuta, millesimi e caratteri decimali verranno sostituiti in fase di esecuzione con i relativi equivalenti specifici delle impostazioni cultura.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A></xref:System.Windows.Forms.MaskedTextBox.Mask%2A>   
 <xref:System.Windows.Forms.MaskedTextBox></xref:System.Windows.Forms.MaskedTextBox>   
 [Convalida delle stringhe in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)   
 [MaskedTextBox (controllo)](http://msdn.microsoft.com/library/235d6121-027d-481d-8d59-4f6794d15d0c)
