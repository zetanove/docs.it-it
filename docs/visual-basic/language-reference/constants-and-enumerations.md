---
title: "Constants and Enumerations (Visual Basic) | Microsoft Docs"
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
  - "enumerations [Visual Basic]"
  - "constants"
  - "constants, list of"
ms.assetid: 309c0ad5-83e4-4f96-99ea-83cd95107417
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Constants and Enumerations (Visual Basic)
[!INCLUDE[vs2017banner](../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce una serie di costanti ed enumerazioni predefinite per gli sviluppatori.  Nelle costanti sono memorizzati valori che rimangono costanti durante l'esecuzione di un'applicazione.  Le enumerazioni costituiscono un comodo mezzo per utilizzare set di costanti correlate e di associare i valori costanti a nomi.  
  
## Costanti  
  
### Costanti di compilazione condizionale  
 Nella tabella seguente sono elencate le costanti predefinite disponibili per la compilazione condizionale.  
  
|||  
|-|-|  
|**Costante**|**Descrizione**|  
|`CONFIG`|Stringa che corrisponde all'impostazione corrente della casella **Configurazione soluzione attiva** di **Gestione configurazione**.|  
|`DEBUG`|Valore `Boolean` che può essere impostato nella finestra di dialogo **Proprietà progetto**.  Per impostazione predefinita, `DEBUG` è definita nella configurazione di debug di un progetto.  Una volta definita la costante `DEBUG`, viene generato l'output dei metodi della classe <xref:System.Diagnostics.Debug> nella finestra **Output**.  In assenza della definizione di tale costante, non viene eseguita la compilazione dei metodi della classe <xref:System.Diagnostics.Debug> e non viene generato alcun output di debug.|  
|`TARGET`|Stringa che rappresenta il tipo di output del progetto o l'impostazione dell'opzione della riga di comando **\/target**.  I valori possibili di `TARGET` sono i seguenti:<br /><br /> -   "winexe" per un'applicazione Windows.<br />-   "exe" per un'applicazione console.<br />-   "library" per una libreria di classi.<br />-   "module" per un modulo.<br />-   L'opzione **\/target** può essere impostata nell'ambiente di sviluppo integrato di [!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)].  Per ulteriori informazioni, vedere [\/target](../../visual-basic/reference/command-line-compiler/target.md).|  
|`TRACE`|Valore `Boolean` che può essere impostato nella finestra di dialogo **Proprietà progetto**.  Per impostazione predefinita, `TRACE` è definita in tutte le configurazioni di un progetto.  Una volta definita la costante `TRACE`, viene generato l'output dei metodi della classe <xref:System.Diagnostics.Trace> nella finestra **Output**.  In assenza della definizione di tale costante, non viene eseguita la compilazione dei metodi della classe <xref:System.Diagnostics.Trace> e non viene generato alcun output di `Trace`.|  
|`VBC_VER`|Numero che rappresenta la versione di [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] nel formato *principale*.*secondario*.  Il numero di versione per [!INCLUDE[vbprvblong](../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] è 8.0.|  
  
### Costanti Print e Display  
 Quando si chiamano le funzioni di stampa e visualizzazione, i valori effettivi nel codice possono essere sostituiti con le costanti seguenti.  
  
|||  
|-|-|  
|**Costante**|**Descrizione**|  
|`vbCrLf`|Combinazione di ritorno a capo e avanzamento riga.|  
|`vbCr`|Carattere di ritorno a capo.|  
|`vbLf`|Carattere di avanzamento riga.|  
|`vbNewLine`|Carattere di nuova riga.|  
|`vbNullChar`|Carattere null.|  
|`vbNullString`|Non equivale a una stringa di lunghezza zero \(""\) e viene utilizzata per la chiamata di routine esterne.|  
|`vbObjectError`|Un codice di errore.  I numeri errore definiti dall'utente devono essere maggiori di questo valore.  Di seguito è riportato un esempio:<br /><br /> `Err.Raise(Number) = vbObjectError + 1000`|  
|`vbTab`|Carattere di tabulazione.|  
|`vbBack`|Carattere backspace.|  
|`vbFormFeed`|Carattere non utilizzato in Microsoft Windows.|  
|`vbVerticalTab`|Carattere non utilizzato in Microsoft Windows.|  
  
## Enumerazioni  
 Nella tabella seguente sono elencate e descritte le enumerazioni disponibili in [!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
|||  
|-|-|  
|Enumerazione|Descrizione|  
|<xref:Microsoft.VisualBasic.AppWinStyle>|Indica lo stile della finestra da utilizzare per il programma richiamato quando viene chiamata la funzione <xref:Microsoft.VisualBasic.Interaction.Shell%2A>.|  
|<xref:Microsoft.VisualBasic.AudioPlayMode>|Indica come riprodurre i suoni quando vengono chiamati i metodi audio.|  
|<xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole>|Indica il tipo di ruolo da controllare quando viene chiamato il metodo <xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A>.|  
|<xref:Microsoft.VisualBasic.CallType>|Indica il tipo di routine da richiamare quando viene chiamata la funzione <xref:Microsoft.VisualBasic.Interaction.CallByName%2A>.|  
|<xref:Microsoft.VisualBasic.CompareMethod>|Indica come confrontare le stringhe quando si chiamano funzioni di confronto.|  
|<xref:Microsoft.VisualBasic.DateFormat>|Indica come visualizzare le date quando si chiama la funzione <xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>.|  
|<xref:Microsoft.VisualBasic.DateInterval>|Indica come determinare e formattare gli intervalli di date quando si chiamano funzioni relative alla data.|  
|<xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption>|Specifica le azioni da intraprendere quando si deve eliminare una directory contenente file o directory.|  
|<xref:Microsoft.VisualBasic.DueDate>|Indica le scadenze dei pagamenti quando vengono chiamati i metodi finanziari.|  
|<xref:Microsoft.VisualBasic.FileIO.FieldType>|Indica se i campi di testo sono delimitati o a larghezza fissa.|  
|<xref:Microsoft.VisualBasic.FileAttribute>|Indica gli attributi file da utilizzare quando si chiamano funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.FirstDayOfWeek>|Indica il primo giorno della settimana da utilizzare quando si chiamano funzioni relative alla data.|  
|<xref:Microsoft.VisualBasic.FirstWeekOfYear>|Indica la prima settimana dell'anno da utilizzare quando si chiamano funzioni relative alla data.|  
|<xref:Microsoft.VisualBasic.MsgBoxResult>|Indica quale pulsante è stato premuto in una finestra di messaggio, restituito dalla funzione <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>.|  
|<xref:Microsoft.VisualBasic.MsgBoxStyle>|Indica quali pulsanti visualizzare quando viene chiamata la funzione <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>.|  
|<xref:Microsoft.VisualBasic.OpenAccess>|Indica la modalità di apertura del file quando si chiamano le funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.OpenMode>|Indica la modalità di apertura del file quando si chiamano le funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.OpenShare>|Indica la modalità di apertura del file quando si chiamano le funzioni di accesso ai file.|  
|<xref:Microsoft.VisualBasic.FileIO.RecycleOption>|Specifica se un file deve essere eliminato in modo permanente o spostato nel Cestino.|  
|<xref:Microsoft.VisualBasic.FileIO.SearchOption>|Specifica se eseguire la ricerca in tutte le directory o solo in quelle di primo livello.|  
|<xref:Microsoft.VisualBasic.TriState>|Indica un valore `Boolean` oppure se è necessario utilizzare l'impostazione predefinita quando si chiamano le funzioni di formattazione dei numeri.|  
|<xref:Microsoft.VisualBasic.FileIO.UICancelOption>|Specifica le azioni da intraprendere se l'utente fa clic su **Annulla** durante un'operazione.|  
|<xref:Microsoft.VisualBasic.FileIO.UIOption>|Specifica se visualizzare una finestra di dialogo di avanzamento durante la copia, l'eliminazione o lo spostamento di file o directory.|  
|<xref:Microsoft.VisualBasic.VariantType>|Indica il tipo di un oggetto Variant restituito dalla funzione <xref:Microsoft.VisualBasic.Information.VarType%2A>.|  
|<xref:Microsoft.VisualBasic.VbStrConv>|Indica il tipo di conversione da eseguire quando viene chiamata la funzione <xref:Microsoft.VisualBasic.Strings.StrConv%2A>.|  
  
## Vedere anche  
 [Visual Basic Language Reference](../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../visual-basic/index.md)   
 [Constants Overview](../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Enumerations Overview](../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)