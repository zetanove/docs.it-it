---
title: "How Culture Affects Strings in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "locale, effect on strings"
  - "strings [Visual Basic], locale dependence"
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# How Culture Affects Strings in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa pagina della Guida viene illustrato come in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] le informazioni relative alle impostazioni cultura vengono utilizzate per eseguire conversioni e confronti tra le stringhe.  
  
## Quando utilizzare le stringhe specifiche delle impostazioni cultura  
 Generalmente è necessario utilizzare stringhe specifiche delle impostazioni cultura per tutti i dati presentati e letti dagli utenti e utilizzare le stringhe indipendenti dalle impostazioni cultura per i dati interni dell'applicazione.  
  
 Se ad esempio all'utente viene richiesto di immettere una data sotto forma di stringa, l'utente dovrebbe formattare le stringhe in base alle proprie impostazioni cultura e l'applicazione dovrebbe convertire la stringa in modo appropriato.  Se l'applicazione presenta quindi quella data nell'interfaccia utente, dovrebbe presentarla nelle impostazioni cultura dell'utente.  
  
 Tuttavia se l'applicazione carica la data in un server centrale, la stringa dovrebbe essere formattata in base a impostazioni cultura specifiche, per impedire di far confusione tra formati della data potenzialmente diversi.  
  
## Funzioni dipendenti dalle impostazioni cultura  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] tutte le funzioni per la conversione delle stringhe \(ad eccezione delle funzioni `Str` e `Val`\) utilizzano le informazioni relative alle impostazioni cultura dell'applicazione per accertarsi che le conversioni e i confronti siano appropriati per la cultura dell'utente dell'applicazione.  
  
 La chiave per l'utilizzo corretto delle funzioni per la conversione delle stringhe nelle applicazioni eseguite sui computer con diverse impostazioni cultura consiste nel comprendere quali funzioni utilizzano impostazioni cultura specifiche e quali utilizzano le impostazioni cultura correnti.  Si noti che le impostazioni cultura dell'applicazione vengono, per impostazione predefinita, ereditate dalle impostazioni cultura del sistema operativo.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Strings.Asc%2A>, <xref:Microsoft.VisualBasic.Strings.AscW%2A>, <xref:Microsoft.VisualBasic.Strings.Chr%2A>, <xref:Microsoft.VisualBasic.Strings.ChrW%2A>, <xref:Microsoft.VisualBasic.Strings.Format%2A>, <xref:Microsoft.VisualBasic.Conversion.Hex%2A>, <xref:Microsoft.VisualBasic.Conversion.Oct%2A> e [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md).  
  
 Le funzioni `Str` \(conversione di numeri in stringhe\) e `Val` \(conversione di stringhe in numeri\) non utilizzano le informazioni relative alle impostazioni cultura dell'applicazione per la conversione tra stringhe e numeri.  Riconoscono invece solo il punto \(.\) come separatore decimale valido.  Gli equivalenti sensibili alle impostazioni cultura di queste funzioni sono:  
  
-   **Conversioni che utilizzano le impostazioni cultura correnti.** Le funzioni `CStr` e `Format` consentono di convertire un numero in una stringa, mentre le funzioni `CDbl` e `CInt` consentono di convertire una stringa in un numero.  
  
-   **Conversioni che utilizzano impostazioni cultura specifiche.** In ogni oggetto numero esiste un metodo `ToString(IFormatProvider)` per la conversione di numeri in stringhe e un metodo `Parse(String, IFormatProvider)` per la conversione di stringhe in numeri.  Nel tipo `Double` ad esempio sono presenti i metodi <xref:System.Double.ToString%28System.IFormatProvider%29> e <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29>.  
  
 Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Conversion.Str%2A> e <xref:Microsoft.VisualBasic.Conversion.Val%2A>.  
  
