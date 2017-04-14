---
title: "Cenni preliminari sul controllo SplitContainer (Windows Form) | Microsoft Docs"
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
  - "SplitContainer"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "SplitContainer (controllo) [Windows Form], informazioni sul controllo SplitContainer"
ms.assetid: 6de5a5f7-97a5-402d-be6d-7e2785483db5
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo SplitContainer (Windows Form)
Il controllo <xref:System.Windows.Forms.SplitContainer> Windows Form può essere considerato un oggetto composto, poiché è costituito da due pannelli separati da una barra mobile.  Quando il puntatore del mouse viene posizionato sopra la barra, assume una forma diversa per indicare che la barra è mobile.  
  
> [!IMPORTANT]
>  Nella **Casella degli strumenti**, il controllo <xref:System.Windows.Forms.SplitContainer> sostituisce il controllo <xref:System.Windows.Forms.Splitter> della versione precedente di [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  È consigliabile utilizzare il controllo <xref:System.Windows.Forms.SplitContainer> anziché il controllo <xref:System.Windows.Forms.Splitter>.  La classe <xref:System.Windows.Forms.Splitter> è ancora inclusa in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per assicurare la compatibilità con le applicazioni esistenti, tuttavia per i nuovi progetti si consiglia di utilizzare il controllo <xref:System.Windows.Forms.SplitContainer>.  
  
 Il controllo <xref:System.Windows.Forms.SplitContainer> consente di creare complesse interfacce utente, in cui l'elemento selezionato in un pannello determina in genere gli oggetti visualizzati nell'altro.  Questa disposizione è particolarmente efficace per la visualizzazione e la ricerca di informazioni.  Grazie alla presenza dei due pannelli è possibile aggregare le informazioni in aree, mentre la barra di divisione consente di ridimensionare i pannelli.  
  
 È inoltre possibile annidare più controlli <xref:System.Windows.Forms.SplitContainer>, orientando il secondo controllo <xref:System.Windows.Forms.SplitContainer> orizzontalmente, per creare un pannello superiore e un pannello inferiore.  
  
 Il controllo <xref:System.Windows.Forms.SplitContainer> è accessibile da tastiera per impostazione predefinita. Per spostare la barra di divisione è sufficiente premere i tasti di direzione, se la proprietà <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> è impostata su `false`.  
  
 La proprietà <xref:System.Windows.Forms.SplitContainer.Orientation%2A> del controllo <xref:System.Windows.Forms.SplitContainer> determina la direzione della barra di divisione, non del controllo stesso.  Quando tale proprietà è impostata su <xref:System.Windows.Forms.Orientation>, la barra di divisione è disposta in verticale, creando un pannello a destra e uno a sinistra.  
  
 Il valore della proprietà <xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A> dipende inoltre da quello della proprietà <xref:System.Windows.Forms.SplitContainer.Orientation%2A>.  Per ulteriori informazioni, vedere l'argomento relativo alla proprietà <xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A>.  
  
 È inoltre possibile limitare le dimensioni e lo spostamento del controllo <xref:System.Windows.Forms.SplitContainer>.  La proprietà <xref:System.Windows.Forms.SplitContainer.FixedPanel%2A> determina il pannello le cui dimensioni devono rimanere invariate in caso di ridimensionamento del controllo <xref:System.Windows.Forms.SplitContainer>, mentre la proprietà <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> determina se la barra di divisione può essere spostata tramite mouse o tastiera.  
  
> [!NOTE]
>  Anche se la proprietà <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> è impostata su `true`, la barra di divisione può essere comunque spostata a livello di codice, ad esempio utilizzando la proprietà <xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A>.  
  
 Per ciascun pannello del controllo <xref:System.Windows.Forms.SplitContainer> sono infine disponibili proprietà che consentono di determinarne le dimensioni.  
  
## Proprietà, metodi ed eventi di uso comune  
  
|Nome|Descrizione|  
|----------|-----------------|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.FixedPanel%2A>|Determina il pannello le cui dimensioni devono rimanere invariate in caso di ridimensionamento del controllo <xref:System.Windows.Forms.SplitContainer>.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A>|Determina se la barra di divisione può essere spostata tramite mouse o tastiera.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.Orientation%2A>|Determina se la barra di divisione deve essere disposta in orizzontale o in verticale.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A>|Determina la distanza in pixel dal bordo superiore o sinistro alla barra di divisione mobile.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>|Determina la distanza minima in pixel per cui la barra di divisione può essere spostata dall'utente.|  
|Proprietà <xref:System.Windows.Forms.SplitContainer.SplitterWidth%2A>|Determina lo spessore in pixel della barra di divisione.|  
|Evento <xref:System.Windows.Forms.SplitContainer.SplitterMoving>|Viene generato durante lo spostamento della barra di divisione.|  
|Evento <xref:System.Windows.Forms.SplitContainer.SplitterMoved>|Viene generato al termine dello spostamento della barra di divisione.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 [Controllo SplitContainer](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)   
 [SplitContainer Control Sample](http://msdn.microsoft.com/it-it/9015fad0-7108-4d85-a83a-a72d038c4f65)