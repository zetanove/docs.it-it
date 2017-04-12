---
title: Influenza delle impostazioni cultura sulle stringhe in Visual Basic | Documenti di Microsoft
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
- locale, effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
caps.latest.revision: 20
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
ms.openlocfilehash: 63228a40897b29d0324be73ca1a17bcb19af2a16
ms.lasthandoff: 03/13/2017

---
# <a name="how-culture-affects-strings-in-visual-basic"></a>Influenza delle impostazioni cultura sulle stringhe in Visual Basic
Questa pagina della Guida viene illustrato come [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] utilizza informazioni per eseguire le conversioni di stringhe e i confronti delle impostazioni cultura.  
  
## <a name="when-to-use-culture-specific-strings"></a>Quando utilizzare le stringhe specifiche delle impostazioni cultura  
 In genere, è necessario utilizzare stringhe specifiche delle impostazioni cultura per tutti i dati presentati e letti dagli utenti e utilizzare stringhe di impostazioni cultura invarianti per dati interni dell'applicazione.  
  
 Ad esempio, se l'applicazione richiede agli utenti di immettere una data come stringa, deve aspettarsi che gli utenti per formattare le stringhe secondo le proprie impostazioni cultura e l'applicazione dovrebbe convertire la stringa in modo appropriato. Se l'applicazione presenta quindi tale data nella relativa interfaccia utente, dovrebbe presentarla nelle impostazioni cultura dell'utente.  
  
 Tuttavia, se l'applicazione carica la data in un server centrale, dovrebbe essere formattata la stringa in base alle impostazioni cultura specifiche, per evitare confusione tra formati della data potenzialmente diversi.  
  
## <a name="culture-sensitive-functions"></a>Funzioni dipendenti dalle impostazioni cultura  
 Tutti i [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] funzioni di conversione di stringhe (tranne che per il `Str` e `Val` funzioni) utilizzare informazioni sulle impostazioni cultura dell'applicazione per assicurarsi che le conversioni e confronti siano appropriati per le impostazioni cultura dell'utente dell'applicazione.  
  
 La chiave per l'utilizzo corretto delle funzioni di conversione di stringhe nelle applicazioni eseguite in computer con diverse impostazioni cultura consiste nel comprendere quali funzioni utilizzano impostazioni cultura specifiche, e che utilizzano le impostazioni cultura correnti. Si noti che le impostazioni dell'applicazione delle impostazioni cultura sono, per impostazione predefinita, ereditate dalle impostazioni cultura del sistema operativo. Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Strings.Asc%2A>, <xref:Microsoft.VisualBasic.Strings.AscW%2A>, <xref:Microsoft.VisualBasic.Strings.Chr%2A>, <xref:Microsoft.VisualBasic.Strings.ChrW%2A>, <xref:Microsoft.VisualBasic.Strings.Format%2A>, <xref:Microsoft.VisualBasic.Conversion.Hex%2A>, <xref:Microsoft.VisualBasic.Conversion.Oct%2A>, e [funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md).</xref:Microsoft.VisualBasic.Conversion.Oct%2A> </xref:Microsoft.VisualBasic.Conversion.Hex%2A> </xref:Microsoft.VisualBasic.Strings.Format%2A> </xref:Microsoft.VisualBasic.Strings.ChrW%2A> </xref:Microsoft.VisualBasic.Strings.Chr%2A> </xref:Microsoft.VisualBasic.Strings.AscW%2A> </xref:Microsoft.VisualBasic.Strings.Asc%2A>  
  
 Il `Str` (converte i numeri in stringhe) e `Val` funzioni (conversione di stringhe in numeri) non utilizzano informazioni relative alla lingua dell'applicazione durante la conversione tra stringhe e numeri. Riconoscono invece solo il punto (.) come separatore decimale valido. I sensibili analoghi di queste funzioni sono:  
  
