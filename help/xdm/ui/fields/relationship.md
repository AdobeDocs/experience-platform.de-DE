---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Arbeitsbereich; Beziehung; Feld;
solution: Experience Platform
title: Beziehungsfelder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie in der Benutzeroberfläche von Experience Platform ein Beziehungsfeld definieren.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definieren von Beziehungsfeldern in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) ist ein [Vereinigungsschema](../../schema/composition.md#union) eine einheitliche Ansicht aller Schemas, die derselben Klasse gehören und auch für [Echtzeit-Kundenprofil](../../../profile/home.md) aktiviert wurden. Das Vereinigungsschema wird vom Profil genutzt, um eine vollständige Darstellung eines Kunden aus unterschiedlichen Erlebnisdaten zu erstellen.

In einigen Fällen können Sie Daten erfassen, die nicht unbedingt Teil eines Profils sind, aber dennoch mit dem Profil verbunden sind. Ein Beispiel für diese Art von Daten wäre ein Feld &quot;Lieblingshotel&quot;für einen Kunden. Da die Attribute des Lieblingshotels einer Person keine Attribute der Person selbst sind, ist ein Hotel am besten durch ein separates Schema dargestellt, das auf einer benutzerdefinierten Klasse basiert, anstatt [!DNL XDM Individual Profile].

Da Vereinigungsschemas nur auf Schemas basieren, die dieselbe Klasse teilen, enthält die einfache Aktivierung des Schemas &quot;Hotels&quot;zur Verwendung im Profil nicht das Schema der Felderunion für [!DNL XDM Individual Profile]. Stattdessen müssen Sie eine Beziehung zwischen &quot;Hotels&quot;und einem anderen Schema definieren, das zur Vereinigung gehört. Dazu gehört das Definieren eines **Beziehungsfelds** in einem Quellschema, das auf die primäre Identität eines Zielschemas verweist.

Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemas in der Adobe Experience Platform-Benutzeroberfläche finden Sie im Tutorial [Benutzeroberfläche für Beziehungen](../../tutorials/relationship-ui.md).
