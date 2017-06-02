---
title: "Procedura: leggere i metadati delle immagini | Microsoft Docs"
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
  - "metadati, elemento della proprietà"
  - "metadati, lettura dell'immagine"
ms.assetid: 72ec0b31-0be7-444a-9575-1dbcb864e0be
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: leggere i metadati delle immagini
Alcuni file di immagine contengono metadati leggibili per determinare le caratteristiche di un'immagine.  Una fotografia digitale, ad esempio, potrebbe contenere metadati leggibili per determinare produttore e modello della fotocamera utilizzata per scattare la fotografia.  Con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile leggere metadati esistenti e, inoltre, scrivere nuovi metadati in file di immagine.  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] consente di memorizzare un singolo metadato in un oggetto <xref:System.Drawing.Imaging.PropertyItem>.  È possibile leggere la proprietà <xref:System.Drawing.Image.PropertyItems%2A> di un oggetto <xref:System.Drawing.Image> per recuperare tutti i metadati da un file.  La proprietà <xref:System.Drawing.Image.PropertyItems%2A> restituisce una matrice di oggetti <xref:System.Drawing.Imaging.PropertyItem>.  
  
 Un oggetto <xref:System.Drawing.Imaging.PropertyItem> dispone delle seguenti quattro proprietà: `Id`, `Value`, `Len` e `Type`.  
  
## Id  
 Tag che identifica l'elemento dei metadati.  Nella tabella seguente sono indicati alcuni valori che è possibile assegnare a <xref:System.Drawing.Imaging.PropertyItem.Id%2A>.  
  
|Valore esadecimale|Descrizione|  
|------------------------|-----------------|  
|0x0320<br /><br /> 0x010F<br /><br /> 0x0110<br /><br /> 0x9003<br /><br /> 0x829A<br /><br /> 0x5090<br /><br /> 0x5091|Titolo dell'immagine<br /><br /> Produttore dell'apparecchio<br /><br /> Modello dell'apparecchio<br /><br /> ExifDTOriginal<br /><br /> Tempo di esposizione del file exif<br /><br /> Tabella di luminanza<br /><br /> Tabella di saturazione|  
  
## Valore  
 Matrice di valori.  Il formato dei valori è determinato dalla proprietà <xref:System.Drawing.Imaging.PropertyItem.Type%2A>.  
  
## Len  
 La lunghezza espressa in byte della matrice di valori cui fa riferimento la proprietà <xref:System.Drawing.Imaging.PropertyItem.Value%2A>.  
  
## Type  
 Il tipo di dati dei valori nella matrice a cui fa riferimento la proprietà `Value`.  I formati indicati dai valori della proprietà `Type` sono elencati nella tabella seguente.  
  
|Valore numerico|Descrizione|  
|---------------------|-----------------|  
|1|Oggetto `Byte`|  
|2|Una matrice di oggetti `Byte` codificati in ASCII|  
|3|Un Integer a 16 bit|  
|4|Un Integer a 32 bit|  
|5|Una matrice di due oggetti `Byte` che rappresenta un numero razionale|  
|6|Non utilizzato|  
|7|Non definito|  
|8|Non utilizzato|  
|9|`SLong`|  
|10|`SRational`|  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito vengono letti e visualizzati i sette metadati del file `FakePhoto.jpg`.  Il secondo elemento della proprietà \(indice 1\) dell'elenco contiene <xref:System.Drawing.Imaging.PropertyItem.Id%2A> 0x010F \(produttore dell'attrezzatura\) e <xref:System.Drawing.Imaging.PropertyItem.Type%2A> 2 \(matrice di byte codificata ASCII\).  Nel codice di esempio viene mostrato il valore di tale elemento della proprietà.  
  
 L'output prodotto dal codice è simile al seguente:  
  
 `Property Item 0`  
  
 `id: 0x320`  
  
 `type: 2`  
  
 `length: 16 bytes`  
  
 `Property Item 1`  
  
 `id: 0x10f`  
  
 `type: 2`  
  
 `length: 17 bytes`  
  
 `Property Item 2`  
  
 `id: 0x110`  
  
 `type: 2`  
  
 `length: 7 bytes`  
  
 `Property Item 3`  
  
 `id: 0x9003`  
  
 `type: 2`  
  
 `length: 20 bytes`  
  
 `Property Item 4`  
  
 `id: 0x829a`  
  
 `type: 5`  
  
 `length: 8 bytes`  
  
 `Property Item 5`  
  
 `id: 0x5090`  
  
 `type: 3`  
  
 `length: 128 bytes`  
  
 `Property Item 6`  
  
 `id: 0x5091`  
  
 `type: 3`  
  
 `length: 128 bytes`  
  
 `The equipment make is Northwind Camera.`  
  
### Codice  
 [!code-csharp[System.Drawing.WorkingWithImages#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.WorkingWithImages#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#51)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Gestire l'evento <xref:System.Windows.Forms.Control.Paint> del form e incollare il codice nel gestore dell'evento Paint.  È necessario sostituire `FakePhoto.jpg` con il nome e il percorso di un'immagine validi nel sistema in uso e importare lo spazio dei nomi `System.Drawing.Imaging`.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)