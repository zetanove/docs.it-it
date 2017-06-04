---
title: "Hosting di contenuto Win32 in WPF | Microsoft Docs"
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
ms.assetid: 3cc8644a-34f3-4082-9ddc-77623e4df2d8
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Hosting di contenuto Win32 in WPF
## Prerequisiti  
 Vedere [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md).  
  
## Procedura dettagliata di Win32 in Windows Presentation Framework \(HwndHost\)  
 Per riutilizzare il contenuto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] in applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], utilizzare <xref:System.Windows.Interop.HwndHost>, un controllo che dà a HWND l'aspetto di contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Analogamente a <xref:System.Windows.Interop.HwndSource>, <xref:System.Windows.Interop.HwndHost> è facile da utilizzare. È necessario derivare da <xref:System.Windows.Interop.HwndHost> e implementare i metodi `BuildWindowCore` e `DestroyWindowCore`, quindi creare un'istanza della classe <xref:System.Windows.Interop.HwndHost> derivata e inserirla nell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Se la logica [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] è già assemblata come controllo, l'implementazione di `BuildWindowCore` è poco più di una chiamata a `CreateWindow`.  Per creare un controllo LISTBOX di [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] in [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)], ad esempio:  
  
```  
virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {  
    HWND handle = CreateWindowEx(0, L"LISTBOX",   
    L"this is a Win32 listbox",  
    WS_CHILD | WS_VISIBLE | LBS_NOTIFY  
    | WS_VSCROLL | WS_BORDER,  
    0, 0, // x, y  
    30, 70, // height, width  
    (HWND) hwndParent.Handle.ToPointer(), // parent hwnd  
    0, // hmenu  
    0, // hinstance  
    0); // lparam  
  
    return HandleRef(this, IntPtr(handle));  
}  
  
virtual void DestroyWindowCore(HandleRef hwnd) override {  
    // HwndHost will dispose the hwnd for us  
}  
```  
  
 Si supponga, invece, che il codice [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] non sia completamente autonomo.  In questo caso, è possibile creare una finestra di dialogo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] e incorporarne il contenuto in un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] più grande.  Nell'esempio questo scenario viene illustrato in [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] e [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)], benché sia anche possibile utilizzare un altro linguaggio o la riga di comando.  
  
 Iniziare da una semplice finestra di dialogo, compilata in un progetto [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)].  
  
 Successivamente, inserire la finestra di dialogo nell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] più grande:  
  
-   Compilare la [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] come gestita \(`/clr`\)  
  
-   Convertire la finestra di dialogo in un controllo  
  
-   Definire la classe derivata di <xref:System.Windows.Interop.HwndHost> con i metodi `BuildWindowCore` e `DestroyWindowCore`  
  
-   Eseguire l'override del metodo `TranslateAccelerator` per gestire i tasti della finestra di dialogo  
  
-   Eseguire l'override del metodo `TabInto` per supportare la tabulazione  
  
-   Eseguire l'override del metodo `OnMnemonic` per supportare i tasti di scelta  
  
-   Creare un'istanza della sottoclasse <xref:System.Windows.Interop.HwndHost> e inserirla nell'elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] corretto  
  
### Convertire la finestra di dialogo in un controllo  
 È possibile convertire una finestra di dialogo in HWND figlio utilizzando gli stili WS\_CHILD e DS\_CONTROL.  Accedere al file di risorse \(rc\) in cui è definita la finestra di dialogo e individuare l'inizio della definizione della finestra di dialogo:  
  
```  
IDD_DIALOG1 DIALOGEX 0, 0, 303, 121  
STYLE DS_SETFONT | DS_MODALFRAME | DS_FIXEDSYS | WS_POPUP | WS_CAPTION | WS_SYSMENU  
```  
  
 Modificare la seconda riga come segue:  
  
```  
STYLE DS_SETFONT | WS_CHILD | WS_BORDER | DS_CONTROL  
```  
  
 Con questa azione non viene creato un controllo completamente autonomo. È infatti ancora necessario chiamare `IsDialogMessage()` affinché determinati messaggi vengano elaborati in [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], ma la modifica del controllo costituisce un modo semplice per inserire tali controlli in un altro oggetto HWND.  
  
## Sottoclasse HwndHost  
 Importare i seguenti spazi dei nomi:  
  
