---
title: "Procedura: implementare la convalida dell&#39;associazione | Microsoft Docs"
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
  - "associazione, convalida"
  - "associazione dati, convalida dell'associazione"
  - "convalida dell'associazione"
ms.assetid: eb98b33d-9866-49ae-b981-bc5ff20d607a
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: implementare la convalida dell&#39;associazione
In questo esempio viene mostrato come utilizzare un oggetto <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> e un trigger dello stile per fornire un feedback visivo e informare l'utente quando viene immesso un valore non valido in base a una regola di convalida personalizzata.  
  
## Esempio  
 Il contenuto di testo dell'oggetto <xref:System.Windows.Controls.TextBox> dell'esempio seguente è associato alla proprietà `Age` \(di tipo int\) di un oggetto [origine di associazione](GTMT) denominato `ods`.  L'associazione viene configurata per utilizzare una regola di convalida denominata `AgeRangeRule` in modo che se l'utente immette caratteri non numerici o un valore inferiore a 21 o maggiore di 130, accanto alla casella di testo viene visualizzato un punto esclamativo rosso e quando l'utente sposta il mouse sulla casella di testo viene visualizzata una descrizione comandi con il messaggio di errore.  
  
 [!code-xml[BindValidation#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#2)]  
  
 Nell'esempio seguente viene mostrata l'implementazione di `AgeRangeRule` che eredita da <xref:System.Windows.Controls.ValidationRule> ed esegue l'override del metodo <xref:System.Windows.Controls.ValidationRule.Validate%2A>.  Il metodo Int32.Parse\(\) viene chiamato sul valore per assicurarsi che non contenga caratteri non validi.  Il metodo <xref:System.Windows.Controls.ValidationRule.Validate%2A> restituisce <xref:System.Windows.Controls.ValidationResult> che indica se il valore è valido in base al fatto che venga rilevata un'eccezione durante l'analisi e che il valore di durata non rientri nell'intervallo compreso tra i limiti inferiore e superiore.  
  
 [!code-csharp[BindValidation#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/AgeRangeRule.cs#3)]  
  
 Nell'esempio seguente viene mostrato l'oggetto <xref:System.Windows.Controls.ControlTemplate> `validationTemplate` personalizzato che crea un punto esclamativo rosso per notificare all'utente un errore di convalida.  I modelli di controllo vengono utilizzati per ridefinire l'aspetto di un controllo.  
  
 [!code-xml[BindValidation#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#4)]  
  
 Come mostrato nell'esempio seguente, l'oggetto <xref:System.Windows.Controls.ToolTip> che visualizza il messaggio di errore viene creato utilizzando lo stile denominato `textBoxInError`.  Se il valore di <xref:System.Windows.Controls.Validation.HasError%2A> è `true`, il trigger imposta la descrizione comandi dell'oggetto <xref:System.Windows.Controls.TextBox> corrente sul primo errore di convalida.  L'oggetto <xref:System.Windows.Data.Binding.RelativeSource%2A> viene impostato su <xref:System.Windows.Data.RelativeSourceMode> che fa riferimento all'elemento corrente.  
  
 [!code-xml[BindValidation#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindValidation/CSharp/Window1.xaml#5)]  
  
 Per l'esempio completo, vedere [Esempio Binding Validation](http://go.microsoft.com/fwlink/?LinkID=159972) \(la pagina potrebbe essere in inglese\).  
  
 Notare che se non si fornisce un oggetto <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> personalizzato, il modello di errori predefinito sembra fornire un feedback visivo all'utente, quando si verifica un errore di convalida.  Per ulteriori informazioni, vedere "Convalida dei dati" in [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  Inoltre, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene fornita una regola di convalida incorporata che rileva le eccezioni generate durante l'aggiornamento della proprietà dell'origine di associazione.  Per ulteriori informazioni, vedere <xref:System.Windows.Controls.ExceptionValidationRule>.  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)