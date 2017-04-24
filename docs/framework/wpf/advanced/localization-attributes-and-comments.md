---
title: "Attributi e commenti di localizzazione | Microsoft Docs"
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
  - "localizzazione, attributi"
  - "localizzazione, commenti"
ms.assetid: ead2d9ac-b709-4ec1-a924-39927a29d02f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Attributi e commenti di localizzazione
I commenti di localizzazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] sono proprietà all'interno del codice sorgente [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)], usati dagli sviluppatori per fornire regole o suggerimenti per i localizzatori.  I commenti di localizzazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] contengono due set di informazioni: attributi di localizzabilità e commenti di localizzazione in formato libero.  Gli attributi di localizzabilità vengono utilizzati dall'API di localizzazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per indicare le risorse da localizzare.  I commenti in formato libero comprendono tutte le informazioni che l'autore dell'applicazione desidera includere.  
  
   
  
<a name="Localizer_Comments_"></a>   
## Commenti di localizzazione  
 Se gli autori dell'applicazione di markup necessitano di elementi specifici nel codice [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)], ad esempio vincoli relativi alla lunghezza del testo, alla famiglia o alla dimensione dei caratteri, possono trasmettere queste informazioni ai localizzatori con commenti nel codice [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)].  Di seguito viene riportato il processo di aggiunta di commenti al codice sorgente:  
  
1.  Lo sviluppatore dell'applicazione aggiunge i commenti di localizzazione al codice sorgente di [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)].  
  
2.  Durante il processo di compilazione, nel file proj è possibile specificare se mantenere i commenti di localizzazione in formato libero nell'assembly oppure se rimuoverne una parte o tutti.  I commenti rimossi vengono collocati in un file separato.  L'opzione viene specificata utilizzando un tag `LocalizationDirectivesToLocFile`, ad esempio:  
  
     `<LocalizationDirectivesToLocFile>` *valore* `</LocalizationDirectivesToLocFile>`  
  
3.  Di seguito vengono riportati i valori che è possibile assegnare:  
  
    -   **None**: i commenti e gli attributi rimangono entrambi nell'assembly e non viene generato alcun file separato.  
  
    -   **CommentsOnly**: dall'assembly vengono rimossi solo i commenti, che vengono collocati nel LocFile separato.  
  
    -   **All**: dall'assembly vengono rimossi sia i commenti, sia gli attributi che vengono collocati entrambi in un LocFile separato.  
  
