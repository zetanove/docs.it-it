---
title: Costanti ed enumerazioni (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- enumerations [Visual Basic]
- constants
- constants, list of
ms.assetid: 309c0ad5-83e4-4f96-99ea-83cd95107417
caps.latest.revision: 18
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
ms.openlocfilehash: e37ef2e3c51e96e85cb214054195016e69d52382
ms.lasthandoff: 03/13/2017

---
# <a name="constants-and-enumerations-visual-basic"></a>Costanti ed enumerazioni (Visual Basic)
[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce una serie di costanti ed enumerazioni per gli sviluppatori predefinite. Costanti di archiviano i valori che rimangono costanti durante l'esecuzione di un'applicazione. Le enumerazioni forniscono un modo pratico per l'utilizzo di set di costanti correlate e per associare i valori costanti a nomi.  
  
## <a name="constants"></a>Costanti  
  
### <a name="conditional-compilation-constants"></a>Costanti di compilazione condizionale  
 Nella tabella seguente sono elencate le costanti predefinite disponibili per la compilazione condizionale.  
  
|**Costante**|**Descrizione**|  
|---|---|  
|`CONFIG`|Stringa che corrisponde all'impostazione corrente del **configurazione soluzione attiva** nella casella di **Configuration Manager**.|  
|`DEBUG`|Oggetto `Boolean` valore che può essere impostata nel **le proprietà del progetto** la finestra di dialogo. Per impostazione predefinita, la configurazione di Debug per un progetto definisce `DEBUG`. Quando `DEBUG` è definito, <xref:System.Diagnostics.Debug>metodi della classe generano l'output per il **Output** finestra.</xref:System.Diagnostics.Debug> Quando non è definito, <xref:System.Diagnostics.Debug>metodi non verranno compilati e non genera alcun output di Debug.</xref:System.Diagnostics.Debug>|  
|`TARGET`|Stringa che rappresenta il tipo di output per il progetto o l'impostazione della riga di comando **/destinazione** (opzione). I valori possibili di `TARGET` sono:<br /><br /> -"winexe" per un'applicazione Windows.<br />-"exe" per un'applicazione console.<br />-"library" per una libreria di classi.<br />-"modulo" per un modulo.<br />-La **/destinazione** opzione può essere impostata [!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)] ambiente di sviluppo integrato. Per ulteriori informazioni, vedere [/target (Visual Basic)](../../visual-basic/reference/command-line-compiler/target.md).|  
|`TRACE`|Oggetto `Boolean` valore che può essere impostata nel **le proprietà del progetto** la finestra di dialogo. Per impostazione predefinita, tutte le configurazioni per un progetto definiscono `TRACE`. Quando `TRACE` è definito, <xref:System.Diagnostics.Trace>metodi della classe generano l'output per il **Output** finestra.</xref:System.Diagnostics.Trace> Quando non è definito, <xref:System.Diagnostics.Trace>classe metodi non verranno compilati e non `Trace` viene generato l'output.</xref:System.Diagnostics.Trace>|  
|`VBC_VER`|Un numero che rappresenta il [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] versione, in *principali*.* secondaria* formato. Il numero di versione per [!INCLUDE[vbprvblong](../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] è 8.0.|  
  
### <a name="print-and-display-constants"></a>Costanti di visualizzazione e stampa  
 Quando si chiama stampa e visualizzare le funzioni, è possibile utilizzare le seguenti costanti nel codice al posto dei valori effettivi.  
  
|**Costante**|**Descrizione**|  
|---|---|  
|`vbCrLf`|Combinazione di caratteri di ritorno/avanzamento riga, ritorno a capo.|  
|`vbCr`|Ritorno a capo.|  
|`vbLf`|Carattere di avanzamento riga.|  
|`vbNewLine`|Carattere di nuova riga.|  
|`vbNullChar`|Carattere null.|  
|`vbNullString`|Non equivale a una stringa di lunghezza zero (""); utilizzato per chiamare le routine esterne.|  
|`vbObjectError`|Numero errore. Numeri di errore definiti dall'utente devono essere maggiori di questo valore. Ad esempio:<br /><br /> `Err.Raise(Number) = vbObjectError + 1000`|  
|`vbTab`|Carattere di tabulazione.|  
|`vbBack`|Carattere backspace.|  
|`vbFormFeed`|Non utilizzato in Microsoft Windows.|  
|`vbVerticalTab`|Non è utile in Microsoft Windows.|  
  
## <a name="enumerations"></a>Enumerazioni  
 Nella tabella seguente vengono elencate e descritte le enumerazioni fornite da [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
|Enumerazione|Descrizione|  
|---|---|  
|<xref:Microsoft.VisualBasic.AppWinStyle></xref:Microsoft.VisualBasic.AppWinStyle>|Indica lo stile di finestra da utilizzare per il programma richiamato quando si chiama il <xref:Microsoft.VisualBasic.Interaction.Shell%2A>(funzione).</xref:Microsoft.VisualBasic.Interaction.Shell%2A>|  
|<xref:Microsoft.VisualBasic.AudioPlayMode></xref:Microsoft.VisualBasic.AudioPlayMode>|Indica la modalità di riproduzione di suoni quando si chiamano metodi audio.|  
|<xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole></xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole>|Indica il tipo di ruolo da controllare quando si chiama il <xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A>(metodo).</xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A>|  
|<xref:Microsoft.VisualBasic.CallType></xref:Microsoft.VisualBasic.CallType>|Indica il tipo di routine che viene richiamata quando si chiama il <xref:Microsoft.VisualBasic.Interaction.CallByName%2A>(funzione).</xref:Microsoft.VisualBasic.Interaction.CallByName%2A>|  
|<xref:Microsoft.VisualBasic.CompareMethod></xref:Microsoft.VisualBasic.CompareMethod>|Indica come confrontare le stringhe quando si chiama le funzioni di confronto.|  
|<xref:Microsoft.VisualBasic.DateFormat></xref:Microsoft.VisualBasic.DateFormat>|Indica come visualizzare le date quando si chiama il <xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>(funzione).</xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>|  
|<xref:Microsoft.VisualBasic.DateInterval></xref:Microsoft.VisualBasic.DateInterval>|Indica come determinare e formattare gli intervalli di date quando si chiamano funzioni relative alle date.|  
|<xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption></xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption>|Specifica le azioni da intraprendere quando una directory che deve essere eliminato contiene file o directory.|  
|<xref:Microsoft.VisualBasic.DueDate></xref:Microsoft.VisualBasic.DueDate>|Indica le scadenze dei pagamenti quando si chiamano metodi finanziari.|  
|<xref:Microsoft.VisualBasic.FileIO.FieldType></xref:Microsoft.VisualBasic.FileIO.FieldType>|Indica se i campi di testo sono delimitati o a larghezza fissa.|  
|<xref:Microsoft.VisualBasic.FileAttribute></xref:Microsoft.VisualBasic.FileAttribute>|Indica gli attributi di file da utilizzare quando si chiamano funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.FirstDayOfWeek></xref:Microsoft.VisualBasic.FirstDayOfWeek>|Indica il primo giorno della settimana da utilizzare quando si chiamano funzioni relative alla data.|  
|<xref:Microsoft.VisualBasic.FirstWeekOfYear></xref:Microsoft.VisualBasic.FirstWeekOfYear>|Indica la prima settimana dell'anno da utilizzare quando si chiamano funzioni relative alla data.|  
|<xref:Microsoft.VisualBasic.MsgBoxResult></xref:Microsoft.VisualBasic.MsgBoxResult>|Indica quale pulsante è stato premuto in una finestra di messaggio restituita dal <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>(funzione).</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>|  
|<xref:Microsoft.VisualBasic.MsgBoxStyle></xref:Microsoft.VisualBasic.MsgBoxStyle>|Indica i pulsanti da visualizzare quando si chiama il <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>(funzione).</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>|  
|<xref:Microsoft.VisualBasic.OpenAccess></xref:Microsoft.VisualBasic.OpenAccess>|Indica come aprire un file quando si chiamano funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.OpenMode></xref:Microsoft.VisualBasic.OpenMode>|Indica come aprire un file quando si chiamano funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.OpenShare></xref:Microsoft.VisualBasic.OpenShare>|Indica come aprire un file quando si chiamano funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.FileIO.RecycleOption></xref:Microsoft.VisualBasic.FileIO.RecycleOption>|Specifica se un file deve essere eliminato in modo permanente o inserito nel Cestino.|  
|<xref:Microsoft.VisualBasic.FileIO.SearchOption></xref:Microsoft.VisualBasic.FileIO.SearchOption>|Specifica se la ricerca in tutte o solo le directory di livello superiore.|  
|<xref:Microsoft.VisualBasic.TriState></xref:Microsoft.VisualBasic.TriState>|Indica un `Boolean` valore o se il valore predefinito deve essere utilizzato quando si chiamano funzioni di formattazione dei numeri.|  
|<xref:Microsoft.VisualBasic.FileIO.UICancelOption></xref:Microsoft.VisualBasic.FileIO.UICancelOption>|Specifica l'azione da eseguire se l'utente sceglie **Annulla** durante un'operazione.|  
|<xref:Microsoft.VisualBasic.FileIO.UIOption></xref:Microsoft.VisualBasic.FileIO.UIOption>|Specifica se visualizzare o meno per una finestra di dialogo di avanzamento durante la copia, eliminazione o spostamento di file o directory.|  
|<xref:Microsoft.VisualBasic.VariantType></xref:Microsoft.VisualBasic.VariantType>|Indica il tipo di un oggetto variant restituito dal <xref:Microsoft.VisualBasic.Information.VarType%2A>(funzione).</xref:Microsoft.VisualBasic.Information.VarType%2A>|  
|<xref:Microsoft.VisualBasic.VbStrConv></xref:Microsoft.VisualBasic.VbStrConv>|Indica il tipo di conversione da eseguire quando si chiama il <xref:Microsoft.VisualBasic.Strings.StrConv%2A>(funzione).</xref:Microsoft.VisualBasic.Strings.StrConv%2A>|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti al linguaggio Visual Basic](../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../visual-basic/index.md)   
 [Cenni preliminari sulle costanti](../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Cenni preliminari sulle enumerazioni](../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
