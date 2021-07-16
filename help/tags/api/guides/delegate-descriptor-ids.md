---
title: Deskriptor-IDs delegieren
description: Erfahren Sie mehr über Delegate-Deskriptor-IDs in der Reactor-API und wie sie Ressourcen mit Erweiterungen verknüpfen.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 1%

---

# Deskriptor-IDs delegieren

Bei der Verwendung von Tags in Adobe Experience Platform werden alle Funktionen, die Sie auf Ihrer Site bereitstellen können, durch Erweiterungen bereitgestellt. Die von den einzelnen Erweiterungen bereitgestellten Funktionen werden vom Erweiterungsentwickler definiert. Wenn eine Erweiterung bereitgestellt wird, wird sie mit den verschiedenen Funktionen in Form eines [Erweiterungspakets](../endpoints/extension-packages.md) gebündelt. Die Funktionen, die Entwickler zu einem Erweiterungspaket hinzufügen, werden als &quot;Delegate&quot;dieses Pakets betrachtet.

Jeder Delegate innerhalb eines Erweiterungspakets erhält eine eindeutige Delegate-Deskriptor-ID. Die Delegate-Deskriptor-ID für eine bestimmte Ressource teilt dem System mit, welche Ressource es ist und zu welchem Erweiterungspaket es gehört.

## Syntax

Eine Delegate-Deskriptor-ID besteht aus drei Zeichenfolgen, die durch Doppelpunkt-Zeichen (`::`) verbunden werden und den Namen des Erweiterungspakets, den Delegatstyp und den Delegatnamen darstellen. Diese Zeichenfolgen sind für Menschen lesbar und werden automatisch vom System generiert und zugewiesen, wenn ein Erweiterungspaket erfasst wird.

Wenn beispielsweise ein Erweiterungspaket mit dem Namen `example-package` eine Aktion mit dem Namen `custom-code` aufweist, würde diese Aktion die folgende Delegate-Deskriptor-ID aufweisen: `example-package::actions::custom-code`.

## Verwenden von Delegate-Deskriptor-IDs für anwendbare Ressourcen

Deskriptor-IDs delegieren ist wichtig, wenn es um das Definieren von Regelkomponenten (Ereignisse, Bedingungen und Aktionen) und Datenelementen in der API geht. In den folgenden Abschnitten wird beschrieben, wie diese IDs für jede Ressource verwendet werden.

### Regel Komponenten

Eine [Regelkomponente](../endpoints/rule-components.md) muss mit einem Ereignis, einer Bedingung oder einer Aktion verknüpft sein, das/die zu einem Erweiterungspaket gehört. Dies stellt den &quot;Typ&quot;der Regelkomponente dar, da er sich auf die Logik der Gesamtregel bezieht (ein Ereignis, eine Bedingung oder eine Aktion). Daher muss beim Erstellen einer Regelkomponente eine Delegate-Deskriptor-ID bereitgestellt werden, um anzugeben, mit welchem Ereignis, welcher Bedingung oder welcher Aktion die Regelkomponente verknüpft werden soll.

Um beispielsweise eine Ereignisregelkomponente zu erstellen, die auf einem `click`-Ereignis in einem Erweiterungspaket `example-package` basiert, verwendet die Regelkomponente den folgenden `delegate_descriptor_id`-Wert: `example-package::events::click`.

Weitere Informationen finden Sie im Abschnitt [Erstellen einer Regelkomponente](../endpoints/rule-components.md#create) .

### Datenelemente

Ein [Datenelement](../endpoints/data-elements.md) muss bei der ersten Erstellung mit einem Erweiterungspaket verknüpft werden, da jedes Erweiterungspaket die kompatiblen Typen für die delegierten Datenelemente sowie ihr beabsichtigtes Verhalten definiert.

Um beispielsweise ein Datenelement zu erstellen, das den Typ `cookie` verwendet, wie er durch ein Erweiterungspaket `example-package` definiert ist, verwendet das Datenelement den folgenden `delegate_descriptor_id`-Wert: `example-package::dataElements::cookie`.

Weitere Informationen finden Sie im Abschnitt [Erstellen eines Datenelements](../endpoints/data-elements.md#create) .

### Erweiterungen

Eine [Erweiterung](../endpoints/extensions.md) wird bei der ersten Erstellung automatisch mit einem Erweiterungspaket verknüpft und wird im `relationships` -Objekt der Erweiterung dargestellt. Wenn Ihre Erweiterung benutzerdefinierte Einstellungen erfordert, ist auch eine Delegate-Deskriptor-ID erforderlich.

>[!NOTE]
>
>Erweiterungen, für die keine benutzerdefinierten Einstellungen erforderlich sind, benötigen keine Delegate-Deskriptor-ID.

Um beispielsweise eine Delegate-Deskriptor-ID zu einer Erweiterung hinzuzufügen, die zum Erweiterungspaket `example-package` gehört, verwendet die Erweiterung den folgenden `delegate_descriptor_id`-Wert: `example-package::extensionConfiguration::config`.

Weitere Informationen finden Sie im Handbuch zum Erstellen einer Erweiterung](../endpoints/extensions.md#create) .[