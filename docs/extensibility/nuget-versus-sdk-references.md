---
title: Hinzufügen von Referenzen mithilfe von NuGet im Vergleich zu einer SDK-Erweiterung
ms.date: 08/02/2019
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 372e82f9bb032ac5a81362017d2062ecf0d44e3f
ms.sourcegitcommit: a124076dfd6b4e5aecda4d01984fee7b0c034745
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2019
ms.locfileid: "68795593"
---
# <a name="nuget-versus-sdk-as-a-project-reference"></a>Nuget im Vergleich zum SDK als Projekt Verweis

Dieser Artikel soll Entwicklern helfen, zu entscheiden, ob Sie Ihre Software als nuget-Paket oder als Software Development Kit (SDK) verpacken möchten. Insbesondere werden die Unterschiede zwischen den beiden erläutert, wenn in einem Visual Studio-Projekt auf Sie verwiesen wird.

- [Nuget](/nuget) ist ein Open-Source-Paketverwaltungssystem, das den Prozess der Integration von Bibliotheken in ein Projekt vereinfacht. Für .net (einschließlich .net Core) ist nuget der von Microsoft unterstützte Mechanismus zur Freigabe von Code. Nuget definiert, wie Pakete für .NET erstellt, gehostet und genutzt werden, und stellt die Tools für jede dieser Rollen bereit. In Visual Studio fügen Sie einem Projekt nuget-Pakete hinzu, indem Sie die Benutzeroberfläche des [Paket-Managers](/nuget/consume-packages/install-use-packages-visual-studio) verwenden.

- Ein [SDK](../extensibility/creating-a-software-development-kit.md) ist eine Sammlung von Dateien, die von Visual Studio als einzelnes Verweis Element behandelt werden. Im Dialogfeld Verweis-Manager in Visual Studio werden alle sdgkte aufgelistet, die für das aktuelle Projekt relevant sind, wenn Sie **Verweis hinzufügen**auswählen. Wenn Sie einem Projekt ein SDK hinzufügen, können Sie über IntelliSense, das Toolbox Fenster, die Designer, die Objektkatalog, MSBuild, Bereitstellung, Debuggen und Verpacken auf den gesamten Inhalt dieses SDK zugreifen.

## <a name="which-mechanism-should-i-use"></a>Welche Vorgehensweise sollte ich verwenden?

Die folgende Tabelle bieten einen Vergleich zwischen den verweisenden Funktionen eines SDK und den Funktionen von NuGet.

