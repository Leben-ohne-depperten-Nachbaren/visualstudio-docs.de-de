---
title: Verfügbar machung von Befehlen | Microsoft-Dokumentation
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d30d71290c08019acfdc75313516d8b1b1c4be3a
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186362"
---
# <a name="making-commands-available"></a>Verfügbar machung von Befehlen

Wenn Visual Studio mehrere VSPackages hinzugefügt werden, kann die Benutzeroberfläche (UI) mit Befehlen überfüllt werden. Um dieses Problem zu beheben, können Sie das Paket wie folgt programmieren:

- Program mieren Sie das Paket so, dass es nur geladen wird, wenn es von einem Benutzer benötigt wird.

- Program mieren Sie das Paket so, dass seine Befehle nur angezeigt werden, wenn Sie im Kontext des aktuellen Status der integrierten Entwicklungsumgebung (Integrated Development Environment, IDE) erforderlich sind.

## <a name="delayed-loading"></a>Verzögertes Laden

Die übliche Vorgehensweise zum Aktivieren des verzögerten Ladens besteht darin, das VSPackage so zu entwerfen, dass seine Befehle in der Benutzeroberfläche angezeigt werden. das Paket selbst wird jedoch erst geladen, wenn ein Benutzer auf einen der Befehle klickt. Um dies zu erreichen, erstellen Sie in der vsct-Datei Befehle ohne Befehlsflags.

Das folgende Beispiel zeigt die Definition eines Menübefehls aus einer vsct-Datei. Dies ist der Befehl, der von der Visual Studio-Paket Vorlage generiert wird, wenn die **Menübefehls** Option in der Vorlage ausgewählt wird.

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

Wenn in diesem Beispiel die übergeordnete Gruppe, `MyMenuGroup`, ein untergeordnetes Element eines Menüs der obersten Ebene ist, z. b. **im Menü Extras** , wird der Befehl in diesem Menü angezeigt, das Paket, das den Befehl ausführt, wird jedoch erst geladen, wenn ein Benutzer auf den Befehl klickt. Wenn Sie jedoch den Befehl zum Implementieren der <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>-Schnittstelle programmieren, können Sie das Laden des Pakets aktivieren, wenn das Menü, das den Befehl enthält, zuerst erweitert wird.

Beachten Sie, dass durch das verzögerte Laden auch die Startleistung verbessert werden kann.

## <a name="current-context-and-the-visibility-of-commands"></a>Aktueller Kontext und die Sichtbarkeit von Befehlen

Sie können VSPackage-Befehle so programmieren, dass Sie sichtbar oder ausgeblendet werden, je nach dem aktuellen Zustand der VSPackage-Daten oder den aktuell relevanten Aktionen. Sie können das VSPackage aktivieren, um den Status seiner Befehle festzulegen, in der Regel mithilfe einer Implementierung der <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A>-Methode aus der <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>-Schnittstelle. hierfür muss jedoch das VSPackage geladen werden, bevor der Code ausgeführt werden kann. Stattdessen empfiehlt es sich, die IDE zum Verwalten der Sichtbarkeit der Befehle zu aktivieren, ohne das Paket zu laden. Ordnen Sie zu diesem Zweck in der vsct-Datei Befehle einem oder mehreren speziellen UI-Kontexten zu. Diese UI-Kontexte werden durch eine GUID identifiziert, die als *Befehls Kontext-GUID*bezeichnet wird.

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] überwacht Änderungen, die sich aus Benutzeraktionen ergeben, z. b. das Laden eines Projekts oder das Wechseln von der Bearbeitung zum Aufbau. Wenn Änderungen auftreten, wird die Darstellung der IDE automatisch geändert. In der folgenden Tabelle sind vier wichtige Kontexte der IDE-Änderungen aufgeführt, die von [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] überwacht werden.

| Kontexttyp | Beschreibung |
|-------------------------| - |
| Aktiver Projekttyp | Bei den meisten Projekttypen ist dieser `GUID` Wert mit der GUID des VSPackage identisch, das das Projekt implementiert. [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] Projekte verwenden jedoch den Projekttyp `GUID` als-Wert. |
| Aktives Fenster | In der Regel handelt es sich hierbei um das letzte aktive Dokument Fenster, das den aktuellen UI-Kontext für Tastenbindungen festlegt. Es könnte aber auch ein Tool Fenster mit einer Schlüssel Bindungs Tabelle sein, die dem internen Webbrowser ähnelt. Für Dokument Fenster mit mehreren Registerkarten, wie z. b. den HTML-Editor, verfügt jede Registerkarte über einen anderen Befehls Kontext `GUID`. |
| Aktiver Sprachdienst | Der Sprachdienst, der der Datei zugeordnet ist, die derzeit in einem Text-Editor angezeigt wird. |
| Aktives Tool Fenster | Ein Tool Fenster, das geöffnet ist und den Fokus besitzt. |