-   **Conversioni che utilizzano le impostazioni cultura correnti.** Il `CStr` e `Format` funzioni convertono una stringa, un numero e il `CDbl` e `CInt` funzioni convertono una stringa in un numero.  
  
-   **Conversioni che utilizzano una lingua specifica.** Ogni oggetto number presenta un `ToString(IFormatProvider)` metodo che converte un numero in una stringa e un `Parse(String, IFormatProvider)` metodo che converte una stringa in un numero. Ad esempio, il `Double` tipo fornisce la <xref:System.Double.ToString%28System.IFormatProvider%29>e <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29>metodi.</xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> </xref:System.Double.ToString%28System.IFormatProvider%29>  
  
 Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Conversion.Str%2A>e <xref:Microsoft.VisualBasic.Conversion.Val%2A>.</xref:Microsoft.VisualBasic.Conversion.Val%2A> </xref:Microsoft.VisualBasic.Conversion.Str%2A>  
  
## <a name="using-a-specific-culture"></a>Utilizzo di impostazioni cultura specifiche  
 Si supponga che si sta sviluppando un'applicazione che invia una data (formattata come stringa) a un servizio Web. In questo caso, l'applicazione deve utilizzare una lingua specifica per la conversione di stringa. Per illustrare il motivo, considerare i risultati ottenuti utilizzando la data <xref:System.DateTime.ToString>metodo: se l'applicazione utilizza questo metodo per formattare la data 4 luglio 2005, viene restituito "7/4/2005 12:00:00 AM" viene eseguito con le impostazioni cultura inglese Stati Uniti (en-US), ma restituisce "04.07.2005 00:00:00" viene eseguito con le impostazioni cultura tedesco (de-DE).</xref:System.DateTime.ToString>  
  
 Quando è necessario eseguire una conversione di stringhe in un formato specifico delle impostazioni cultura, è necessario utilizzare il `CultureInfo` classe incorporato nel [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]. È possibile creare un nuovo `CultureInfo` oggetto per impostazioni cultura specifiche, passando il nome delle impostazioni cultura per il <xref:System.Globalization.CultureInfo.%23ctor%2A>costruttore.</xref:System.Globalization.CultureInfo.%23ctor%2A> I nomi delle impostazioni cultura supportati sono elencati nel <xref:System.Globalization.CultureInfo>pagina della Guida (classe).</xref:System.Globalization.CultureInfo>  
  
 In alternativa, è possibile ottenere un'istanza del *invariabile* dalla <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>proprietà.</xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> Le impostazioni cultura invarianti sono basata sulla lingua inglese, ma esistono alcune differenze. Le impostazioni cultura invarianti ad esempio, specificano un formato di 24 ore anziché in un formato 12 ore.  
  
 Per convertire una data nella stringa di impostazioni cultura, passare il <xref:System.Globalization.CultureInfo>oggetto dell'oggetto data <xref:System.DateTime.ToString%28System.IFormatProvider%29>metodo.</xref:System.DateTime.ToString%28System.IFormatProvider%29> </xref:System.Globalization.CultureInfo> Ad esempio, il codice seguente visualizza "07/04/2005 00:00:00", indipendentemente dalle impostazioni cultura dell'applicazione.  
  
 [!code-vb[VbVbalrConcepts n.&1;](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/VisualBasic/how-culture-affects-strings_1.vb)]  
  
> [!NOTE]
>  Valori letterali data vengono sempre interpretati in base alle impostazioni cultura inglesi.  
  
## <a name="comparing-strings"></a>Confronto di stringhe  
 Esistono due situazioni importanti in cui sono necessari i confronti di stringhe:  
  
-   **Ordinamento dei dati da visualizzare all'utente.** Utilizzare le operazioni in base alla lingua corrente in modo ordinamento delle stringhe in modo appropriato.  
  
