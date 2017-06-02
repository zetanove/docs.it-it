---
title: "Procedura: visualizzare la Guida in un&#39;applicazione Windows | Microsoft Docs"
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
  - "form, supporto della Guida"
  - "Guida, Windows (applicazioni)"
  - "HelpProvider (componente) [Windows Form]"
  - "HTML (Guida), Windows Form"
  - "Windows (applicazioni), supporto della Guida"
ms.assetid: 7c4e5cec-2bd2-4f0b-8d75-c2b88929bd61
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: visualizzare la Guida in un&#39;applicazione Windows
È possibile utilizzare il componente <xref:System.Windows.Forms.HelpProvider> per includere argomenti della Guida all'interno di una file della guida in controlli specifici in Windows Form.  Il file della Guida può essere in formato HTML o HTMLHelp 1.X o superiore.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per visualizzare la Guida  
  
1.  Dalla **Casella degli strumenti** trascinare un componente <xref:System.Windows.Forms.HelpProvider> nel form.  
  
     Il componente verrà posizionato nella barra delle applicazioni nella parte inferiore di Progettazione di Windows Form.  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> sul file della Guida chm, col o htm.  
  
3.  Selezionare un altro controllo presente nel form e impostare la proprietà [HelpKeyword](frlrfSystemWindowsFormsHelpProviderClassSetHelpKeywordTopic) nella finestra **Proprietà**.  
  
     Questa è la stringa passata tramite il componente <xref:System.Windows.Forms.HelpProvider> al file della Guida per richiamare l'argomento appropriato.  
  
4.  Nella finestra **Proprietà**, impostare la proprietà [HelpNavigator](frlrfSystemWindowsFormsHelpProviderClassSetHelpNavigatorTopic) su un valore dell'enumerazione <xref:System.Windows.Forms.HelpNavigator>.  
  
     Questa impostazione determina la modalità in cui la proprietà **HelpKeyword** viene passata al sistema della Guida.  Nella tabella riportata di seguito sono elencate tutte le impostazioni e le relative descrizioni.  
  
    |Nome del membro|Descrizione|  
    |---------------------|-----------------|  
    |AssociateIndex|Specifica che l'indice di un argomento specificato viene eseguito nell'URL specificato.|  
    |Find|Specifica che viene visualizzata la pagina di ricerca di un URL specificato.|  
    |Indice|Specifica che viene visualizzato l'indice di un URL specificato.|  
    |KeywordIndex|Specifica una parola chiave da cercare e l'azione da eseguire nell'URL specificato.|  
    |TableOfContents|Specifica che vengono visualizzati gli argomenti della Guida del file della Guida HTML 1.0.|  
    |Argomento|Specifica che viene visualizzato l'argomento a cui fa riferimento l'URL specificato.|  
  
 In fase di esecuzione, premendo F1 quando il controllo per il quale si sono impostate le proprietà **HelpKeyword** e **HelpNavigator** ha lo stato attivo verrà visualizzato il file della Guida associato al componente <xref:System.Windows.Forms.HelpProvider>.  
  
 Attualmente la proprietà **HelpNamespace** supporta i file della Guida nei formati HTMLHelp 1.x, HTMLHelp 2.0 e HTML.  È quindi possibile impostare la proprietà **HelpNamespace** su un indirizzo http:\/\/, ad esempio una pagina Web.  In tal caso, verrà visualizzata nel browser predefinito la pagina Web con la stringa specificata nella proprietà **HelpKeyword** utilizzata come ancoraggio.  L'ancoraggio è utilizzato per passare direttamente a una parte specifica di una pagina HTML.  
  
> [!IMPORTANT]
>  Accertarsi di controllare ogni informazione inviata da un client prima di utilizzarla in un'applicazione,  poiché utenti con pochi scrupoli possono tentare di inviare script eseguibili, istruzioni SQL o altro codice.  Prima di visualizzare l'input di un utente, memorizzarlo in un database o utilizzarlo, verificare che non contenga informazioni potenzialmente pericolose.  Un modo per effettuare questo controllo consiste nell'utilizzo di un'espressione regolare per cercare parole chiave come "SCRIPT" quando si riceve input da un utente.  
  
 È inoltre possibile utilizzare il componente <xref:System.Windows.Forms.HelpProvider> per visualizzare la Guida rapida, anche se è stata configurata per la visualizzazione dei file della Guida per i controlli nei Windows Form.  Per ulteriori informazioni, vedere [Procedura: visualizzare la Guida rapida](../../../../docs/framework/winforms/advanced/how-to-display-pop-up-help.md).  
  
## Vedere anche  
 [Procedura: visualizzare la Guida rapida](../../../../docs/framework/winforms/advanced/how-to-display-pop-up-help.md)   
 [Visualizzazione della Guida relativa a un controllo tramite le descrizioni comandi](../../../../docs/framework/winforms/advanced/control-help-using-tooltips.md)   
 [Integrazione della Guida dell'utente in Windows Form](../../../../docs/framework/winforms/advanced/integrating-user-help-in-windows-forms.md)   
 [Windows Form](../../../../docs/framework/winforms/index.md)