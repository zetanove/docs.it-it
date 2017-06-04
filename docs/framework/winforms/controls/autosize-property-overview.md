---
title: "Cenni preliminari sulla propriet&#224; AutoSize | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ridimensionamento automatico"
  - "AutoSize (proprietà)"
  - "AutoSizeMode (proprietà)"
  - "layout [Windows Form], AutoSize"
  - "ridimensionamento, automatico"
ms.assetid: 62fd82a2-9565-4f65-925b-9d1e66dc4e7d
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari sulla propriet&#224; AutoSize
La proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> consente a un controllo di modificare le proprie dimensioni, se necessario, in modo da riflettere il valore specificato dalla proprietà <xref:System.Windows.Forms.Control.PreferredSize%2A>.  Impostare la proprietà `AutoSizeMode` per regolare il comportamento del ridimensionamento per controlli specifici.  
  
## Comportamento di AutoSize  
 La proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> è supportata solo da alcuni controlli.  Inoltre, alcuni controlli che supportano la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> supportano anche la proprietà `AutoSizeMode`.  
  
 La proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> determina un comportamento leggermente diverso a seconda del tipo di controllo specifico e del valore della proprietà `AutoSizeMode`, se disponibile.  Nella tabella riportata di seguito sono elencati i comportamenti sempre validi e ne viene fornita una breve descrizione.  
  
|Comportamento sempre valido|Descrizione|  
|---------------------------------|-----------------|  
|Il ridimensionamento automatico è una funzionalità di runtime.|Questo significa che un controllo non viene mai ingrandito o ridotto e quindi non produce ulteriori effetti.|  
|Se le dimensioni di un controllo cambiano, il valore della relativa proprietà <xref:System.Windows.Forms.Control.Location%2A> rimane invariato.|Se un controllo viene ingrandito per fare spazio al contenuto, l'aumento di dimensioni avviene verso destra e verso il basso.  I controlli non vengono estesi verso sinistra.|  
|Le proprietà <xref:System.Windows.Forms.Control.Dock%2A> e <xref:System.Windows.Forms.Control.Anchor%2A> vengono rispettate quando <xref:System.Windows.Forms.Control.AutoSize%2A> è `true`.|Il valore della proprietà <xref:System.Windows.Forms.Control.Location%2A> del controllo viene modificato e impostato sul valore corretto.<br /><br /> **Nota** Il controllo <xref:System.Windows.Forms.Label> è un'eccezione a questa regola.  Se la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> di un controllo <xref:System.Windows.Forms.Label> ancorato viene impostata su `true`, il controllo <xref:System.Windows.Forms.Label> non viene esteso.|  
|Le proprietà <xref:System.Windows.Forms.Control.MaximumSize%2A> e <xref:System.Windows.Forms.Control.MinimumSize%2A> di un controllo vengono sempre rispettate, indipendentemente dal valore della relativa proprietà <xref:System.Windows.Forms.Control.AutoSize%2A>.|Le proprietà <xref:System.Windows.Forms.Control.MaximumSize%2A> e <xref:System.Windows.Forms.Control.MinimumSize%2A> non vengono influenzate dalla proprietà <xref:System.Windows.Forms.Control.AutoSize%2A>.|  
|Non esiste un'impostazione predefinita delle dimensioni minime.|Questo significa che se le dimensioni di un controllo senza contenuto vengono ridotte a causa di <xref:System.Windows.Forms.Control.AutoSize%2A>, il valore della proprietà <xref:System.Windows.Forms.Control.Size%2A> diventerà 0,0 e  il controllo verrà ridotto a un punto, risultando quindi praticamente invisibile.|  
|Se un controllo non implementa il metodo <xref:System.Windows.Forms.Control.GetPreferredSize%2A>, il metodo <xref:System.Windows.Forms.Control.GetPreferredSize%2A> restituisce l'ultimo valore assegnato alla proprietà <xref:System.Windows.Forms.Control.Size%2A>.|Questo significa che l'impostazione di <xref:System.Windows.Forms.Control.AutoSize%2A> su `true` non avrà alcun effetto.|  
|Un controllo all'interno di una cella <xref:System.Windows.Forms.TableLayoutPanel> viene sempre ridotto per adattarlo alle dimensioni della cella fino a raggiungere il valore <xref:System.Windows.Forms.Control.MinimumSize%2A>.|Queste dimensioni sono quelle massime consentite.  La situazione è diversa se la cella appartiene a una riga o colonna di tipo <xref:System.Windows.Forms.SizeType>.|  
  
## Proprietà AutoSizeMode  
 La proprietà `AutoSizeMode` offre un controllo più preciso sul comportamento predefinito di <xref:System.Windows.Forms.Control.AutoSize%2A>.  La proprietà `AutoSizeMode` specifica in che modo un controllo si ridimensiona in base al contenuto,  che può essere, ad esempio, il testo per un controllo <xref:System.Windows.Forms.Button> o i controlli figlio per un contenitore.  
  
 Nella tabella riportata di seguito sono illustrate le impostazioni di <xref:System.Windows.Forms.AutoSizeMode> e viene fornita una descrizione del comportamento determinato da ciascuna impostazione.  
  
