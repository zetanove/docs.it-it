---
title: "Suggerimenti per il controllo TableLayoutPanel | Microsoft Docs"
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
  - "AutoSize (proprietà), TableLayoutPanel (controllo)"
  - "procedure ottimali, TableLayoutPanel (controllo)"
  - "controlli [Windows Form], ridimensionamento"
  - "form, procedure ottimali"
  - "layout [Windows Form]"
  - "layout [Windows Form], procedure ottimali"
  - "layout [Windows Form], AutoSize"
  - "ridimensionamento, automatico"
  - "TableLayoutPanel (controllo) [Windows Form], procedure ottimali"
  - "TableLayoutPanel (controllo) [Windows Form], AutoSize (comportamento)"
ms.assetid: b6706efb-d7a4-45ec-8cf4-08fa993e3afb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Suggerimenti per il controllo TableLayoutPanel
Il controllo <xref:System.Windows.Forms.TableLayoutPanel> fornisce potenti funzioni di layout che vanno esaminate attentamente prima di essere utilizzate con Windows Form.  
  
## Consigli  
 I consigli seguenti hanno lo scopo di spiegare come sfruttare al massimo il controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
### Utilizzo mirato  
 Utilizzare il controllo <xref:System.Windows.Forms.TableLayoutPanel> sporadicamente.  Non utilizzarlo in tutte le situazioni che richiedono un layout ridimensionabile.  Nell'elenco seguente vengono descritti i layout che traggono i maggiori vantaggi dall'uso del controllo <xref:System.Windows.Forms.TableLayoutPanel>:  
  
-   Layout in cui vi sono più parti del form ridimensionabili proporzionalmente l'una all'altra.  
  
-   Layout che verranno modificati o generati dinamicamente in fase di esecuzione, ad esempio i form per l'immissione di dati in cui vengono aggiunti o rimossi campi personalizzabili dall'utente in base alle preferenze.  
  
-   Layout le cui dimensioni globali dovrebbero rimanere fisse.  Ad esempio, è possibile che vi sia una finestra di dialogo le cui dimensioni devono rimanere inferiori a 800 x 600, ma che deve supportare le stringhe localizzate.  
  
 Nell'elenco seguente vengono descritti i layout che non traggono grandi vantaggi dall'utilizzo del controllo <xref:System.Windows.Forms.TableLayoutPanel>:  
  
-   Form per l'immissione di dati semplici con una colonna di etichette e una colonna di aree per l'immissione di testo.  
  
-   Form con un'unica area di visualizzazione di grandi dimensioni che deve occupare tutto lo spazio disponibile quando un form viene ridimensionato.  Un esempio è un form che consente di visualizzare un unico controllo <xref:System.Windows.Forms.PropertyGrid>.  In questo caso utilizzare l'ancoraggio perché nessun altro elemento deve venire espanso quando il form viene ridimensionato.  
  
 Scegliere con attenzione i controlli che devono essere inseriti in un controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Se è disponibile spazio per aumentare la dimensione del testo del 30% tramite ancoraggio, è consigliabile utilizzare solo la proprietà <xref:System.Windows.Forms.Control.Anchor%2A>.  Se è possibile stimare lo spazio richiesto dal layout, è più facile utilizzare <xref:System.Windows.Forms.Control.Dock%2A> e <xref:System.Windows.Forms.Control.Anchor%2A> anziché stimare i dettagli dello spazio rimanente e del comportamento di <xref:System.Windows.Forms.Control.AutoSize%2A>.  
  
 In generale, quando si progetta il layout con il controllo <xref:System.Windows.Forms.TableLayoutPanel>, utilizzare una progettazione più semplice possibile.  
  
### Utilizzare la finestra Struttura documento  
 La finestra Struttura documento fornisce una visualizzazione struttura ad albero del layout, che è possibile utilizzare per modificare l'ordine Z e le relazioni padre\-figlio dei controlli.  Scegliere **Altre finestre** dal menu **Visualizza**, quindi **Struttura documento**.  
  
### Evitare l'annidamento  
 Evitare di annidare altri controlli <xref:System.Windows.Forms.TableLayoutPanel> in un controllo <xref:System.Windows.Forms.TableLayoutPanel>.  Il debug dei layout annidati può essere difficile.  
  
### Evitare l'ereditarietà visiva  
 Il controllo <xref:System.Windows.Forms.TableLayoutPanel> non supporta l'ereditarietà visiva in Progettazione Windows Forms.  Il controllo <xref:System.Windows.Forms.TableLayoutPanel> in una classe derivata appare bloccato in fase di progettazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TableLayoutPanel>   
 <xref:System.Windows.Forms.FlowLayoutPanel>