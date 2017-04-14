---
title: "Procedura dettagliata: hosting di un oggetto Clock WPF in Win32 | Microsoft Docs"
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
  - "interoperabilità [WPF], esercitazioni"
  - "interoperabilità [WPF], Win32"
  - "codice Win32, interoperabilità WPF"
ms.assetid: 555e55a7-0851-4ec8-b1c6-0acba7e9b648
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura dettagliata: hosting di un oggetto Clock WPF in Win32
Per inserire [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in applicazioni [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], utilizzare <xref:System.Windows.Interop.HwndSource> che fornisce HWND con il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Innanzitutto, viene creato <xref:System.Windows.Interop.HwndSource> a cui si assegnano parametri simili a CreateWindow.  Quindi, viene comunicato a <xref:System.Windows.Interop.HwndSource> quale contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] si desidera inserire.  Infine, viene estratto HWND da <xref:System.Windows.Interop.HwndSource>.  In questa procedura dettagliata viene illustrato come creare [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] misto nell'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] che implementa nuovamente la finestra di dialogo **Proprietà data e ora** del sistema operativo.  
  
## Prerequisiti  
 Vedere [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md).  
  
## Istruzioni per l'utilizzo di questa esercitazione  
 In questa esercitazione vengono illustrati i passaggi più importanti nella produzione di un'applicazione di interoperatività.  L'esercitazione è supportata da un esempio, [Esempio di interoperatività con l'orologio Win32](http://go.microsoft.com/fwlink/?LinkID=160051) che riflette il prodotto finale.  In questa esercitazione vengono documentati i passaggi necessari a partire da un progetto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] esistente, magari preesistente, e con l'aggiunta di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato nell'applicazione.  È possibile confrontare il prodotto finale con [Esempio di interoperatività con l'orologio Win32](http://go.microsoft.com/fwlink/?LinkID=160051) \(la pagina potrebbe essere in inglese\).  
  
## Procedura dettagliata di Windows Presentation Framework in Win32 \(HwndSource\)  
 Nelle figure seguenti viene illustrato il prodotto finale di questa esercitazione:  
  
 ![Finestra di dialogo Proprietà data e ora](../../../../docs/framework/wpf/advanced/media/interoparch06.png "InteropArch06")  
  
 È possibile ricreare questa finestra di dialogo creando un progetto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] C\+\+ in [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] e utilizzando l'editor della finestra di dialogo per creare quanto segue:  
  
 ![Finestra di dialogo Proprietà data e ora](../../../../docs/framework/wpf/advanced/media/interoparch07.png "InteropArch07")  
  
 Non è necessario [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] per utilizzare <xref:System.Windows.Interop.HwndSource>, né occorre utilizzare C\+\+ per scrivere programmi [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], benché si tratti di un modo di procedere tipico adatto alla spiegazione di un'esercitazione.  
  
 È necessario eseguire cinque sottopassaggi particolari per inserire un orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nella finestra di dialogo:  
  
1.  Consentire la chiamata di codice gestito \(**\/clr**\) dal progetto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] modificando le impostazioni del progetto in [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)].  
  
2.  Creare <xref:System.Windows.Controls.Page> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una DLL separata.  
  
3.  Inserire <xref:System.Windows.Controls.Page> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in <xref:System.Windows.Interop.HwndSource>.  
  
4.  Ottenere HWND per <xref:System.Windows.Controls.Page> utilizzando la proprietà <xref:System.Windows.Interop.HwndSource.Handle%2A>.  
  
5.  Utilizzare [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] per decidere dove posizionare HWND all'interno dell'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] più grande.  
  
## \/clr  
 Il primo passaggio consiste nel trasformare il progetto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] non gestito in un progetto in grado di chiamare codice gestito.  Viene utilizzata l'opzione del compilatore \/clr per stabilire il collegamento alle DLL necessarie da utilizzare e viene impostato il metodo Main per l'utilizzo con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Per consentire l'utilizzo di codice gestito nel progetto C\+\+, fare clic con il pulsante destro del mouse sul progetto win32clock e selezionare **Proprietà**.  Nella pagina delle proprietà **Generale** \(impostazione predefinita\), impostare il supporto Common Language Runtime su `/clr`.  
  
 In seguito, aggiungere riferimenti alle DLL necessarie per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]: PresentationCore.dll, PresentationFramework.dll, System.dll, WindowsBase.dll, UIAutomationProvider.dll e UIAutomationTypes.dll.  Nelle istruzioni riportate di seguito si suppone che il sistema operativo sia installato nell'unità C:.  
  
