---
title: 'Prüfliste: Erstellen eines Legacysprachdiensts | Microsoft-Dokumentation'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17e9936561bd0ebaa3742610b9b481d60e8489fb
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823657"
---
# <a name="checklist-create-a-legacy-language-service"></a>Prüfliste: Erstellen Sie einen Dienst der legacysprache
Die folgende Checkliste werden zusammengefasst, die grundlegenden Schritte müssen zum Erstellen eines Sprachdiensts für die [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] -Kern-Editor. Integrieren Sie Ihren Sprachdienst in [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], müssen Sie eine Debug-ausdrucksauswertung erstellen. Weitere Informationen finden Sie unter [schreiben Sie eine CLR-ausdrucksauswertung](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md) in die [Visual Studio-Debugger-Erweiterbarkeit](../../extensibility/debugger/visual-studio-debugger-extensibility.md).

## <a name="steps-to-create-a-language-service"></a>Schritte zum Erstellen eines Sprachdiensts

1. Implementieren Sie die <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>-Schnittstelle.

    - In einem VSPackage, implementieren die <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> Schnittstelle, um den Sprachdienst bereitzustellen.

    - Verfügbarmachen von Ihren Sprachdienst für die integrierte Entwicklungsumgebung (IDE) in Ihrer <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> Implementierung.

2. Implementieren der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> -Schnittstelle in der Hauptsprache Dienstklasse.

     Die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> Schnittstelle ist der Ausgangspunkt der Interaktion zwischen der Kern-Editor und den Sprachdienst.

### <a name="optional-features"></a>Optionale features
 Die folgenden Funktionen sind optional und können in beliebiger Reihenfolge implementiert werden. Diese Features erhöhen Sie die Funktionalität von den Sprachdienst.

- Farben für Syntax

  Implementieren Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>-Schnittstelle. Die Implementierung dieser Schnittstelle sollten die Parser-Informationen, um die entsprechende Farbe Informationen zurückzugeben.

  Die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> Methode gibt die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> Schnittstelle. Wird für jede Textpuffer, eine separate Farbauswahl-Instanz erstellt, damit Sie implementieren sollten die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> Schnittstelle separat. Weitere Informationen finden Sie unter [Syntaxfarben in einem legacysprachdiensten](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md).

- Codefenster

  Implementieren der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> Schnittstelle, mit der Sprachdienst den Empfang einer Nachricht, wenn ein neues Codefenster erstellt wird.

  Die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> Methode gibt die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> Schnittstelle. Der Sprachdienst können Sie die spezielle Benutzeroberfläche hinzufügen, um das Codefenster im <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A>. Der Sprachdienst ist spezielle Verarbeitung, z. B. das Hinzufügen eines textansichtsfilter in ebenfalls möglich <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A>.

- Textansichtsfilter

  Um IntelliSense-Anweisungsvervollständigung in einem Sprachdienst zu gewährleisten, müssen Sie einige der Befehle abfangen, die andernfalls von die Textansicht behandelt würden. Führen Sie zum Abfangen dieser Befehle die folgenden Schritte aus:

  - Implementieren <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> zur Teilnahme an der Befehl-Kette und Handle-Editor-Befehl.

  - Rufen Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> Methode und übergeben Ihr <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> Implementierung.

  - Rufen Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A> Methode, wenn Sie aus der Ansicht trennen, so dass diese Befehle nicht mehr an Sie übergeben werden.

  Befehle, die verarbeitet werden müssen, hängen von der Dienste, die bereitgestellt werden. Weitere Informationen finden Sie unter [wichtige Befehle für Language service Filter](../../extensibility/internals/important-commands-for-language-service-filters.md).

  > [!NOTE]
  > Die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> -Schnittstelle muss implementiert werden, auf das gleiche Objekt wie die <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> Schnittstelle.

- Anweisungsvervollständigung

  Implementieren Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>-Schnittstelle.

  Die Anweisung abgeschlossen-Befehl unterstützt (, also <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>), und rufen Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> -Methode in der die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> -Schnittstelle, übergeben die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> Schnittstelle. Weitere Informationen finden Sie unter [Anweisungsvervollständigung in einem älteren Sprachdienst](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md).

- Methodentipps

  Implementieren der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> Schnittstelle, um Daten für das methodentippfenster bereitzustellen.

  Installieren Sie die Filter für die Text-Ansicht, um Befehle entsprechend zu behandeln, damit Sie wissen, wann ein methodentippfenster für die Daten angezeigt werden. Weitere Informationen finden Sie unter [ParameterInfo in einer legacysprachdiensten](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md).

- Fehlermarker

  Implementieren Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>-Schnittstelle.

  Die beim Erstellen der Marker-Objekte, implementieren die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> -Schnittstelle, und rufen die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> -Methode und übergeben die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> Schnittstelle das Marker-Fehlerobjekt.

  In der Regel verwaltet jeder fehlermarker ein Element in das Aufgabenlistenfenster an.

- Aufgabenlistenelementen

  Implementieren einer Klasse bereitstellen Task Element der <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem> Schnittstelle.

  Implementieren einer Aufgabe Anbieter Klasse Bereitstellen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider> Schnittstelle und die <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> Schnittstelle.

  Implementieren einer Aufgabe Enumerator Klasse Bereitstellen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems> Schnittstelle.

  Registrieren Sie den Aufgabenanbieter bei der Aufgabenliste <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A> Methode.

  Abrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> Schnittstelle durch Aufrufen der Sprachdienst-Dienstanbieter mit dem Dienst-GUID <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>.

  Erstellen von Aufgabenobjekten-Element, und rufen die <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A> -Methode in der die <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> -Schnittstelle auf, wenn es neue gibt oder aktualisiert Aufgaben.

- Kommentar-Aufgaben

  Verwenden der <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> Schnittstelle und die <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> Schnittstelle, um den Kommentar Task-Token zu beziehen.

  Abrufen einer <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> -Schnittstelle aus der <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> Service.

  Abrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> -Schnittstelle aus der <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A> Methode.

  Implementieren der <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents> Schnittstelle zum Lauschen auf Änderungen in der Liste mit token.

- Gliedern

  Es gibt mehrere Optionen für die Unterstützung der Gliederung. Sie können z. B. unterstützen die **reduzieren auf Definitionen** Befehl, editorgesteuert Gliederungsbereiche bereitzustellen oder Client gesteuerter Regionen unterstützen. Weitere Informationen finden Sie unter [Vorgehensweise: Geben Sie die Unterstützung für erweiterten Gliederungen in einem älteren Sprachdienst](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md).

- Language-Service-Registrierung

  Weitere Informationen dazu, wie Sie einen Sprachdienst zu registrieren, finden Sie unter [Registrieren von Diensten legacysprache](../../extensibility/internals/registering-a-legacy-language-service2.md) und [verwalten VSPackages](../../extensibility/managing-vspackages.md).

- Kontextbezogene Hilfe

  Bereitstellen von Kontext für den Editor in einem der folgenden Methoden:

  - Bereitstellen von Kontext für Textmarker durch die Implementierung der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> Schnittstelle.

  - Geben Sie alle Benutzerkontext durch die Implementierung der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> Schnittstelle.

## <a name="see-also"></a>Siehe auch
- [Entwickeln eines Datendiensts legacysprache](../../extensibility/internals/developing-a-legacy-language-service.md)
- [Schreiben Sie eine CLR-ausdrucksauswertung](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
