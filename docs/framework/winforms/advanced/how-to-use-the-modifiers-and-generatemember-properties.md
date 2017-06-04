---
title: "Procedura: utilizzare modificatori e propriet&#224; GenerateMember | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Designer_GenerateMember"
  - "Designer_Modifiers"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "form di base"
  - "ereditarietà di form"
  - "GenerateMember (proprietà)"
  - "ereditarietà, form"
  - "form ereditati"
  - "form ereditati, Windows Form"
  - "Modifiers (proprietà)"
  - "Windows Form, ereditarietà"
ms.assetid: 3381a5e4-e1a3-44e2-a765-a0b758937b85
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: utilizzare modificatori e propriet&#224; GenerateMember
Con il posizionamento di un componente in un Windows Form vengono messe a disposizione dall'ambiente di progettazione due proprietà: `GenerateMember` e `Modifiers`.  La proprietà `GenerateMember` consente di specificare il momento in cui Progettazione Windows Form dovrà generare una variabile membro per un componente.  La proprietà `Modifiers` rappresenta il modificatore di accesso assegnato a tale variabile membro.  Se il valore della proprietà `GenerateMember` è `false`, il valore della proprietà `Modifiers` non avrà alcun effetto.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per specificare se un componente è un membro del form  
  
1.  In Progettazione Windows Form aprire il form.  
  
2.  Aprire la **Casella degli strumenti** e posizionare tre controlli <xref:System.Windows.Forms.Button> nel form.  
  
3.  Impostare le proprietà `GenerateMember` e `Modifiers` di ciascun controllo <xref:System.Windows.Forms.Button> sui valori indicati nella tabella seguente.  
  
    |Nome del pulsante|Valore di GenerateMember|Valore di Modifiers|  
    |-----------------------|------------------------------|-------------------------|  
    |`button1`|`true`|`private`|  
    |`button2`|`true`|`protected`|  
    |`button3`|`false`|Nessuna modifica|  
  
4.  Compilare la soluzione.  
  
5.  In **Esplora soluzioni** fare clic sul pulsante **Mostra tutti i file**.  
  
6.  Aprire il nodo **Form1**, quindi nell'**Editor di codice** aprire il file **Form1.Designer.vb** o **Form1.Designer.cs**.  Questo file contiene il codice creato da Progettazione Windows Form.  
  
7.  Trovare le dichiarazioni dei tre pulsanti.  Nell'esempio di codice riportato di seguito sono illustrate le differenze specificate dalle proprietà `GenerateMember` e `Modifiers`.  
  
     [!code-csharp[System.Windows.Forms.GenerateMember#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.GenerateMember#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.GenerateMember#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.GenerateMember#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#2)]  
  
> [!NOTE]
>  Per impostazione predefinita, in Progettazione Windows Form viene assegnato il modificatore `private` \(`Friend` in Visual Basic\) ai controlli contenitore come <xref:System.Windows.Forms.Panel>.  Se il controllo di base <xref:System.Windows.Forms.UserControl> o <xref:System.Windows.Forms.Form> include un controllo contenitore, non accetterà nuovi elementi figlio nei controlli e nei form ereditati.  La soluzione è cambiare il modificate del controllo contenitore di base in `protected` o `public`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Button>   
 [Ereditarietà visiva di Windows Form](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)   
 [Procedura dettagliata: dimostrazione dell'ereditarietà visiva](../../../../docs/framework/winforms/advanced/walkthrough-demonstrating-visual-inheritance.md)   
 [Procedura: ereditare Windows Form](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)