-   **Determinazione della corrispondenza esatta di due stringhe interne all'applicazione (in genere per motivi di sicurezza).** Utilizzare le operazioni che non tengono conto delle impostazioni cultura correnti.  
  
 È possibile eseguire entrambi i tipi di confronti con la [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Strings.StrComp%2A>funzione.</xref:Microsoft.VisualBasic.Strings.StrComp%2A> Specificare l'opzione facoltativa `Compare` argomento per controllare il tipo di confronto: `Text` per la maggior parte di input e output `Binary` per determinare le corrispondenze esatte.  
  
 Il `StrComp` funzione restituisce un intero che indica la relazione tra le due stringhe confrontate in base ai criteri di ordinamento. Un valore positivo per il risultato indica che la prima stringa è maggiore della seconda stringa. Un risultato negativo indica la prima stringa è minore, mentre zero indica l'uguaglianza tra le stringhe.  
  
 [!code-vb[VbVbalrStrings&#22;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_2.vb)]  
  
 È inoltre possibile utilizzare il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] i partner di `StrComp` funzione, il <xref:System.String.Compare%2A?displayProperty=fullName>(metodo).</xref:System.String.Compare%2A?displayProperty=fullName> Questo è un metodo statico, overload della classe string di base. Nell'esempio seguente viene illustrato come viene utilizzato questo metodo:  
  
 [!code-vb[VbVbalrStrings n.&48;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_3.vb)]  
  
 Per un maggiore controllo sul modo in cui vengono eseguiti i confronti, è possibile utilizzare altri overload di <xref:System.String.Compare%2A>(metodo).</xref:System.String.Compare%2A> Con il <xref:System.String.Compare%2A?displayProperty=fullName>(metodo), è possibile utilizzare il `comparisonType` argomento per specificare il tipo di confronto da utilizzare.</xref:System.String.Compare%2A?displayProperty=fullName>  
  
|Il valore per `comparisonType` argomento|Tipo di confronto|Quando utilizzarlo|  
|---|---|---|  
|`Ordinal`|Confronto in base ai byte componente stringhe.|Utilizzare questo valore quando si confrontano: gli identificatori tra maiuscole e minuscole, le impostazioni relative alla sicurezza o altri identificatori non linguistici in cui i byte devono corrispondere esattamente.|  
|`OrdinalIgnoreCase`|Confronto in base ai byte componente stringhe.<br /><br /> `OrdinalIgnoreCase`utilizza le informazioni di impostazioni cultura invarianti per determinare se due caratteri si differenziano solo in lettere maiuscole/minuscole.|Utilizzare questo valore quando si confrontano: gli identificatori tra maiuscole e minuscole, le impostazioni relative alla sicurezza e dati archiviati in Windows.|  
|`CurrentCulture` o `CurrentCultureIgnoreCase`|Confronto in base all'interpretazione delle stringhe nelle impostazioni cultura correnti.|Utilizzare questi valori quando si confrontano: i dati visualizzati all'utente, la maggior parte dell'input dell'utente e altri dati che richiedono interpretazione linguistica.|  
|`InvariantCulture` o `InvariantCultureIgnoreCase`|Confronto in base all'interpretazione delle stringhe nelle impostazioni cultura invarianti.<br /><br /> Questo è diverso da quello di `Ordinal` e `OrdinalIgnoreCase`, in quanto le impostazioni cultura invarianti trattano i caratteri di fuori dell'intervallo accettato come caratteri invarianti equivalenti.|Utilizzare questi valori solo durante il confronto dei dati persistenti o la visualizzazione dei dati linguisticamente rilevanti che richiede un ordinamento fisso.|  
  
### <a name="security-considerations"></a>Considerazioni sulla sicurezza  
 Se l'applicazione prende decisioni di protezione in base al risultato di un'operazione di modifica di maiuscole o confronto, quindi l'operazione deve utilizzare il <xref:System.String.Compare%2A?displayProperty=fullName>metodo e passare `Ordinal` o `OrdinalIgnoreCase` per il `comparisonType` argomento.</xref:System.String.Compare%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Globalization.CultureInfo></xref:System.Globalization.CultureInfo>   
 [Introduzione alle stringhe in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [Funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
