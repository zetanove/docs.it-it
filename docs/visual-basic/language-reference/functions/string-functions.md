---
title: "Funzioni stringa (Visual Basic) | Microsoft Docs"
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
  - "funzioni stringa"
ms.assetid: f1bf9ac2-cbcf-4298-ae51-53182076bdc8
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Funzioni stringa (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nella tabella seguente vengono elencate le funzioni disponibili in Visual Basic per cercare e modificare le stringhe.  
  
|Metodo di .NET Framework|Descrizione|  
|------------------------------|-----------------|  
|<xref:Microsoft.VisualBasic.Strings.Asc%2A>, <xref:Microsoft.VisualBasic.Strings.AscW%2A>|Restituisce un `Integer` che rappresenta il codice carattere corrispondente a un carattere.|  
|<xref:Microsoft.VisualBasic.Strings.Chr%2A>, <xref:Microsoft.VisualBasic.Strings.ChrW%2A>|Restituisce il carattere associato al codice carattere specificato.|  
|<xref:Microsoft.VisualBasic.Strings.Filter%2A>|Restituisce una matrice con indice in base zero che contiene un sottoinsieme di una matrice `String` definito in base ai criteri di filtro specificati.|  
|<xref:Microsoft.VisualBasic.Strings.Format%2A>|Restituisce una stringa formattata in base alle istruzioni contenute in un'espressione `String` di formato.|  
|<xref:Microsoft.VisualBasic.Strings.FormatCurrency%2A>|Restituisce un'espressione nel formato valore di valuta utilizzando il simbolo di valuta impostato nel Pannello di controllo del sistema.|  
|<xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>|Restituisce un'espressione stringa che rappresenta un valore data\/ora.|  
|<xref:Microsoft.VisualBasic.Strings.FormatNumber%2A>|Restituisce un'espressione in formato di numero.|  
|<xref:Microsoft.VisualBasic.Strings.FormatPercent%2A>|Restituisce un'espressione nel formato percentuale, ossia moltiplicata per 100, seguita dal carattere %.|  
|<xref:Microsoft.VisualBasic.Strings.InStr%2A>|Restituisce un Integer che specifica la posizione di inizio della prima occorrenza di una stringa in un'altra.|  
|<xref:Microsoft.VisualBasic.Strings.InStrRev%2A>|Restituisce la posizione della prima occorrenza di una stringa inclusa in un'altra a partire dalla destra della stringa.|  
|<xref:Microsoft.VisualBasic.Strings.Join%2A>|Restituisce una stringa creata unendo un certo numero di sottostringhe di una matrice.|  
|<xref:Microsoft.VisualBasic.Strings.LCase%2A>|Restituisce una stringa o un carattere convertito in minuscolo.|  
|<xref:Microsoft.VisualBasic.Strings.Left%2A>|Restituisce una stringa contenente un numero specificato di caratteri a partire dal lato sinistro di una stringa.|  
|<xref:Microsoft.VisualBasic.Strings.Len%2A>|Restituisce un intero in cui è contenuto il numero di caratteri in una stringa.|  
|<xref:Microsoft.VisualBasic.Strings.LSet%2A>|Restituisce una stringa allineata a sinistra contenente la stringa specificata adeguata alla lunghezza specificata.|  
|<xref:Microsoft.VisualBasic.Strings.LTrim%2A>|Restituisce una stringa contenente una copia di una stringa specificata senza spazi iniziali.|  
|<xref:Microsoft.VisualBasic.Strings.Mid%2A>|Restituisce una stringa contenente il numero di caratteri specificato da una stringa.|  
|<xref:Microsoft.VisualBasic.Strings.Replace%2A>|Restituisce una stringa nella quale la sottostringa specificata è stata sostituita con un'altra sottostringa per il numero di volte indicato.|  
|<xref:Microsoft.VisualBasic.Strings.Right%2A>|Restituisce una stringa contenente un numero di caratteri specificato a partire dalla destra della stringa.|  
|<xref:Microsoft.VisualBasic.Strings.RSet%2A>|Restituisce una stringa allineata a destra contenente la stringa specificata adattata alla lunghezza specificata.|  
|<xref:Microsoft.VisualBasic.Strings.RTrim%2A>|Restituisce una stringa contenente una copia di una stringa specificata senza spazi finali.|  
|<xref:Microsoft.VisualBasic.Strings.Space%2A>|Restituisce una stringa composta dal numero di spazi specificato.|  
|<xref:Microsoft.VisualBasic.Strings.Split%2A>|Restituisce una matrice unidimensionale con indice in base zero che contiene il numero di sottostringhe specificato.|  
|<xref:Microsoft.VisualBasic.Strings.StrComp%2A>|Restituisce \-1, 0 o 1 in base al risultato di un confronto tra stringhe.|  
|<xref:Microsoft.VisualBasic.Strings.StrConv%2A>|Restituisce una stringa convertita come specificato.|  
|<xref:Microsoft.VisualBasic.Strings.StrDup%2A>|Restituisce una stringa o un oggetto composto dal carattere specificato ripetuto per il numero di volte specificato.|  
|<xref:Microsoft.VisualBasic.Strings.StrReverse%2A>|Restituisce una stringa nella quale è stato invertito l'ordine dei caratteri della stringa specificata.|  
|<xref:Microsoft.VisualBasic.Strings.Trim%2A>|Restituisce una stringa contenente una copia di una stringa specificata senza spazi iniziali o finali.|  
|<xref:Microsoft.VisualBasic.Strings.UCase%2A>|Restituisce una stringa o un carattere contenente la stringa specificata convertita in lettere maiuscole.|  
  
 È possibile utilizzare l'istruzione [Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md) per specificare se le stringhe vengono confrontate tramite un ordinamento di testo senza distinzione tra maiuscole e minuscole determinato dalle impostazioni locali del sistema \(`Text`\) o dalle rappresentazioni binarie interne dei caratteri \(`Binary`\).  Il metodo di confronto del testo predefinito è `Binary`.  
  
## Esempio  
 Nell'esempio seguente la funzione `UCase` viene utilizzata per restituire una versione in lettere maiuscole di una stringa:  
  
 [!code-vb[VbVbalrStrings#31](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_1.vb)]  
  
## Esempio  
 In questo esempio vengono utilizzate la funzione `LTrim` per rimuovere gli spazi iniziali e la funzione `RTrim` per rimuovere gli spazi finali da una variabile String.  Viene utilizzata la funzione `Trim` per eliminare entrambi i tipi di spazi.  
  
 [!code-vb[VbVbalrStrings#25](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_2.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito la funzione `Mid` viene utilizzata per restituire un determinato numero di caratteri da una stringa.  
  
 [!code-vb[VbVbalrStrings#17](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_3.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito la funzione `Len` viene utilizzata per restituire il numero di caratteri di una stringa.  
  
 [!code-vb[VbVbalrStrings#33](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_4.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito la funzione `InStr` viene utilizzata per restituire la posizione della prima occorrenza di una stringa in un'altra:  
  
 [!code-vb[VbVbalrStrings#8](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_5.vb)]  
  
## Esempio  
 In questo esempio sono presentati vari utilizzi della funzione `Format` per formattare valori mediante formati sia di tipo `String` che definiti dall'utente.  Per quanto riguarda il separatore della data \(`/`\), dell'ora \(`:`\) e gli indicatori AM\/PM \(`t` e `tt`\), l'output formattato visualizzato dal sistema dipende dalle impostazioni locali utilizzate per il codice.  Nell'ambiente di sviluppo la data e l'ora vengono visualizzate nel formato breve delle impostazioni locali.  
  
> [!NOTE]
>  Per le impostazioni locali che utilizzano il formato 24 ore, gli indicatori AM\/PM \(`t` e `tt`\) non visualizzano alcun output.  
  
 [!code-vb[VbVbalrStrings#27](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-functions_6.vb)]  
  
## Vedere anche  
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic Runtime Library Members](../../../visual-basic/language-reference/runtime-library-members.md)   
 [String Manipulation Summary](../../../visual-basic/language-reference/keywords/string-manipulation-summary.md)