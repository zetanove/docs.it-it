---
title: "Procedura: Usare eventi in un&#39;applicazione Web Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "eventi [.NET Framework], Web Form"
  - "Web Form (controlli), ed eventi"
  - "gestori eventi [.NET Framework], Web Form"
  - "eventi [.NET Framework], utilizzo"
  - "Web Form, gestione di eventi"
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Procedura: Usare eventi in un&#39;applicazione Web Form
Uno scenario comune nelle applicazioni ASP.NET Web Form consiste nell'inserimento di una pagina web con controlli, quindi ottimizza un'azione specificata, in base a quale controllo viene selezionato dall'utente.  Ad esempio, un controllo <xref:System.Web.UI.WebControls.Button?displayProperty=fullName>, genera un evento quando un utente fa clic sulla pagina web.  Tramite la gestione dell'evento, l'applicazione esegue la logica appropriata all'azione dell'utente.  
  
### Per gestire un evento selezione di un pulsante in una pagina Web  
  
1.  Creare una pagina Web Form ASP.NET \(pagina Web\) contenente un controllo <xref:System.Web.UI.WebControls.Button> con il valore `OnClick` impostato sul nome del metodo che verrà definito nel prossimo passaggio.  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2.  Definire un gestore eventi corrispondente alla firma del delegato <xref:System.Web.UI.WebControls.Button.Click> e con il nome definito per il valore `OnClick`.  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     L'evento <xref:System.Web.UI.WebControls.Button.Click> utilizza la classe <xref:System.EventHandler> per il tipo di delegato e la classe <xref:System.EventArgs> per i dati dell'evento.  La pagina del framework ASP.NET genera automaticamente codice che crea un istanza di <xref:System.EventHandler> e aggiunge un istanza del delegato per l'evento <xref:System.Web.UI.WebControls.Button.Click> della istanza <xref:System.Web.UI.WebControls.Button>.  
  
3.  Nel metodo del gestore definito nel passaggio 2, aggiungere il codice per eseguire le eventuali azioni necessarie quando si verifica l'evento.  
  
## Vedere anche  
 [Eventi](../../../docs/standard/events/index.md)