|Impostazione di AutoSizeMode|Comportamento|  
|----------------------------------|-------------------|  
|GrowAndShrink|Il controllo si ingrandisce o si riduce per adattarsi al contenuto.<br /><br /> I valori di <xref:System.Windows.Forms.Control.MinimumSize%2A> e <xref:System.Windows.Forms.Control.MaximumSize%2A> vengono rispettati ma il valore corrente della proprietà <xref:System.Windows.Forms.Control.Size%2A> viene ignorato.<br /><br /> Il comportamento è analogo a quello dei controlli con proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> e senza proprietà `AutoSizeMode`.|  
|GrowOnly|Il controllo si ingrandisce fino alle dimensioni necessarie per racchiudere il contenuto, ma non si riduce al di sotto del valore specificato dalla relativa proprietà <xref:System.Windows.Forms.Control.Size%2A>.<br /><br /> Questo è il valore predefinito per `AutoSizeMode`.|  
  
## Controlli che supportano la proprietà AutoSize  
 Nella tabella riportata di seguito sono elencati i controlli che supportano le proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> e `AutoSizeMode`.  
  
|Supporto AutoSize|Tipo di controllo|  
|-----------------------|-----------------------|  
|-   Proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> supportata.<br />-   Nessuna proprietà `AutoSizeMode`.|<xref:System.Windows.Forms.CheckBox><br /><br /> <xref:System.Windows.Forms.DomainUpDown><br /><br /> <xref:System.Windows.Forms.Label><br /><br /> <xref:System.Windows.Forms.LinkLabel><br /><br /> <xref:System.Windows.Forms.MaskedTextBox> \(<xref:System.Windows.Forms.TextBox> base\)<br /><br /> <xref:System.Windows.Forms.NumericUpDown><br /><br /> <xref:System.Windows.Forms.RadioButton><br /><br /> <xref:System.Windows.Forms.TextBox><br /><br /> <xref:System.Windows.Forms.TrackBar>|  
|-   Proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> supportata.<br />-   Proprietà `AutoSizeMode` supportata.|<xref:System.Windows.Forms.Button><br /><br /> <xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.FlowLayoutPanel><br /><br /> <xref:System.Windows.Forms.Form><br /><br /> <xref:System.Windows.Forms.GroupBox><br /><br /> <xref:System.Windows.Forms.Panel><br /><br /> <xref:System.Windows.Forms.TableLayoutPanel>|  
|-   Nessuna proprietà <xref:System.Windows.Forms.Control.AutoSize%2A>.|<xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.ComboBox><br /><br /> <xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DateTimePicker><br /><br /> <xref:System.Windows.Forms.ListBox><br /><br /> <xref:System.Windows.Forms.ListView><br /><br /> <xref:System.Windows.Forms.MaskedTextBox><br /><br /> <xref:System.Windows.Forms.MonthCalendar><br /><br /> <xref:System.Windows.Forms.ProgressBar><br /><br /> <xref:System.Windows.Forms.PropertyGrid><br /><br /> <xref:System.Windows.Forms.RichTextBox><br /><br /> <xref:System.Windows.Forms.SplitContainer><br /><br /> <xref:System.Windows.Forms.TabControl><br /><br /> <xref:System.Windows.Forms.TabPage><br /><br /> <xref:System.Windows.Forms.TreeView><br /><br /> <xref:System.Windows.Forms.WebBrowser><br /><br /> <xref:System.Windows.Forms.ScrollBar>|  
  
## AutoSize nell'ambiente di progettazione  
 Nella tabella riportata di seguito viene descritto il comportamento del ridimensionamento di un controllo in fase di progettazione, in base al valore delle relative proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> e `AutoSizeMode`.  
  
 Eseguire l'override della proprietà <xref:System.Windows.Forms.Design.ControlDesigner.SelectionRules%2A> per determinare se un dato controllo può essere ridimensionato dall'utente.  Nella tabella riportata di seguito "non può" significa solo <xref:System.Windows.Forms.Design.SelectionRules> mentre "può" significa <xref:System.Windows.Forms.Design.SelectionRules> e <xref:System.Windows.Forms.Design.SelectionRules>.  
  
|Impostazioni di AutoSize|Azione di ridimensionamento in fase di progettazione|  
|------------------------------|----------------------------------------------------------|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `true`<br />-   Nessuna proprietà `AutoSizeMode`.|Il controllo non può essere ridimensionato dall'utente in fase di progettazione, con le seguenti eccezioni:<br /><br /> -   <xref:System.Windows.Forms.TextBox><br />-   <xref:System.Windows.Forms.MaskedTextBox><br />-   <xref:System.Windows.Forms.RichTextBox><br />-   <xref:System.Windows.Forms.TrackBar>|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `true`<br />-   `AutoSizeMode` \= <xref:System.Windows.Forms.AutoSizeMode>|Il controllo non può essere ridimensionato dall'utente in fase di progettazione.|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `true`<br />-   `AutoSizeMode` \= <xref:System.Windows.Forms.AutoSizeMode>|Il controllo può essere ridimensionato dall'utente in fase di progettazione.  Una volta impostata la proprietà <xref:System.Windows.Forms.Control.Size%2A>, l'utente può solo aumentare le dimensioni del controllo.|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `false` o la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> è nascosta.|Il controllo può essere ridimensionato dall'utente in fase di progettazione.|  
  
> [!NOTE]
>  Per ottimizzare la produttività, Progettazione Windows Form esegue lo shadowing della proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> per la classe <xref:System.Windows.Forms.Form>.  In fase di progettazione il form si comporta come se la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> fosse impostata su `false`, a prescindere dall'impostazione effettiva.  In fase di esecuzione non vengono effettuati adattamenti particolari e la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> viene applicata in base a quanto specificato dalla relativa impostazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.AutoSize%2A>   
 <xref:System.Windows.Forms.Control.PreferredSize%2A>   
 <xref:System.Windows.Forms.Control.GetPreferredSize%2A>