1.  Fare clic con il pulsante destro del mouse sul progetto win32clock e scegliere **Riferimenti...**, quindi nella finestra di dialogo:  
  
2.  Fare clic con il pulsante destro del mouse sul progetto win32clock e scegliere **Riferimenti...**.  
  
3.  Scegliere **Aggiungi nuovo riferimento**, fare clic sulla scheda Sfoglia, immettere C:\\Programmi\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\PresentationCore.dll e scegliere OK.  
  
4.  Ripetere il passaggio per PresentationFramework.dll: C:\\Programmi\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\PresentationFramework.dll.  
  
5.  Ripetere il passaggio per WindowsBase.dll: C:\\Programmi\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\WindowsBase.dll.  
  
6.  Ripetere il passaggio per UIAutomationTypes.dll: C:\\Programmi\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\UIAutomationTypes.dll.  
  
7.  Ripetere il passaggio per UIAutomationProvider.dll: C:\\Programmi\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\UIAutomationProvider.dll.  
  
8.  Scegliere **Aggiungi nuovo riferimento**, selezionare System.dll e fare clic su **OK**.  
  
9. Fare clic su **OK** per uscire dalle pagine delle proprietà di win32clock per l'aggiunta di riferimenti.  
  
 Infine, aggiungere `STAThreadAttribute` al metodo `_tWinMain` per l'utilizzo con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
```  
[System::STAThreadAttribute]  
int APIENTRY _tWinMain(HINSTANCE hInstance,  
                     HINSTANCE hPrevInstance,  
                     LPTSTR    lpCmdLine,  
                     int       nCmdShow)  
```  
  
 Con questo attributo si comunica a [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] che, durante l'inizializzazione di [!INCLUDE[TLA#tla_com](../../../../includes/tlasharptla-com-md.md)], è necessario utilizzare un modello di apartment a thread singolo \(STA\), richiesto per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
## Creare una pagina di Windows Presentation Framework  
 Successivamente, viene creata una DLL che definisce <xref:System.Windows.Controls.Page> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  È spesso più facile creare <xref:System.Windows.Controls.Page> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] come applicazione autonoma, quindi scrivere ed eseguire il debug della parte [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nel modo indicato.  Dopo questa operazione, è possibile convertire il progetto in una DLL facendo clic con il pulsante destro del mouse sul progetto stesso, scegliendo **Proprietà**, Applicazione, quindi impostando Tipo di output su Libreria di classi Windows.  
  
 Il progetto di DLL [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] può quindi essere combinato con il progetto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] \(una soluzione che contiene due progetti\). Fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Aggiungi progetto esistente**.  
  
 Per utilizzare la DLL [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dal progetto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], è necessario aggiungere un riferimento.  
  
1.  Fare clic con il pulsante destro del mouse sul progetto win32clock e scegliere **Riferimenti...**.  
  
2.  Scegliere **Aggiungi nuovo riferimento**.  
  
3.  Fare clic sulla scheda **Progetti**.  Selezionare WPFClock e fare clic su OK.  
  
4.  Fare clic su **OK** per uscire dalle pagine delle proprietà di win32clock per l'aggiunta di riferimenti.  
  
## HwndSource  
 Quindi, utilizzare <xref:System.Windows.Interop.HwndSource> in modo che <xref:System.Windows.Controls.Page> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] abbia l'aspetto di HWND.  Il seguente blocco di codice viene aggiunto a un file C\+\+:  
  
```  
namespace ManagedCode  
{  
    using namespace System;  
    using namespace System::Windows;  
    using namespace System::Windows::Interop;  
    using namespace System::Windows::Media;  
  
    HWND GetHwnd(HWND parent, int x, int y, int width, int height) {  
        HwndSource^ source = gcnew HwndSource(  
            0, // class style  
            WS_VISIBLE | WS_CHILD, // style  
            0, // exstyle  
            x, y, width, height,  
            "hi", // NAME  
            IntPtr(parent)        // parent window   
            );  
  
        UIElement^ page = gcnew WPFClock::Clock();  
        source->RootVisual = page;  
        return (HWND) source->Handle.ToPointer();  
    }  
}  
}  
```  
  
 Trattandosi di codice complesso, sono necessarie spiegazioni più dettagliate.  Nella prima parte sono presenti varie clausole per evitare di indicare il nome completo di tutte le chiamate:  
  
