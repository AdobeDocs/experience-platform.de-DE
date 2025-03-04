---
title: Delegaten-Deskriptor-IDs
description: Erfahren Sie mehr über Delegaten-Deskriptor-IDs in der Reactor-API und wie sie Ressourcen mit Erweiterungen verknüpfen.
exl-id: 2c2b9b31-0618-4b93-97ec-0798fc06aac0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 99%

---

# Delegaten-Deskriptor-IDs

Wenn Sie Tags in Adobe Experience Platform verwenden, werden alle Funktionen, die Sie auf Ihrer Site bereitstellen können, durch Erweiterungen bereitgestellt. Die von jeder Erweiterung bereitgestellten Funktionen werden vom Erweiterungsentwickler definiert. Wenn eine Erweiterung bereitgestellt wird, wird sie mit den verschiedenen Funktionen in Form eines [Erweiterungspakets](../endpoints/extension-packages.md) gebündelt. Die Funktionen, die Entwickler einem Erweiterungspaket hinzufügen, werden als „Delegaten“ dieses Pakets betrachtet.

Jedem Delegaten in einem Erweiterungspaket wird eine eindeutige Delegaten-Deskriptor-ID zugewiesen. Die Delegaten-Deskriptor-ID für eine bestimmte Ressource teilt dem System mit, um welche Art von Ressource es sich handelt und zu welchem Erweiterungspaket sie gehört.

## Syntax

Eine Delegaten-Deskriptor-ID besteht aus drei Zeichenfolgen, die durch Doppelpunktzeichen (`::`) verbunden sind und den Namen des Erweiterungspakets, den Delegatentyp bzw. den Delegatennamen darstellen. Diese Zeichenfolgen sind so verfasst, dass sie für Menschen lesbar sind, und werden automatisch vom System generiert und zugewiesen, wenn ein Erweiterungspaket aufgenommen wird.

Wenn beispielsweise ein Erweiterungspaket mit dem Namen `example-package`eine Aktion mit dem Namen`custom-code` enthält, hätte diese Aktion die folgende Delegaten-Deskriptor-ID: `example-package::actions::custom-code`.

## Verwenden von Delegaten-Deskriptor-IDs für entsprechende Ressourcen

Es ist wichtig, Delegaten-Deskriptor-IDs zu verstehen, wenn Sie Regelkomponenten (Ereignisse, Bedingungen und Aktionen) und Datenelemente in der API definieren möchten. In den folgenden Abschnitten wird beschrieben, welche Rolle diese IDs für die einzelnen Ressourcen spielen.

### Regelkomponenten

Eine [Regelkomponente](../endpoints/rule-components.md) muss einem Ereignis, einer Bedingung oder einer Aktion zugeordnet sein, das/die zu einem Erweiterungspaket gehört. Dies stellt den „Typ“ der Regelkomponente dar, der sich auf die Logik der Gesamtregel bezieht (ein Ereignis, eine Bedingung oder eine Aktion). Daher muss beim Erstellen einer Regelkomponente eine Delegierten-Deskriptor-ID bereitgestellt werden, um anzugeben, welchem Ereignis, welcher Bedingung oder Aktion die Regelkomponente zugeordnet werden soll.

Um beispielsweise eine Ereignisregelkomponente zu erstellen, die auf einem `click`-Ereignis in einem Erweiterungspaket `example-package` basiert, würde die Regelkomponente den folgenden `delegate_descriptor_id`-Wert verwenden: `example-package::events::click`.

Weitere Informationen finden Sie im Abschnitt zum [Erstellen einer Regelkomponente](../endpoints/rule-components.md#create).

### Datenelemente

Ein [Datenelement](../endpoints/data-elements.md) muss bei seiner ersten Erstellung einem Erweiterungspaket zugeordnet werden, da jedes Erweiterungspaket die kompatiblen Typen für seine Delegierten-Datenelemente sowie deren beabsichtigtes Verhalten definiert.

Um beispielsweise ein Datenelement zu erstellen, das den vom Erweiterungspaket `example-package` definierten `cookie`-Typ verwendet, würde das Datenelement den folgenden `delegate_descriptor_id`-Wert verwenden: `example-package::dataElements::cookie`.

Weitere Informationen finden Sie im Abschnitt zum [Erstellen eines Datenelements](../endpoints/data-elements.md#create).

### Erweiterungen

Eine [Erweiterung](../endpoints/extensions.md) wird beim ersten Erstellen automatisch einem Erweiterungspaket zugeordnet und im `relationships`-Objekt der Erweiterung dargestellt. Wenn Ihre Erweiterung benutzerdefinierte Einstellungen erfordert, ist auch eine Delegaten-Deskriptor-ID erforderlich.

>[!NOTE]
>
>Erweiterungen, die keine benutzerdefinierten Einstellungen erfordern, benötigen keine Delegierten-Deskriptor-ID.

Um beispielsweise einer Erweiterung, die zum Erweiterungspaket `example-package` gehört, eine Delegierten-Deskriptor-ID hinzuzufügen, würde die Erweiterung den folgenden `delegate_descriptor_id`-Wert verwenden: `example-package::extensionConfiguration::config`.

Weitere Informationen finden Sie im Handbuch zum [Erstellen einer Erweiterung](../endpoints/extensions.md#create).