| Feature | SDK-Unterstützung | SDK-Hinweise | NuGet-Unterstützung | NuGet-Hinweise |
| - | - | - |---------------| - |
| Bei dieser Vorgehensweise wird auf eine Entität verwiesen. Anschließend sind alle Dateien und Funktionen verfügbar. | J | Sie fügen ein SDK im Dialogfeld **Verweis-Manager** hinzu. Alle Dateien und Funktionen sind während des Entwicklungsworkflows verfügbar. | J | |
| MSBuild verwendet automatisch Assemblys und Windows-Metadaten-Dateien ( *.winmd*). | J | Verweise im SDK werden automatisch an den Compiler übergeben. | J | |
| MSBuild verwendet automatisch die H- oder LIB-Dateien. | J | Die *SDKName.props*-Datei teilt Visual Studio mit, wie das Visual C++-Verzeichnis usw. für automatischen *H*- oder *LIB*-Dateiverbrauch eingerichtet wird. | N | |
| MSBuild verwendet automatisch *JS*- oder *CSS*-Dateien. | J | Im **Projektmappen-Explorer** können Sie den JavaScript-SDK-Verweisknoten aufklappen, um einzelne *JS*- oder *CSS*-Dateien anzuzeigen, und anschließend `<source include/>`-Tags generieren, indem Sie diese Dateien zu den Quelldateien ziehen. Das SDK unterstützt F5 und die automatische Paketeinrichtung. | J | |
| MSBuild fügt der **Toolbox** automatisch das Steuerelement hinzu. | J | Die **Toolbox** kann SDKs nutzen und Steuerelemente in den von Ihnen angegebenen Registerkarten anzeigen. | N | |
| Die Vorgehensweise unterstützt das Visual Studio-Installationsprogramm für Erweiterungen (VSIX). | J | VSIX verfügt über ein spezielles Manifest und eine Logik zum Erstellen von SDK-Paketen. | J | Das VSIX-Programm kann in ein anderes Setupprogramm eingebettet werden. |
| Der **Objektkatalog** listet Verweise auf. | Y | Der **Objektkatalog** erhält die Liste der Verweise in SDKs automatisch und listet sie auf. | N | |
| Dateien und Links werden dem Dialogfeld **Verweis-Manager** automatisch hinzugefügt (Hilfelinks usw. werden automatisch aufgefüllt). | J | Das Dialogfeld **Verweis-Manager** listet SDKs zusammen mit Hilfelinks und der Liste von SDK-Abhängigkeiten automatisch auf. | N | NuGet stellt ein eigenes Dialogfeld **NuGet-Pakete verwalten** bereit. |
| Der Mechanismus unterstützt mehrere Architekturen. | J | SDKs können mit mehreren Konfigurationen ausgeliefert werden. MSBuild verwendet die entsprechenden Dateien für jede Projektkonfiguration. | N | |
| Der Mechanismus unterstützt mehrere Konfigurationen. | J | SDKs können mit mehreren Konfigurationen ausgeliefert werden. Abhängig von der Projektarchitektur verwendet MSBuild die entsprechenden Dateien für jede Projektarchitektur. | N | |
| Mit dem Mechanismus kann angegeben werden, dass Dateien „nicht kopiert“ werden sollen. | J | Je nachdem, ob Dateien im Verzeichnis *\redist* oder *\designtime* abgelegt werden, können Sie steuern, welche Dateien in das Paket der Anwendung, die die Dateien nutzt, kopiert werden sollen. | N | Sie deklarieren, welche Dateien im das Paketmanifest kopiert werden sollen. |
| Der Inhalt wird in lokalisierten Dateien angezeigt. | J | Lokalisierte XML-Dokumenten werden automatisch in die SDKs integriert, um die Entwurfszeitumgebung zu verbessern. | N | |
| MSBuild unterstützt den gleichzeitigen Verbrauch mehrerer Versionen eines SDKs. | J | Das SDK unterstützt den gleichzeitigen Verbrauch mehrerer Versionen. | N | Dies ist keine Verweiserstellung. Ihr Projekt darf jeweils nicht mehr als eine Version von NuGet-Dateien enthalten. |
| Der Mechanismus unterstützt die Angabe der anwendbaren Zielframeworks, der Visual Studio-Versionen und der Projekttypen. | J | Das Dialogfeld **Verweis-Manager** und die **Toolbox** zeigen nur die SDKs an, die für ein Projekt gelten, sodass Benutzer die entsprechenden SDKs leichter auswählen können. | Y (partiell) | Pivot ist das Zielframework. Es erfolgt kein Filtern auf der Benutzeroberfläche. Bei der Installation kann ein Fehler zurückgegeben werden. |
| Der Mechanismus unterstützt das Festlegen von Registrierungsinformationen für systemeigene WinMDs. | J | Sie können die Korrelation zwischen der WINMD-Datei und der DLL-Datei in *SDKManifest.xml* angeben. | N | |
| Der Mechanismus unterstützt das Festlegen von Abhängigkeiten von anderen SDKs. | J | Das SDK benachrichtigt den Benutzer nur. Der Benutzer muss die Installation und die Verweiserstellung nach wie vor manuell vornehmen. | J | NuGet überträgt die Daten automatisch. Der Benutzer wird nicht benachrichtigt. |
| Der Mechanismus ist in [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]-Konzepten wie Anwendungsmanifest und Framework ID integriert. | J | Das SDK muss Konzepte übergeben, die für [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] spezifisch sind, damit das Verpacken und die F5-Funktion mit SDKs, die im [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] verfügbar sind, ordnungsgemäß funktionieren. | N | |
| Der Mechanismus kann in die Pipeline zum App-Debugging für [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]-Apps integriert werden. | J | Das SDK muss an [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)]-spezifische Konzepte übergeben werden, damit das Verpacken und die F5-Funktion mit den im [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] verfügbaren SDKs ordnungsgemäß funktionieren. | J | NuGet-Inhalt wird Teil des Projekts. F5 muss nicht speziell berücksichtigt werden. |
| Der Mechanismus wird in Anwendungsmanifeste integriert. | J | Das SDK muss an [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)]-spezifische Konzepte übergeben werden, damit das Verpacken und die F5-Funktion mit den im [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)] verfügbaren SDKs ordnungsgemäß funktionieren. | J | NuGet-Inhalt wird Teil des Projekts. F5 muss nicht speziell berücksichtigt werden. |
| Der Mechanismus stellt Dateien ohne Verweis bereit (stellen Sie z. B. ein Testframework zum Ausführen von Tests von [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]-Apps bereit). | J | Wenn Sie die Dateien im Ordner *\redist* ablegen, werden die Dateien automatisch bereitgestellt. | J | |
| Der Mechanismus fügt die Plattform-SDKs automatisch der Visual Studio-IDE hinzu. | J | Wenn Sie das [!INCLUDE[win8](../debugger/includes/win8_md.md)] SDK oder das Windows Phone SDK in einem bestimmten Speicherort mit einem bestimmten Layout ablegen, wird das SDK automatisch mit allen Visual Studio-Funktionen integriert. | N | |
| Der Mechanismus unterstützt einen fehlerfreien Entwicklercomputer. (Das heißt, es ist keine Installation erforderlich, und das einfache Abrufen der Quellcodeverwaltung funktioniert.) | N | Da Sie auf ein SDK verweisen, müssen Sie die Projektmappe und das SDK getrennt einchecken. Sie können das SDK von den zwei Nichtregistrierungs-Standardspeicherorten einchecken, die MSBuild beim Durchlaufen der SDKs verwendet (Details finden Sie unter [Erstellen eines Software Development Kits](../extensibility/creating-a-software-development-kit.md)). Wenn ein benutzerdefinierter Speicherort der SDKs vorhanden ist, können Sie stattdessen den folgenden Code in der Projektdatei angeben:<br /><br />`<PropertyGroup>`<br />&nbsp;&nbsp;`<SDKReferenceDirectoryRoot>`<br />&nbsp;&nbsp;`C:\MySDKs`<br />&nbsp;&nbsp;`</SDKReferenceDirectoryRoot>`<br />`</PropertyGroup>`<br /><br /> Checken Sie die SDKs dann in diesen Speicherort ein. | J | Wenn Sie die Projektmappe auschecken, erkennt Visual Studio die Dateien sofort und bearbeitet sie entsprechend. |
| Sie können einer großen vorhandenen Community von Paketerstellern beitreten. | N/V | Die Community ist neu. | J | |
| Sie können einer großen vorhandenen Community von Paketverbrauchern beitreten. | N/V | Die Community ist neu. | J | |
| Sie können an einem Ökosystem von Partnern (benutzerdefinierte Galerien, Repositorys usw.) teilhaben. | N/V | Die verfügbaren Repositorys umfassen Visual Studio Marketplace, Microsoft Download Center und [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]. | J | |
| Der Mechanismus wird in Server mit fortlaufenden Integrationsbuilds sowohl für die Paketerstellung als auch den Paketverbrauch integriert. | J | Das SDK muss den eingecheckten Speicherort (SDKReferenceDirectoryRoot-Eigenschaft) in der Befehlszeile an MSBuild übergeben. | J | |
| Der Mechanismus unterstützt stabile und Vorabveröffentlichungspaketversionen. | J | Das SDK unterstützt das Hinzufügen von Verweisen auf mehrere Versionen. | J | |
| Die Mechanismus unterstützt das automatische Update von installierten Paketen. | J | Wenn es als VSIX oder Bestandteil der automatischen Visual Studio-Updates ausgeliefert wird, bietet das SDK automatische Benachrichtigungen. | J | |
| Der Mechanismus enthält eine eigenständige *EXE*-Datei zum Erstellen und Nutzen von Paketen. | J | Das SDK enthält *MSBuild.exe*. | J | |
| Pakete können in die Versionskontrolle eingecheckt werden. | J | Sie können keine Elemente außerhalb des Knotens „Dokumente“ einchecken, d.h., dass die Erweiterungs-SDKs möglicherweise nicht eingecheckt werden. Das Erweiterungs-SDK ist möglicherweise sehr groß. | J | |
| Sie können eine PowerShell-Schnittstelle verwenden, um Pakete zu erstellen und zu nutzen. | J (Verbrauch), N (Erstellung) | Keine Werkzeugausstattung zum Erstellen eines SDK. Durch den Verbrauch wird MSBuild in der Befehlszeile ausgeführt. | J | |
| Sie können ein Symbolpaket für die Debugunterstützung verwenden. | J | Wenn Sie *PDB*-Dateien im SDK ablegen, werden die Dateien automatisch ausgewählt. | J | |
| Der Mechanismus unterstützt automatische Paketmanagerupdates. | N/V | Das SDK wird mit MSBuild überarbeitet. | J | |
| Der Mechanismus unterstützt ein einfaches Manifestformat. | J | *SDKManifest.xml* unterstützt viele Attribute. Normalerweise ist eine kleine Teilmenge erforderlich. | J | |
| Der Mechanismus ist für alle Visual Studio-Editionen verfügbar. | J | Das SDK unterstützt alle Visual Studio-Editionen. | J | NuGet unterstützt alle Visual Studio-Editionen. |

## <a name="see-also"></a>Siehe auch

- [Verwalten von Verweisen in einem Projekt](../ide/managing-references-in-a-project.md)
- [Verwalten von Verweisen in einem Projekt (Visual Studio für Mac)](/visualstudio/mac/managing-references-in-a-project)