```  
namespace ManagedCode  
{  
    using namespace System;  
    using namespace System::Windows;  
    using namespace System::Windows::Interop;  
    using namespace System::Windows::Media;  
```  
  
 Viene quindi definita una funzione per creare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], attorno al quale viene inserito <xref:System.Windows.Interop.HwndSource> e viene restituito HWND:  
  
```  
HWND GetHwnd(HWND parent, int x, int y, int width, int height) {  
```  
  
 Innanzitutto, viene creato <xref:System.Windows.Interop.HwndSource>, con parametri simili a CreateWindow.  
  
```  
HwndSource^ source = gcnew HwndSource(  
    0, // class style  
    WS_VISIBLE | WS_CHILD, // style  
    0, // exstyle  
    x, y, width, height,  
    "hi", // NAME  
    IntPtr(parent) // parent window   
    );  
```  
  
 Viene quindi creata la classe contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mediante la chiamata al relativo costruttore:  
  
```  
UIElement^ page = gcnew WPFClock::Clock();  
```  
  
 La pagina viene quindi connessa a <xref:System.Windows.Interop.HwndSource>:  
  
```  
source->RootVisual = page;  
```  
  
 Nella riga finale, viene restituito HWND per <xref:System.Windows.Interop.HwndSource>:  
  
```  
return (HWND) source->Handle.ToPointer();  
```  
  
## Posizionamento di HWND  
 A questo punto si dispone di HWND contenente l'orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ed è necessario inserirlo nella finestra di dialogo di [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Se si conosce la posizione in cui inserire HWND, è sufficiente passare tali dimensione e posizione alla funzione `GetHwnd` definita in precedenza.  In questo caso, tuttavia, si è utilizzato un file di risorse per definire la finestra di dialogo, pertanto non si conosce esattamente la posizione degli oggetti HWND.  È possibile utilizzare l'editor finestre di [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] per inserire un controllo STATIC [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] nel punto in cui si desidera posizionare l'orologio \("Insert clock here"\) e utilizzare tale controllo per posizionare l'orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Nella gestione di WM\_INITDIALOG, viene utilizzato `GetDlgItem` per recuperare HWND per il segnaposto STATIC:  
  
```  
HWND placeholder = GetDlgItem(hDlg, IDC_CLOCK);  
```  
  
 Vengono quindi calcolate la dimensione e la posizione del segnaposto STATIC, per consentire l'inserimento dell'orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in tale punto:  
  
 Rettangolo RECT;  
  
```  
GetWindowRect(placeholder, &rectangle);  
int width = rectangle.right - rectangle.left;  
int height = rectangle.bottom - rectangle.top;  
POINT point;  
point.x = rectangle.left;  
point.y = rectangle.top;  
result = MapWindowPoints(NULL, hDlg, &point, 1);  
```  
  
 Viene quindi nascosto il segnaposto STATIC:  
  
```  
ShowWindow(placeholder, SW_HIDE);  
```  
  
 Viene creato l'oggetto HWND orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in tale posizione:  
  
```  
HWND clock = ManagedCode::GetHwnd(hDlg, point.x, point.y, width, height);  
```  
  
 Per rendere interessante l'esercitazione e realizzare un vero orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario creare un controllo orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a questo punto.  È possibile procedere in questo modo nel markup, con pochi gestori eventi in code\-behind.  Poiché questa esercitazione fa riferimento all'interoperatività e non alla progettazione dei controlli, il codice completo per l'orologio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene fornito come blocco di codice, senza istruzioni specifiche per la compilazione, né spiegazioni sulle singole parti.  È possibile modificare questo codice per dare al controllo aspetto e funzionalità differenti.  
  
 Il markup è il seguente:  
  
 [!code-xml[Win32Clock#AllClockXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml#allclockxaml)]  
  
 Il code\-behind correlato è il seguente:  
  
 [!code-csharp[Win32Clock#AllClockCS](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml.cs#allclockcs)]  
  
 Il risultato finale sarà analogo al seguente:  
  
 ![Finestra di dialogo Proprietà data e ora](../../../../docs/framework/wpf/advanced/media/interoparch08.png "InteropArch08")  
  
 Per confrontare il risultato finale al codice con cui è stata prodotta la schermata qui riportata, vedere [Esempio di interoperatività con l'orologio Win32](http://go.microsoft.com/fwlink/?LinkID=160051).  
  
## Vedere anche  
 <xref:System.Windows.Interop.HwndSource>   
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [Esempio di interoperatività con l'orologio Win32](http://go.microsoft.com/fwlink/?LinkID=160051)