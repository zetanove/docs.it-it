---
title: "Procedura: creare una raccolta di caratteri privata | Microsoft Docs"
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
  - "tipi di carattere, creazione di raccolte private"
  - "raccolte private di tipi di carattere, creazione"
ms.assetid: 6533d5e5-a8dc-4b76-9fc4-3bf75c8b9212
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: creare una raccolta di caratteri privata
La classe <xref:System.Drawing.Text.PrivateFontCollection> eredita dalla classe di base astratta <xref:System.Drawing.Text.FontCollection>.  È possibile utilizzare un oggetto <xref:System.Drawing.Text.PrivateFontCollection> per conservare un insieme di caratteri specifico per l'applicazione.  Una raccolta di caratteri privata può includere sia caratteri di sistema installati sia caratteri non installati sul computer.  Per aggiungere un file di caratteri a una raccolta di caratteri privata, chiamare il metodo <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile%2A> di un oggetto <xref:System.Drawing.Text.PrivateFontCollection>.  
  
 La proprietà <xref:System.Drawing.Text.FontCollection.Families%2A> di un oggetto <xref:System.Drawing.Text.PrivateFontCollection> include la matrice di oggetti <xref:System.Drawing.FontFamily>.  
  
 Il numero dei gruppi di caratteri in una raccolta di caratteri privata non coincide necessariamente con il numero dei file di caratteri inclusi nella raccolta.  Si supponga ad esempio di aggiungere i file ArialBd.tff, Times.tff e TimesBd.tff a una raccolta.  Nella raccolta ci saranno tre file ma solamente due gruppi, poiché Times.tff e TimesBd.tff appartengono allo stesso gruppo.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono aggiunti i seguenti tre file di caratteri a un oggetto <xref:System.Drawing.Text.PrivateFontCollection>:  
  
-   C:\\*systemroot*\\Fonts\\Arial.tff \(Arial, normale\)  
  
-   C:\\*systemroot*\\Fonts\\CourBI.tff \(Courier New, grassetto corsivo\)  
  
-   C:\\*systemroot*\\Fonts\\TimesBd.tff \(Times New Roman, grassetto\)  
  
 Viene recuperata una matrice di oggetti <xref:System.Drawing.FontFamily> dalla proprietà <xref:System.Drawing.Text.FontCollection.Families%2A> dell'oggetto <xref:System.Drawing.Text.PrivateFontCollection>.  
  
 Per ogni oggetto <xref:System.Drawing.FontFamily> della raccolta, viene chiamato il metodo <xref:System.Drawing.FontFamily.IsStyleAvailable%2A> per determinare se gli stili normale, grassetto, corsivo, grassetto corsivo, sottolineato e barrato siano disponibili.  Gli argomenti passati al metodo <xref:System.Drawing.FontFamily.IsStyleAvailable%2A> sono membri dell'enumerazione <xref:System.Drawing.FontStyle>.  
  
 Se è disponibile una data combinazione stile\/gruppo, viene costruito un oggetto <xref:System.Drawing.Font> utilizzando quel gruppo e quello stile.  Il primo argomento passato al costruttore <xref:System.Drawing.Font.%23ctor%2A> è il nome del gruppo di caratteri. Si noti che in altre variazioni del costruttore <xref:System.Drawing.Font.%23ctor%2A> viene invece passato un oggetto <xref:System.Drawing.FontFamily>.  L'oggetto <xref:System.Drawing.Font> costruito viene passato al metodo <xref:System.Drawing.Graphics.DrawString%2A> della classe <xref:System.Drawing.Graphics> per visualizzare il nome del gruppo insieme al nome dello stile.  
  
 Se si esegue il codice che segue, l'output sarà simile a quello mostrato nell'immagine seguente.  
  
 ![Testo caratteri](../../../../docs/framework/winforms/advanced/media/csfontstext7.png "csfontstext7")  
  
 Arial.tff, aggiunto nell'esempio di codice seguente alla raccolta di caratteri privata, è il file di caratteri per lo stile normale del carattere Arial.  Si noti, tuttavia, che l'output di programma mostra numerosi stili disponibili, oltre a quello normale, per il gruppo di caratteri Arial.  Questo perché in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile simulare gli stili grassetto, corsivo e grassetto corsivo dallo stile normale.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è anche possibile ottenere, a partire dallo stile normale, caratteri barrati e sottolineati.  
  
 Analogamente, in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile simulare lo stile grassetto corsivo sia dallo stile grassetto sia dal corsivo.  Dall'output di programma risulta evidente che lo stile grassetto corsivo è disponibile per il gruppo Times anche se TimesBd.tff \(Times New Roman, grassetto\) è l'unico file Times nella raccolta.  
  
 [!code-csharp[System.Drawing.FontsAndText#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.FontsAndText#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#51)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 <xref:System.Drawing.Text.PrivateFontCollection>   
 [Utilizzo di tipi di carattere e testo](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)