```  
namespace ManagedCpp  
{  
    using namespace System;  
    using namespace System::Windows;  
    using namespace System::Windows::Interop;  
    using namespace System::Windows::Input;  
    using namespace System::Windows::Media;  
    using namespace System::Runtime::InteropServices;  
```  
  
 Creare quindi una classe derivata di <xref:System.Windows.Interop.HwndHost> ed eseguire l'override dei metodi `BuildWindowCore` e `DestroyWindowCore`:  
  
```  
public ref class MyHwndHost : public HwndHost, IKeyboardInputSink {  
    private:  
        HWND dialog;  
  
    protected:   
        virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {  
            InitializeGlobals();   
            dialog = CreateDialog(hInstance,   
                MAKEINTRESOURCE(IDD_DIALOG1),   
                (HWND) hwndParent.Handle.ToPointer(),  
                (DLGPROC) About);   
            return HandleRef(this, IntPtr(dialog));  
        }  
  
        virtual void DestroyWindowCore(HandleRef hwnd) override {  
            // hwnd will be disposed for us  
        }  
```  
  
 In questo caso, viene utilizzato `CreateDialog` per creare la finestra di dialogo che in realtà è un controllo.  Poiché si tratta di uno dei primi metodi chiamati nella [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)], è inoltre necessario eseguire un'inizializzazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] standard chiamando una funzione che verrà definita in un secondo momento, denominata `InitializeGlobals()`:  
  
```  
bool initialized = false;  
    void InitializeGlobals() {  
        if (initialized) return;  
        initialized = true;  
  
        // TODO: Place code here.  
        MSG msg;  
        HACCEL hAccelTable;  
  
        // Initialize global strings  
        LoadString(hInstance, IDS_APP_TITLE, szTitle, MAX_LOADSTRING);  
        LoadString(hInstance, IDC_TYPICALWIN32DIALOG, szWindowClass, MAX_LOADSTRING);  
        MyRegisterClass(hInstance);  
  
```  
  
### Eseguire l'override del metodo TranslateAccelerator per gestire i tasti della finestra di dialogo  
 Se si eseguisse ora questo esempio, si otterrebbe un controllo finestra di dialogo che viene visualizzato, ma in cui viene ignorata l'elaborazione da tastiera necessaria per ottenere una finestra di dialogo funzionale.  È necessario eseguire l'override dell'implementazione di `TranslateAccelerator` \(proveniente da `IKeyboardInputSink`, un'interfaccia implementata da <xref:System.Windows.Interop.HwndHost>\).  Questo metodo viene chiamato quando l'applicazione riceve WM\_KEYDOWN e WM\_SYSKEYDOWN.  
  
```  
  
#undef TranslateAccelerator  
        virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,   
            ModifierKeys modifiers) override   
        {  
            ::MSG m = ConvertMessage(msg);  
  
            // Win32's IsDialogMessage() will handle most of our tabbing, but doesn't know   
            // what to do when it reaches the last tab stop  
            if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {  
                HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);  
                HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);  
                TraversalRequest^ request = nullptr;  
  
                if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {  
                    // this code should work, but there’s a bug with interop shift-tab in current builds                      
                    request = gcnew TraversalRequest(FocusNavigationDirection::Last);  
                }  
                else if (!GetKeyState(VK_SHIFT) && GetFocus() == lastTabStop) {  
                    request = gcnew TraversalRequest(FocusNavigationDirection::Next);  
                }  
  
                if (request != nullptr)  
                    return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);  
  
            }  
  
            // Only call IsDialogMessage for keys it will do something with.  
            if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {  
                switch (m.wParam) {  
                    case VK_TAB:  
                    case VK_LEFT:  
                    case VK_UP:  
                    case VK_RIGHT:  
                    case VK_DOWN:  
                    case VK_EXECUTE:  
                    case VK_RETURN:  
                    case VK_ESCAPE:  
                    case VK_CANCEL:  
                        IsDialogMessage(dialog, &m);  
                        // IsDialogMessage should be called ProcessDialogMessage --  
                        // it processes messages without ever really telling you  
                        // if it handled a specific message or not  
                        return true;  
                }  
            }  
  
            return false; // not a key we handled  
        }  
```  
  
 Trattandosi di un codice complesso, sono necessarie spiegazione più dettagliate.  Innanzitutto, nel codice vengono utilizzati [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] e macro [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)], è pertanto importante sapere che esiste già una macro denominata `TranslateAccelerator`, definita in winuser.h:  
  
