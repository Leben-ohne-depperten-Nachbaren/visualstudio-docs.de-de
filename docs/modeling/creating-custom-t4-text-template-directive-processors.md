---
title: Erstellen von benutzerdefinierten T4-Direktivenprozessoren für Textvorlagen
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c70aa1853701ef671b7057ad698a0fb63334a1ca
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597177"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>Erstellen von benutzerdefinierten T4-Anweisungsprozessoren für Textvorlagen

Der *Textvorlagen-Transformationsprozess* übernimmt eine *Textvorlagen* Datei als Eingabe und erzeugt eine Textdatei als Ausgabe. Die *Textvorlagen-Transformations-Engine* steuert den Prozess, und die Engine interagiert mit einem Textvorlagen-Transformations Host und mindestens einem Text Template- *Direktivenprozessor* , um den Vorgang abzuschließen. Weitere Informationen finden Sie [unter Text Template Transformation Process](../modeling/the-text-template-transformation-process.md).

Zum Erstellen eines benutzerdefinierten Anweisungsprozessors erstellen Sie eine Klasse, die von <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> oder <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> erbt.

Der Unterschied zwischen diesen beiden besteht darin, dass <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> die minimale Schnittstelle implementiert, die erforderlich ist, um Parameter vom Benutzer zu erhalten und den Code zu generieren, der die Vorlagen Ausgabedatei erzeugt. <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> implementiert das Entwurfsmuster "erfordert/bereitstellen". <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> behandelt zwei spezielle Parameter, `requires` und `provides`.  Beispielsweise kann ein benutzerdefinierter Direktivenprozessor einen Dateinamen vom Benutzer akzeptieren, die Datei öffnen und lesen und dann den Text der Datei in einer Variablen mit dem Namen `fileText`speichern. Eine Unterklasse der <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>-Klasse kann einen Dateinamen vom Benutzer als Wert des `requires`-Parameters und den Namen der Variablen, in der der Text als Wert des Parameters `provides` gespeichert werden soll, annehmen. Dieser Prozessor würde die Datei öffnen und lesen und dann den Text der Datei in der angegebenen Variablen speichern.

Bevor Sie einen benutzerdefinierten Direktivenprozessor aus einer Textvorlage in Visual Studio aufzurufen, müssen Sie ihn registrieren.

Weitere Informationen zum Hinzufügen des Registrierungsschlüssels finden Sie unter Bereitstellen [eines benutzerdefinierten direktivenprozessors](../modeling/deploying-a-custom-directive-processor.md).

## <a name="custom-directives"></a>Benutzerdefinierte Direktiven

Eine benutzerdefinierte Direktive sieht wie folgt aus:

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

Sie können einen benutzerdefinierten Direktivenprozessor verwenden, wenn Sie über eine Textvorlage auf externe Daten oder Ressourcen zugreifen möchten.

Verschiedene Textvorlagen können die Funktionalität gemeinsam nutzen, die von einem einzelnen Direktivenprozessor bereitgestellt wird. Daher bieten direktivenprozessoren die Möglichkeit, Code für die Wiederverwendung Die integrierte `include` Direktive ist ähnlich, da Sie Sie verwenden können, um Code zu berücksichtigen und Sie für verschiedene Textvorlagen freizugeben. Der Unterschied besteht darin, dass alle Funktionen, die die `include`-Direktive bereitstellt, korrigiert sind und keine Parameter akzeptieren. Wenn Sie einer Textvorlage allgemeine Funktionen bereitstellen und der Vorlage das Übergeben von Parametern gestatten möchten, müssen Sie einen benutzerdefinierten Direktivenprozessor erstellen.

Einige Beispiele für benutzerdefinierte direktivenprozessoren können wie folgt lauten:

- Ein Direktivenprozessor zum Zurückgeben von Daten aus einer Datenbank, die einen Benutzernamen und ein Kennwort als Parameter akzeptiert.

- Ein Direktivenprozessor zum Öffnen und Lesen einer Datei, die den Namen der Datei als Parameter akzeptiert.

### <a name="principal-parts-of-a-custom-directive-processor"></a>Prinzipal Teile eines benutzerdefinierten direktivenprozessors

Zum Entwickeln eines direktivenprozessors müssen Sie eine Klasse erstellen, die von <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> oder <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>erbt.

Die wichtigsten `DirectiveProcessor` Methoden, die Sie implementieren müssen, sind wie folgt.

- `bool IsDirectiveSupported(string directiveName)` `true` zurück, wenn der Direktivenprozessor die benannte Direktive behandeln kann.

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)`: die Vorlagen-Engine ruft diese Methode für jedes Vorkommen einer Direktive in der Vorlage auf. Der Prozessor sollte die Ergebnisse speichern.

Nach allen Aufrufen von processdirective () werden diese Methoden von der Vorlagen-Engine aufgerufen:

- `string[] GetReferencesForProcessingRun()`: gibt die Namen von Assemblys zurück, die der Vorlagen Code erfordert.

- `string[] GetImportsForProcessingRun()`: gibt die Namespaces zurück, die im Vorlagen Code verwendet werden können.

- `string GetClassCodeForProcessingRun()`: gibt den Code von Methoden, Eigenschaften und anderen Deklarationen zurück, die vom Vorlagen Code verwendet werden können. Die einfachste Möglichkeit hierzu besteht darin, eine Zeichenfolge zu erstellen, C# die den-oder-Visual Basic Code enthält. Damit der Direktivenprozessor aus einer Vorlage aufgerufen werden kann, die eine CLR-Sprache verwendet, können Sie die-Anweisungen als CodeDom-Struktur erstellen und dann das Ergebnis der Serialisierung der Struktur in der von der Vorlage verwendeten Sprache zurückgeben.

- Weitere Informationen finden Sie unter Exemplarische Vorgehensweise [: Erstellen eines benutzerdefinierten direktivenprozessors](../modeling/walkthrough-creating-a-custom-directive-processor.md).

## <a name="see-also"></a>Siehe auch

- Bereitstellen [eines benutzerdefinierten direktivenprozessors](../modeling/deploying-a-custom-directive-processor.md) erläutert das Registrieren eines benutzerdefinierten Anweisungs Prozessors
- Exemplarische Vorgehensweise [: Erstellen eines benutzerdefinierten direktivenprozessors](../modeling/walkthrough-creating-a-custom-directive-processor.md) beschreibt das Erstellen eines benutzerdefinierten direktivenprozessors, das registrieren und Testen des direktivenprozessors und das Formatieren der Ausgabedatei als HTML.