## Utilizzo di impostazioni cultura specifiche  
 Si supponga di voler sviluppare un'applicazione per l'invio di una data \(formattata come stringa\) in un servizio Web.  In questo caso, è necessario che l'applicazione utilizzi impostazioni cultura specifiche per la conversione delle stringhe.  A titolo esplicativo considerare il risultato provocato dal metodo <xref:System.DateTime.ToString> della data. Se l'applicazione utilizza quel metodo per la formattazione della data 4 luglio 2005, restituirà "7\/4\/2005" 12:00:00 AM" quando viene eseguita con le impostazioni cultura inglesi \(Stati Uniti\), ma restituisce "04.07.2005 00:00:00" quando viene eseguita con le impostazioni cultura tedesche \(de\-DE\).  
  
 Per eseguire una conversione delle stringhe in un formato specifico delle impostazioni cultura, è necessario utilizzare la classe `CultureInfo` incorporata nel [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)].  È possibile creare un oggetto `CultureInfo` nuovo per impostazioni cultura specifiche, passando il nome delle impostazioni cultura al costruttore <xref:System.Globalization.CultureInfo.%23ctor%2A>.  I nomi delle impostazioni cultura supportati sono elencati nella pagine della guida della classe <xref:System.Globalization.CultureInfo>.  
  
 In alternativa, è possibile ottenere un'istanza delle *impostazioni cultura invarianti* dalla proprietà <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  Le impostazioni cultura invarianti corrispondono alle impostazioni cultura inglesi, ma ci sono delle differenze.  Ad esempio, le impostazioni cultura invarianti utilizzano il formato a 24 ore anziché a 12 ore.  
  
 Per convertire una data nella stringa delle impostazioni cultura, passare l'oggetto <xref:System.Globalization.CultureInfo> al metodo <xref:System.DateTime.ToString%28System.IFormatProvider%29> dell'oggetto della data.  Nel codice che segue, ad esempio, viene visualizzato "07\/04\/2005 00:00:00", indipendentemente dalle impostazioni cultura dell'applicazione.  
  
 [!code-vb[VbVbalrConcepts#1](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/visualbasic/how-culture-affects-stri_1.vb)]  
  
> [!NOTE]
>  I valori letterali di data vengono sempre interpretati in base alle impostazioni cultura inglesi.  
  
## Confronto di stringhe  
 Esistono due situazioni importanti in cui sono necessari i confronti di stringhe:  
  
-   **Ordinamento dei dati da visualizzare.**  Utilizzare operazioni basate sulle impostazioni cultura correnti in modo da permettere l'ordinamento appropriato delle stringhe.  
  
-   **Determinare la corrispondenza esatta di due stringhe interne all'applicazione \(generalmente per motivi di sicurezza\).** Utilizzare operazioni che non tengono conto delle impostazioni cultura correnti.  
  
 È possibile eseguire entrambi i tipi di confronto con la funzione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] <xref:Microsoft.VisualBasic.Strings.StrComp%2A>.  Specificare l'argomento `Compare` facoltativo per controllare il tipo di confronto: `Text` per la maggior parte di input e output, `Binary` per la determinazione di corrispondenze esatte.  
  
 La funzione `StrComp` restituisce un intero che indica la relazione tra le due stringhe confrontate in base ai criteri di ordinamento.  Un risultato di valore positivo indica che la prima stringa è maggiore della seconda.  Un risultato negativo indica che la prima stringa è minore, mentre zero indica l'eguaglianza delle stringhe.  
  
 [!code-vb[VbVbalrStrings#22](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/how-culture-affects-stri_2.vb)]  
  
 È possibile inoltre utilizzare il partner [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort-md.md)] della funzione `StrComp`, il metodo <xref:System.String.Compare%2A?displayProperty=fullName>.  Si tratta di un metodo della classe base stringa su cui avviene un overload statico.  Nell'esempio seguente è illustrato l'utilizzo di questo metodo:  
  
 [!code-vb[VbVbalrStrings#48](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/how-culture-affects-stri_3.vb)]  
  
 Per un maggiore controllo sul modo in cui vengono eseguiti i confronti, è possibile utilizzare overload aggiuntivi del metodo <xref:System.String.Compare%2A>.  Con il metodo <xref:System.String.Compare%2A?displayProperty=fullName>, è possibile utilizzare l'argomento `comparisonType` per specificare il tipo di confronto da utilizzare.  
  
||||  
|-|-|-|  
|Valore per l'argomento `comparisonType`|Tipo di confronto|Casi di utilizzo|  
|`Ordinal`|Confronto basato sui byte dei componenti della stringa.|Utilizzare questo valore per il confronto tra: identificatori con distinzione tra maiuscole e minuscole, impostazioni relative alla sicurezza o altri identificatori non linguistici in cui i byte devono corrispondere in maniera esatta.|  
|`OrdinalIgnoreCase`|Confronto basato sui byte dei componenti della stringa.<br /><br /> `OrdinalIgnoreCase` utilizza le informazioni delle impostazioni cultura invarianti per determinare se due caratteri si differenziano solo per l'uso di maiuscole e minuscole.|Utilizzare questo valore per il confronto tra: identificatori senza distinzione tra maiuscole e minuscole, impostazioni relative alla sicurezza e dati memorizzati in Windows.|  
|`CurrentCulture` oppure `CurrentCultureIgnoreCase`|Confronto in base all'interpretazione delle stringhe nelle impostazioni cultura correnti.|Utilizzare questi valori per il confronto tra: dati visualizzati per l'utente, la maggior parte dell'input dell'utente e altri dati che necessitano di un'interpretazione linguistica.|  
|`InvariantCulture` oppure `InvariantCultureIgnoreCase`|Confronto in base all'interpretazione delle stringhe nelle impostazioni cultura invarianti.<br /><br /> Questa è diversa da `Ordinal` e `OrdinalIgnoreCase`, in quanto le impostazioni cultura invarianti trattano i caratteri al di fuori dell'intervallo accettato come caratteri invarianti equivalenti.|Utilizzare questi valori solo durante il confronto di dati persistenti o la visualizzazione di dati rilevanti da un punto di vista linguistico che richiedono un tipo di ordinamento fisso.|  
  
### Considerazioni sulla sicurezza  
 Se l'applicazione prende decisioni di sicurezza in base al risultato di un confronto o un'operazione basata sul risultato di una modifica, l'operazione dovrebbe utilizzare il metodo <xref:System.String.Compare%2A?displayProperty=fullName> e passare `Ordinal` o `OrdinalIgnoreCase` per l'argomento `comparisonType`.  
  
## Vedere anche  
 <xref:System.Globalization.CultureInfo>   
 [Introduction to Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)