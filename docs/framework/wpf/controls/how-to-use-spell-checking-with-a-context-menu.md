---
title: "Procedura: utilizzare il controllo ortografico con un menu di scelta rapida | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controllo ortografico in una casella di testo (abilitazione) [WPF]"
  - "controllo ortografico in una casella di testo (riabilitazione) [WPF]"
  - "controllo ortografico con un menu di scelta rapida [WPF]"
ms.assetid: 61f69a20-2ff3-4056-9060-e32f4483ec5e
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: utilizzare il controllo ortografico con un menu di scelta rapida
Per impostazione predefinita, quando si abilita il controllo ortografico in un controllo di modifica come <xref:System.Windows.Controls.TextBox> o <xref:System.Windows.Controls.RichTextBox>, si ottengono opzioni di scelta per il controllo ortografico nel menu di scelta rapida.  Ad esempio, quando un utente fa clic con il pulsante destro del mouse su una parola con ortografia errata, vengono visualizzati alcuni suggerimenti di ortografia oppure l'opzione **Ignora tutto**.  Tuttavia, quando si esegue l'override del menu di scelta rapida predefinito con un menu di scelta rapida personalizzato, questa funzionalità viene persa ed è necessario scrivere codice specifico per abilitare nuovamente la funzionalità di controllo ortografico nel menu di scelta rapida.  Nell'esempio riportato di seguito viene illustrato come abilitare questa funzionalità in <xref:System.Windows.Controls.TextBox>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato il codice [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] che crea un oggetto <xref:System.Windows.Controls.TextBox> con alcuni eventi utilizzati per implementare il menu di scelta rapida.  
  
 [!code-xml[TextBoxMiscSnippets_snip#SpellerCustomContextMenuExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml#spellercustomcontextmenuexamplewholepage)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato il codice che implementa il menu di scelta rapida.  
  
 [!code-csharp[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml.cs#spellercustomcontextmenucodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/speller_custom_context_menu.xaml.vb#spellercustomcontextmenucodeexamplewholepage)]  
  
 Il codice utilizzato per eseguire questa operazione con <xref:System.Windows.Controls.RichTextBox> è simile.  La differenza principale è data dal parametro passato al metodo `GetSpellingError`.  Per <xref:System.Windows.Controls.TextBox>, passare l'indice integer della posizione del punto di inserimento:  
  
 `spellingError = myTextBox.GetSpellingError(caretIndex);`  
  
 Per <xref:System.Windows.Controls.RichTextBox>, passare l'oggetto <xref:System.Windows.Documents.TextPointer> che specifica la posizione del punto di inserimento:  
  
 `spellingError = myRichTextBox.GetSpellingError(myRichTextBox.CaretPosition);`  
  
## Vedere anche  
 [Cenni preliminari sulla classe TextBox](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [Cenni generali sul controllo RichTextBox](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [Attivare il controllo ortografico in un controllo di modifica del testo](../../../../docs/framework/wpf/controls/how-to-enable-spell-checking-in-a-text-editing-control.md)   
 [Utilizzare un menu di scelta rapida personalizzato con un oggetto TextBox](../../../../docs/framework/wpf/controls/how-to-use-a-custom-context-menu-with-a-textbox.md)