4.  Se le risorse localizzabili vengono estratte da [!INCLUDE[TLA2#tla_baml](../../../../includes/tla2sharptla-baml-md.md)], gli attributi di localizzazione vengono rispettati dall'API di localizzazione di [!INCLUDE[TLA2#tla_baml](../../../../includes/tla2sharptla-baml-md.md)].  
  
5.  I file dei commenti di localizzazione, nei quali sono contenuti solo commenti in formato libero, vengono incorporati al processo di localizzazione in un secondo momento.  
  
 Nell'esempio riportato di seguito viene illustrato come aggiungere commenti di localizzazione a un file [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)].  
  
 `<TextBlock x:Id = "text01"`  
  
 `FontFamily = "Microsoft Sans Serif"`  
  
 `FontSize = "12"`  
  
 `Localization.Attributes = "$Content (Unmodifiable Readable Text)`  
  
 `FontFamily (Unmodifiable Readable)"`  
  
 `Localization.Comments = "$Content (Trademark)`  
  
 `FontSize (Trademark font size)" >`  
  
 `Microsoft`  
  
 `</TextBlock>`  
  
 Nell'esempio precedente, nella sezione Localization.Attributes erano disponibili gli attributi di localizzazione, mentre nella sezione Localization.Comments i commenti in formato libero.  Nella tabella riportata di seguito vengono illustrati gli attributi, i commenti e il relativo significato per il localizzatore.  
  
|Attributi di localizzazione|Significato|  
|---------------------------------|-----------------|  
|$Content \(testo leggibile immodificabile\)|Il contenuto dell'elemento TextBlock non può essere modificato.  I localizzatori non possono modificare la parola "Microsoft".  Il contenuto è visibile \(leggibile\) al localizzatore.  La categoria del contenuto è testo.|  
|FontFamily \(leggibile immodificabile\)|La proprietà della famiglia di caratteri dell'elemento TextBlock non può essere modificata, ma è visibile al localizzatore.|  
  
|Commenti di localizzazione in formato libero|Significato|  
|--------------------------------------------------|-----------------|  
|$Content \(marchio\)|L'autore dell'applicazione indica al localizzatore che il contenuto dell'elemento TextBlock è un marchio.|  
|FontSize \(dimensione del carattere del marchio\)|L'autore dell'applicazione indica che la proprietà della dimensione del carattere deve rispettare la dimensione standard del marchio.|  
  
### Attributi di localizzabilità  
 Le informazioni disponibili nella sezione Localization.Attributes contengono un elenco di coppie: il nome del valore di destinazione e i valori di localizzabilità associati.  Il nome di destinazione può essere un nome di proprietà o il nome speciale $Content.  Se si tratta di un nome di proprietà, il valore di destinazione è il valore della proprietà.  Se si tratta di $Content, il valore di destinazione è il contenuto dell'elemento.  
  
 Sono disponibili tre tipi di attributi:  
  
-   **Category**.  Specifica se un valore può essere modificato con uno strumento del localizzatore.  Vedere <xref:System.Windows.LocalizabilityAttribute.Category%2A>.  
  
-   **Readability**.  Specifica se uno strumento del localizzatore è in grado di leggere \(e visualizzare\) un valore.  Vedere <xref:System.Windows.LocalizabilityAttribute.Readability%2A>.  
  
-   **Modifiability**.  Specifica se uno strumento del localizzatore consente la modifica di un valore.  Vedere <xref:System.Windows.LocalizabilityAttribute.Modifiability%2A>.  
  
 Questi attributi possono essere specificati in qualsiasi ordine, delimitandoli con uno spazio.  Nel caso in cui vengano specificati attributi duplicati, l'ultimo sostituirà i precedenti.  Ad esempio, Localization.Attributes \= "Unmodifiable Modifiable" imposta Modifiability su Modifiable poiché questo è l'ultimo valore.  
  
 Gli attribuiti Modifiability e Readability sono di facile comprensione.  L'attributo Category fornisce categorie predefinite che supportano il localizzatore nella traduzione del testo.  Categorie quali Text, Label e Title offrono al localizzatore informazioni sulla modalità di traduzione del testo.  Sono disponibili anche categorie speciali: None, Inherit, Ignore e NeverLocalize.  
  
 Nella tabella riportata di seguito viene illustrato il significato delle categorie speciali.  
  
|Categoria|Significato|  
|---------------|-----------------|  
|Nessuno|Il valore di destinazione non dispone di una categoria definita.|  
|Inherit|Il valore di destinazione eredita la categoria dall'elemento padre.|  
|Ignora|Il valore di destinazione viene ignorato nel processo di localizzazione.  Questa categoria influisce solo sul valore corrente  e non sui nodi figlio.|  
|NeverLocalize|Il valore corrente non può essere localizzato.  Questa categoria viene ereditata dagli elementi figlio di un elemento.|  
  
<a name="Localization_Comments"></a>   
## Commenti di localizzazione  
 Nella sezione Localization.Comments sono contenute le stringhe in formato libero relative al valore di destinazione.  Gli sviluppatori dell'applicazione possono aggiungere informazioni per offrire ai localizzatori suggerimenti sulla modalità di traduzione del testo delle applicazioni.  Il formato dei commenti può essere una qualsiasi stringa racchiusa tra "\(\)".  Utilizzare "\\" per i caratteri di escape.  
  
## Vedere anche  
 [Globalizzazione per WPF](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)   
 [Utilizzare il layout automatico per creare un pulsante](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)   
 [Utilizzare una griglia per il layout automatico](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)   
 [Localizzare un'applicazione](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)