```  
#define TranslateAccelerator  TranslateAcceleratorW  
```  
  
 Assicurarsi quindi di definire un metodo `TranslateAccelerator`, non un metodo `TranslateAcceleratorW`.  
  
 Analogamente, sono presenti entrambe le strutture winuser.h MSG non gestita e `Microsoft::Win32::MSG` gestita.  Per evitare ambiguità tra le due utilizzare l'operatore [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] `::`.  
  
```  
  
virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,   
    ModifierKeys modifiers) override   
{  
    ::MSG m = ConvertMessage(msg);  
```  
  
 Le due strutture MSG hanno gli stessi dati, ma talvolta è più facile utilizzare la definizione non gestita, pertanto in questo esempio è possibile definire la routine di conversione ovvia:  
  
```  
::MSG ConvertMessage(System::Windows::Interop::MSG% msg) {  
    ::MSG m;  
    m.hwnd = (HWND) msg.hwnd.ToPointer();  
    m.lParam = (LPARAM) msg.lParam.ToPointer();  
    m.message = msg.message;  
    m.wParam = (WPARAM) msg.wParam.ToPointer();  
  
    m.time = msg.time;  
  
    POINT pt;  
    pt.x = msg.pt_x;  
    pt.y = msg.pt_y;  
    m.pt = pt;  
  
    return m;  
}  
```  
  
 Per tornare a `TranslateAccelerator`,  il principio di base consiste nel chiamare la funzione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] `IsDialogMessage` per eseguire il maggior numero di operazioni possibile, ma `IsDialogMessage` non ha accesso ad alcun elemento esterno alla finestra di dialogo. Quando un utente si sposta con il tasto TAB nella finestra di dialogo e la tabulazione supera l'ultimo controllo nella finestra di dialogo, è necessario impostare lo stato attivo sulla parte [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] chiamando `IKeyboardInputSite::OnNoMoreStops`.  
  
```  
// Win32's IsDialogMessage() will handle most of the tabbing, but doesn't know   
// what to do when it reaches the last tab stop  
if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {  
    HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);  
    HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);  
    TraversalRequest^ request = nullptr;  
  
    if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {  
        request = gcnew TraversalRequest(FocusNavigationDirection::Last);  
    }  
    else if (!GetKeyState(VK_SHIFT) && GetFocus() ==  lastTabStop) { {  
        request = gcnew TraversalRequest(FocusNavigationDirection::Next);  
    }  
  
    if (request != nullptr)  
        return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);  
}  
```  
  
 Infine, viene chiamato `IsDialogMessage`.  Una delle responsabilità di un metodo `TranslateAccelerator` è quella di comunicare a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] se la sequenza di tasti è gestita o meno.  In caso contrario, è possibile che l'evento di input sia sottoposto a tunneling e che venga propagato al resto dell'applicazione.  In questo caso, si espone una particolarità della gestione dei messaggi della tastiera e della natura dell'architettura di input in [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Purtroppo, `IsDialogMessage` non fornisce informazioni relative al fatto che una determinata sequenza di tasti venga gestita o meno.  Ancor peggio, chiama `DispatchMessage()` su sequenze di tasti che non deve gestire.  È pertanto necessario decodificare `IsDialogMessage` e chiamarlo solo per i tasti che deve gestire:  
  
```  
// Only call IsDialogMessage for keys it will do something with.  
if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {  
    switch (m.wParam) {  
        case VK_TAB:  
        case VK_LEFT:  
        case VK_UP:  
        case VK_RIGHT:  
        case VK_DOWN:  
        case VK_EXECUTE:  
        case VK_RETURN:  
        case VK_ESCAPE:  
        case VK_CANCEL:  
            IsDialogMessage(dialog, &m);  
            // IsDialogMessage should be called ProcessDialogMessage --  
            // it processes messages without ever really telling you  
            // if it handled a specific message or not  
            return true;  
    }  
```  
  
### Eseguire l'override del metodo TabInto per supportare la tabulazione  
 Dopo avere implementato `TranslateAccelerator`, un utente può spostarsi nella finestra di dialogo e passare all'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] più grande tramite il tasto TAB.  Non è tuttavia possibile utilizzare il tasto TAB per tornare nella finestra di dialogo.  Per risolvere questo problema, eseguire l'override di `TabInto`:  
  
