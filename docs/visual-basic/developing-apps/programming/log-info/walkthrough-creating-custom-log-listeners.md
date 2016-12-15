---
title: "Walkthrough: Creating Custom Log Listeners (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "custom log listeners"
  - "My.Application.Log object, custom log listeners"
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Creating Custom Log Listeners (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questa procedura dettagliata viene illustrato come creare un listener di log personalizzato e configurarlo per l'ascolto dell'output dell'oggetto `My.Application.Log`.  
  
## Introduzione  
 I listener di log devono ereditare dalla classe <xref:System.Diagnostics.TraceListener>.  
  
#### Per creare il listener  
  
-   Nell'applicazione creare una classe denominata `SimpleListener` che erediti da <xref:System.Diagnostics.TraceListener>.  
  
     [!code-vb[VbVbalrMyApplicationLog#16](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-creating-custom-log-listeners_1.vb)]  
  
     I metodi <xref:System.Diagnostics.TraceListener.Write%2A> e <xref:System.Diagnostics.TraceListener.WriteLine%2A>, richiesti dalla classe di base, richiamano `MsgBox` per visualizzare l'input.  
  
     L'attributo <xref:System.Security.Permissions.HostProtectionAttribute> viene applicato ai metodi <xref:System.Diagnostics.TraceListener.Write%2A> e <xref:System.Diagnostics.TraceListener.WriteLine%2A> in modo che i relativi attributi corrispondano ai metodi della classe di base.  L'attributo <xref:System.Security.Permissions.HostProtectionAttribute> consente all'host su cui è in esecuzione il codice di determinare se il codice esegue la sincronizzazione di protezione host.  
  
    > [!NOTE]
    >  L'attributo <xref:System.Security.Permissions.HostProtectionAttribute> è efficace solo in applicazioni non gestite sui cui è in esecuzione Common Language Runtime e che implementano la protezione host, quale SQL Server.  
  
 Per assicurarsi che in `My.Application.Log` venga utilizzato il listener di log creato, assegnare un nome sicuro all'assembly che contiene il listener di log.  
  
 Nella prossima procedura vengono illustrati alcuni semplici passaggi per la creazione di un assembly del listener di log con un nome sicuro.  Per ulteriori informazioni, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md).  
  
#### Per assegnare un nome sicuro all'assembly del listener di log  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Firma**.  
  
3.  Selezionare la casella **Firma assembly**.  
  
4.  Selezionare **\<Nuova...\>** dall'elenco a discesa **Scegli un file chiave con nome sicuro**.  
  
     Verrà visualizzata la finestra di dialogo **Crea chiave con nome sicuro**.  
  
5.  Fornire un nome al file della chiave nella casella **Nome file di chiave**.  
  
6.  Immettere una password nelle caselle **Enter password** e **Conferma password**.  
  
7.  Scegliere **OK**.  
  
8.  Ricompilare l'applicazione.  
  
## Aggiunta del listener  
 Una volta assegnato un nome sicuro all'assembly, è necessario determinare il nome sicuro del listener in modo che in `My.Application.Log` venga applicato il listener di log creato.  
  
 Il formato di un tipo di nome sicuro è il seguente.  
  
 \<nome tipo\>, \<nome assembly\>, \<numero versione\>, \<impostazioni cultura\>, \<nome sicuro\>  
  
#### Per determinare il nome sicuro del listener  
  
-   Nel codice mostrato di seguito viene illustrato come determinare il tipo di nome sicuro per `SimpleListener`.  
  
     [!code-vb[VbVbalrMyApplicationLog#17](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/walkthrough-creating-custom-log-listeners_2.vb)]  
  
     Il nome sicuro per un tipo dipende dal progetto.  
  
 Con un nome sicuro, è possibile aggiungere il listener alla raccolta del listener di log `My.Application.Log`.  
  
#### Per aggiungere il listener a My.Application.Log  
  
1.  Fare clic su app.config con il pulsante destro del mouse in **Esplora soluzioni**, quindi scegliere **Apri**.  
  
     In alternativa  
  
     Se è presente un file app.config:  
  
    1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    2.  Nella finestra di dialogo **Aggiungi nuovo elemento**, selezionare **File di configurazione dell'applicazione**.  
  
    3.  Scegliere **Aggiungi**.  
  
2.  Individuare la sezione `<listeners>`, nella sezione `<source>` con l'attributo "DefaultSource" `name`, che si trova nella sezione `<sources>`.  La sezione `<sources>` si trova all'interno della sezione `<system.diagnostics>`, nella sezione di livello superiore `<configuration>`.  
  
3.  Aggiungere questo elemento alla sezione `<listeners>`:  
  
    ```  
    <add name="SimpleLog" />  
    ```  
  
4.  Individuare la sezione `<sharedListeners>`, contenuta nella sezione `<system.diagnostics>`, a sua volta contenuta nella sezione `<configuration>` di primo livello.  
  
5.  Aggiungere l'elemento alla sezione `<sharedListeners>`:  
  
    ```  
    <add name="SimpleLog" type="SimpleLogStrongName" />  
    ```  
  
     Modificare il valore di `SimpleLogStrongName` in modo che sia il nome sicuro del listener.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [How to: Log Exceptions](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [Procedura: scrivere messaggi di log](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [Procedura dettagliata: modifica della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)