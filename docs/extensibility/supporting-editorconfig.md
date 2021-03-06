---
title: Sprachdienst für die Unterstützung von editorconfig erweitern
ms.date: 11/22/2017
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [extensibility]
- editorconfig, supporting in a language service
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 663a87ba15121896edcb4c049e7adc6b5c38492a
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/28/2019
ms.locfileid: "72983103"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>Unterstützung von editorconfig für Ihren Sprachdienst

Mit [editorconfig](https://editorconfig.org/) -Dateien können Sie allgemeine Text-Editor-Optionen (z. b. Einzugs Größe) auf Projektbasis beschreiben. Weitere Informationen zur Unterstützung von editorconfig-Dateien in Visual Studio finden Sie unter [Erstellen von portablen Editor-Einstellungen mit editorconfig](../ide/create-portable-custom-editor-options.md).

In den meisten Fällen ist bei der Implementierung eines Visual Studio-Sprachdiensts keine zusätzliche Arbeit erforderlich, um universelle EditorConfig-Eigenschaften zu unterstützen. Der Haupteditor ermittelt und liest die .editorconfig-Datei automatisch, wenn Benutzer Dateien öffnen, und er legt den entsprechenden Textpuffer und die Ansichtsoptionen fest. Bei bearbeitbaren Änderungen, z. b. Registerkarten und Leerzeichen, können einige Sprachdienste jedoch eine geeignete kontextabhängige Text Ansichts Option verwenden, anstatt globale Einstellungen zu verwenden. In diesen Fällen muss der Sprachdienst aktualisiert werden, um EditorConfig-Dateien zu unterstützen.

Im folgenden sind die Änderungen aufgeführt, die erforderlich sind, um einen Sprachdienst zur Unterstützung von editorconfig-Dateien zu aktualisieren, indem eine globale _sprachspezifische_ Option durch eine _Kontext_ Option ersetzt wird:

## <a name="indent-style"></a>Einzugsgröße

Sprachspezifische Optionen | Kontextoptionen
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>Einzugsgröße

Sprachspezifische Optionen | Kontextoptionen
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>Tabulatorgröße

Sprachspezifische Optionen | Kontextoptionen
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>Siehe auch

- [Erstellen portabler Editor-Einstellungen mit editorconfig](../ide/create-portable-custom-editor-options.md)
- [Erweitern des Editors und der Sprachdienste](../extensibility/extending-the-editor-and-language-services.md)