```  
  
public:   
    virtual bool TabInto(TraversalRequest^ request) override {  
        if (request->FocusNavigationDirection == FocusNavigationDirection::Last) {  
            HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);  
            SetFocus(lastTabStop);  
        }  
        else {  
            HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);  
            SetFocus(firstTabStop);  
        }  
        return true;  
    }  
  
```  
  
 Il parametro `TraversalRequest` comunica se la tabulazione viene effettuata con TAB o con TAB e MAIUSC.  
  
### Eseguire l'override del metodo OnMnemonic per supportare i tasti di scelta  
 La gestione della tastiera è quasi completa, tranne per quanto riguarda i tasti di scelta.  Se un utente preme ALT\+F, lo stato attivo non passa alla casella di modifica "First Name".  A tale scopo, eseguire l'override del metodo `OnMnemonic`.  
  
```  
virtual bool OnMnemonic(System::Windows::Interop::MSG% msg, ModifierKeys modifiers) override {  
    ::MSG m = ConvertMessage(msg);  
  
    // If it's one of our mnemonics, set focus to the appropriate hwnd  
    if (msg.message == WM_SYSCHAR && GetKeyState(VK_MENU /*alt*/)) {  
        int dialogitem = 9999;  
        switch (m.wParam) {  
            case 's': dialogitem = IDOK; break;  
            case 'c': dialogitem = IDCANCEL; break;  
            case 'f': dialogitem = IDC_EDIT1; break;  
            case 'l': dialogitem = IDC_EDIT2; break;  
            case 'p': dialogitem = IDC_EDIT3; break;  
            case 'a': dialogitem = IDC_EDIT4; break;  
            case 'i': dialogitem = IDC_EDIT5; break;  
            case 't': dialogitem = IDC_EDIT6; break;  
            case 'z': dialogitem = IDC_EDIT7; break;  
        }  
        if (dialogitem != 9999) {  
            HWND hwnd = GetDlgItem(dialog, dialogitem);  
            SetFocus(hwnd);  
            return true;  
        }  
    }  
    return false; // key unhandled  
};  
```  
  
 In questo caso, non viene chiamato `IsDialogMessage`,  poiché si verifica lo stesso problema di prima, ovvero è necessario poter comunicare al codice [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] se la sequenza di tasti viene gestita o meno e non è possibile raggiungere lo scopo con `IsDialogMessage`.  Si verifica inoltre un secondo problema poiché `IsDialogMessage` non elabora il tasto di scelta se l'oggetto HWND con lo stato attivo non è all'interno della finestra di dialogo.  
  
### Creare un'istanza della classe HwndHost derivata  
 Infine, dopo avere impostato il supporto per i tasti e le tabulazioni, è possibile inserire <xref:System.Windows.Interop.HwndHost> nell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] più grande.  Se l'applicazione principale è scritta in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], il modo più semplice per effettuare correttamente l'inserimento consiste nel lasciare un elemento <xref:System.Windows.Controls.Border> vuoto nel punto in cui si intende inserire <xref:System.Windows.Interop.HwndHost>.  Qui viene creato un oggetto <xref:System.Windows.Controls.Border> denominato `insertHwndHostHere`:  
  
```  
<Window x:Class="WPFApplication1.Window1"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    Title="Windows Presentation Framework Application"  
    Loaded="Window1_Loaded"  
    >  
    <StackPanel>  
        <Button Content="WPF button"/>  
        <Border Name="insertHwndHostHere" Height="200" Width="500"/>  
        <Button Content="WPF button"/>  
    </StackPanel>  
</Window>  
```  
  
 A questo punto, non rimane che individuare il punto ideale nella sequenza di codice per creare un'istanza di <xref:System.Windows.Interop.HwndHost> e connetterla a <xref:System.Windows.Controls.Border>.  In questo esempio, l'istanza viene inserita nel costruttore per la classe <xref:System.Windows.Window> derivata:  
  
```  
public partial class Window1 : Window {  
    public Window1() {  
    }  
  
    void Window1_Loaded(object sender, RoutedEventArgs e) {  
        HwndHost host = new ManagedCpp.MyHwndHost();  
        insertHwndHostHere.Child = host;  
    }  
}  
```  
  
 Si ottiene:  
  
 ![Schermata dell'applicazione WPF](../../../../docs/framework/wpf/advanced/media/interoparch09.png "InteropArch09")  
  
## Vedere anche  
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)