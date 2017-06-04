---
title: "Cenni preliminari sul componente ErrorProvider (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ErrorProvider"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "messaggi di errore, visualizzazione"
  - "ErrorProvider (componente) [Windows Form], informazioni sul componente ErrorProvider"
  - "errori [Windows Form], visualizzazione per gli utenti"
ms.assetid: ced189f2-b5c8-46a7-a6f1-37f5af95dc99
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari sul componente ErrorProvider (Windows Form)
Il componente [ErrorProvider](../../../../docs/framework/winforms/controls/errorprovider-component-windows-forms.md) di Windows Form è utilizzato per convalidare l'input dell'utente in un form o controllo.  Viene utilizzato in genere in combinazione con la convalida dell'input dell'utente in un form, o con la visualizzazione di errori in un dataset.  Rappresenta una migliore alternativa rispetto alla visualizzazione di un messaggio di errore in una finestra, poiché una volta chiusa la finestra, il messaggio di errore non sarà più visibile.  Il componente <xref:System.Windows.Forms.ErrorProvider> visualizza un'icona di errore \(![Icona ErrorProvider](../../../../docs/framework/winforms/controls/media/vberrorprovidericon.png "vbErrorProviderIcon")\) accanto al relativo controllo, ad esempio una casella di testo. Quando l'utente posiziona il puntatore del mouse sull'icona di errore, viene visualizzata una descrizione comandi con la stringa del messaggio di errore.  
  
## Proprietà principali  
 Le proprietà principali del componente <xref:System.Windows.Forms.ErrorProvider> sono <xref:System.Windows.Forms.ErrorProvider.DataSource%2A>, <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> e <xref:System.Windows.Forms.ErrorProvider.Icon%2A>.  Se si utilizza il componente <xref:System.Windows.Forms.ErrorProvider> con i controlli di associazione dati, la proprietà <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> deve essere impostata sul contenitore appropriato, in genere Windows Form, in modo che il componente possa visualizzare un'icona di errore nel form.  Quando il componente viene aggiunto nella finestra di progettazione, la proprietà <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> è impostata sul relativo form; se si aggiunge il controllo nel codice, sarà necessario impostarla manualmente.  
  
 La proprietà <xref:System.Windows.Forms.ErrorProvider.Icon%2A> può essere impostata su un'icona di errore personalizzata anziché su quella predefinita.  Quando è impostata la proprietà <xref:System.Windows.Forms.ErrorProvider.DataSource%2A>, il componente <xref:System.Windows.Forms.ErrorProvider> può visualizzare messaggi di errore per un dataset.  Il metodo principale del componente <xref:System.Windows.Forms.ErrorProvider> è il metodo <xref:System.Windows.Forms.ErrorProvider.SetError%2A>, che consente di specificare la stringa del messaggio di errore e la posizione in cui dovrà essere visualizzata l'icona.  
  
> [!NOTE]
>  Il componente <xref:System.Windows.Forms.ErrorProvider> non fornisce supporto incorporato per i client di accessibilità.  Per rendere accessibile l'applicazione quando si utilizza questo componente, è necessario fornire un meccanismo di informazione supplementare accessibile.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ErrorProvider>   
 [Procedura: visualizzare errori in un dataset tramite il componente ErrorProvider di Windows Form](../../../../docs/framework/winforms/controls/view-errors-within-a-dataset-with-wf-errorprovider-component.md)   
 [Procedura: visualizzare le icone di errori per la convalida dei form con il componente ErrorProvider di Windows Form](../../../../docs/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider.md)