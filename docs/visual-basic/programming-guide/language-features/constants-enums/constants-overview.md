---
title: Cenni preliminari sulle costanti (Visual Basic) | Documenti di Microsoft
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
- constants
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
caps.latest.revision: 14
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8004045d233da0db017b26b350743ad9f8d61845
ms.lasthandoff: 03/13/2017

---
# <a name="constants-overview-visual-basic"></a>Cenni preliminari sulle costanti (Visual Basic)
Una costante è un nome significativo che prende il posto di un numero o una stringa che non cambia. Costanti di archiviano i valori, come suggerisce il nome, rimangono invariati nel corso dell'esecuzione di un'applicazione. Notevolmente, è possibile migliorare la leggibilità del codice e semplificare la gestione tramite l'utilizzo di costanti. Utilizzarle nel codice che contiene valori che vengono ripetuti o che dipendono da alcuni numeri che sono difficili da ricordare o non hanno alcun significato evidente.  
  
## <a name="how-to-create-and-use-constants"></a>Come creare e utilizzare le costanti  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]contiene un numero di costanti predefinite, utilizzate principalmente per la stampa e visualizzazione. È inoltre possibile creare costanti personalizzate mediante la `Const` istruzione, utilizzando le stesse linee guida per la creazione di un nome di variabile. Se `Option Strict` è `On`, è necessario dichiarare in modo esplicito il tipo di costante.  
  
 Ambito di una costante, ovvero il set di tutto il codice che è possibile farvi riferimento senza la qualifica del nome è uguale a quello di una variabile dichiarata nella stessa posizione. Per creare una costante che esista nell'ambito di una particolare procedura, dichiararla all'interno di tale procedura. Per creare una costante che sia disponibile in tutta l'applicazione, dichiararla utilizzando il `Public` (parola chiave) nella sezione dichiarazioni della classe.  
  
> [!NOTE]
>  Sebbene costanti siano simili variabili, è possibile modificarle o assegnare di nuovi valori, come per le variabili.  
  
 Le costanti utilizzate nel codice possono essere definite dal modello a oggetti per i controlli o ai componenti utilizzati, o possono essere definiti dall'utente (vale a dire quelle create dall'utente).  
  
## <a name="compile-time-and-run-time-constants"></a>Costanti in fase di compilazione e Runtime  
 Una costante in fase di compilazione viene calcolata al momento che il codice viene compilato, mentre una costante in fase di esecuzione può essere calcolata solo mentre è in esecuzione l'applicazione. Una costante in fase di compilazione avrà lo stesso valore ogni volta che viene eseguita un'applicazione, mentre una costante in fase di esecuzione potrebbe cambiare ogni volta. Costanti in fase di compilazione sono necessarie per i casi, ad esempio i limiti di matrice, le espressioni case o gli inizializzatori degli enumeratori.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Definizione|Termine|  
|---|---|  
|[Procedura: Dichiarare una costante](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)|Viene illustrato come utilizzare il `Const` istruzione per dichiarare una costante e impostarne il valore; dichiarando una costante, assegnare un nome significativo per il valore.|  
|[Costanti definite dall'utente](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)|Viene descritto come creare costanti personalizzate, incluse le informazioni sulla definizione dell'ambito e come evitare riferimenti circolari.|  
|[Tipi di dati costanti e letterali](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)|Vengono fornite informazioni su come il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore Inizializza le costanti quando `Option Explicit` è disattivato.|  
|[Procedura: Raggruppare i valori delle costanti correlate](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-group-related-constant-values-together.md)|Viene illustrato come raggruppare i valori costanti che sono correlati.|  
  
## <a name="reference"></a>Riferimento  
  
|Definizione|Termine|  
|---|---|  
|[Costanti ed enumerazioni](../../../../visual-basic/language-reference/constants-and-enumerations.md)|Vengono elencate le costanti predefinite da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].|  
|[Istruzione Const](../../../../visual-basic/language-reference/statements/const-statement.md)|Viene descritto il `Const` istruzione e il relativo utilizzo.|  
|[Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)|Viene descritto il `Option Strict` istruzione e il relativo utilizzo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sulle enumerazioni](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [Procedura: inizializzare una variabile di matrice in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)
