---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Arbeitsbereich; Beziehung; Feld;
solution: Experience Platform
title: Beziehungsfelder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein Beziehungsfeld definieren.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definieren von Beziehungsfeldern in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) ist ein [Vereinigungsschema](../../schema/composition.md#union) eine einheitliche Ansicht aller Schemas, die derselben Klasse gehören und auch für das [Echtzeit-Kundenprofil](../../../profile/home.md) aktiviert wurden. Das Vereinigungsschema wird vom Profil genutzt, um eine vollständige Darstellung eines Kunden aus unterschiedlichen Erlebnisdaten zu erstellen.

In einigen Fällen können Sie Daten erfassen, die nicht unbedingt Teil eines Profils sind, aber dennoch mit dem Profil verbunden sind. Ein Beispiel für diese Art von Daten wäre ein Feld &quot;Lieblingshotel&quot;für einen Kunden. Da die Attribute des Lieblingshotels einer Person keine Attribute der Person selbst sind, ist ein Hotel am besten durch ein separates Schema dargestellt, das auf einer benutzerdefinierten Klasse basiert, anstatt durch [!DNL XDM Individual Profile].

Da Vereinigungsschemas nur auf Schemas basieren, die dieselbe Klasse teilen, enthält die einfache Aktivierung des Schemas &quot;Hotels&quot;zur Verwendung im Profil nicht das Schema für die Felderunion für [!DNL XDM Individual Profile]. Stattdessen müssen Sie eine Beziehung zwischen &quot;Hotels&quot;und einem anderen Schema definieren, das zur Vereinigung gehört. Dazu gehört das Definieren eines **Beziehungsfelds** in einem Quellschema, das auf die primäre Identität eines Referenzschemas verweist.

Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemas in der Adobe Experience Platform-Benutzeroberfläche finden Sie im Tutorial [Beziehung-UI-Tutorial](../../tutorials/relationship-ui.md).