Ein fünfter Haupt Kontext Bereich ist der UI-Status der IDE. UI-Kontexte werden wie folgt durch den aktiven Befehls Kontext `GUID`s identifiziert:

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

Diese GUIDs werden je nach dem aktuellen Status der IDE als aktiv oder inaktiv gekennzeichnet. Mehrere UI-Kontexte können gleichzeitig aktiv sein.

### <a name="hide-and-display-commands-based-on-context"></a>Ausblenden und Anzeigen von Befehlen auf der Grundlage des Kontexts

Sie können einen Paket Befehl in der IDE anzeigen oder ausblenden, ohne das Paket selbst zu laden. Zu diesem Zweck definieren Sie den Befehl in der vsct-Datei des Pakets, indem Sie die Befehlsflags `DefaultDisabled`, `DefaultInvisible`und `DynamicVisibility` und dem Abschnitt [visibilityeinschränkungs](../../extensibility/visibilityconstraints-element.md) Elemente ein oder mehrere [visibilityitem](../../extensibility/visibilityitem-element.md) -Elemente hinzufügen. Wenn ein angegebener Befehls Kontext `GUID` aktiviert wird, wird der Befehl angezeigt, ohne das Paket zu laden.

### <a name="custom-context-guids"></a>Benutzerdefinierte Kontext-GUIDs

Wenn noch keine geeignete Befehls Kontext-GUID definiert ist, können Sie eine in Ihrem VSPackage definieren und diese dann so programmieren, dass Sie je nach Bedarf aktiv oder inaktiv ist, um die Sichtbarkeit der Befehle zu steuern. Verwenden Sie den <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>-Dienst für Folgendes:

- Registrieren Sie Kontext-GUIDs (durch Aufrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>-Methode).

- Abrufen des Status eines Kontext `GUID` (durch Aufrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>-Methode).

- Aktivieren und deaktivieren Sie den Kontext `GUID`s (durch Aufrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>-Methode).

    > [!CAUTION]
    > Stellen Sie sicher, dass sich das VSPackage nicht auf den Status einer vorhandenen Kontext-GUID auswirkt, da andere VSPackages von Ihnen abhängig sein können.

## <a name="example"></a>Beispiel

Das folgende Beispiel für einen VSPackage-Befehl veranschaulicht die dynamische Sichtbarkeit eines Befehls, der von Befehls Kontexten verwaltet wird, ohne das VSPackage zu laden.

Der Befehl ist so festgelegt, dass er aktiviert und angezeigt wird, wenn eine Projekt Mappe vorhanden ist Das heißt, wenn eine der folgenden Befehls Kontext-GUIDs aktiv ist:

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

Beachten Sie im Beispiel, dass jedes Befehlsflag ein separates [Befehlsflag](../../extensibility/command-flag-element.md) -Element ist.

```xml
<Button guid="guidDynamicVisibilityCmdSet" id="cmdidMyCommand"
        priority="0x0100" type="Button">
  <Parent guid="guidDynamicVisibilityCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <CommandFlag>DefaultDisabled</CommandFlag>
  <CommandFlag>DefaultInvisible</CommandFlag>
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <CommandName>cmdidMyCommand</CommandName>
    <ButtonText>My Command name</ButtonText>
  </Strings>
</Button>
```

Beachten Sie auch, dass jeder Benutzeroberflächen Kontext wie folgt in einem separaten `VisibilityItem` Element angegeben werden muss.

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_EmptySolution" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                      id="cmdidMyCommand" context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

## <a name="see-also"></a>Siehe auch

- [Hinzufügen eines Befehls zum Projektmappen-Explorer Symbolleiste](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [Hinzufügen von Benutzeroberflächenelementen mit VSPackages](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Befehlsrouting in VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)
- [Dynamisches Hinzufügen von Menüelementen](../../extensibility/dynamically-adding-menu-items.md)
