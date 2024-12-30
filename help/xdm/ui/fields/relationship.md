---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Beziehung;Feld;
solution: Experience Platform
title: Definieren von Beziehungsfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein Beziehungsfeld in der Experience Platform-Benutzeroberfläche definieren.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definieren von Beziehungsfeldern in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) ist [Vereinigungsschema](../../schema/composition.md#union) eine einheitliche Ansicht aller Schemata derselben Klasse, die auch für das Echtzeit[Kundenprofil aktiviert ](../../../profile/home.md). Das Vereinigungsschema wird vom Profil genutzt, um aus unterschiedlichen Erlebnisdaten eine vollständige Darstellung eines Kunden zu erstellen.

In einigen Fällen nehmen Sie Daten auf, die nicht unbedingt Teil eines Profils sind, aber trotzdem mit dem Profil zusammenhängen. Ein Beispiel für diese Art von Daten wäre das Feld „Lieblingshotel“ für einen Kunden. Da die Attribute des Lieblingshotels einer Person nicht Attribute der Person selbst sind, wird ein Hotel am besten durch ein separates Schema dargestellt, das auf einer benutzerdefinierten Klasse anstatt auf [!DNL XDM Individual Profile] basiert.

Da Vereinigungsschemata nur auf Schemata basieren, die dieselbe Klasse haben, umfasst die einfache Aktivierung des Schemas „Hotels“ zur Verwendung im Profil nicht dessen Felder „Vereinigungsschema“ für [!DNL XDM Individual Profile]. Stattdessen müssen Sie eine Beziehung zwischen „Hotels“ und einem anderen Schema definieren, das zur Vereinigung gehört. Dazu gehört die Definition eines **Beziehungsfelds** in einem Quellschema, das auf die primäre Identität eines Referenzschemas verweist.

Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemata in der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Tutorial zur Beziehungsbenutzeroberfläche](../../tutorials/relationship-ui.md).
