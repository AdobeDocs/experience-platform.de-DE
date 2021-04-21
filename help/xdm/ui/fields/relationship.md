---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Arbeitsbereich;Beziehung;Feld;
solution: Experience Platform
title: Definieren von Beziehungsfeldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein Beziehungsfeld in der Benutzeroberfläche "Experience Platform"definieren.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definieren von Beziehungsfeldern in der Benutzeroberfläche

Im Erlebnisdatenmodell (XDM) ist ein [Vereinigung-Schema](../../schema/composition.md#union) eine einheitliche Ansicht aller Schema derselben Klasse, die auch für [Echtzeit-Kundendaten-Profil](../../../profile/home.md) aktiviert wurden. Das Schema Vereinigung wird von Profil genutzt, um eine vollständige Kundendarstellung aus unterschiedlichen Erlebnisdaten zu erstellen.

In einigen Fällen können Sie Daten einbeziehen, die nicht unbedingt Teil eines Profils sind, aber dennoch mit dem Profil in Zusammenhang stehen. Ein Beispiel für diese Art von Daten wäre ein &quot;Lieblingshostfeld&quot;für einen Kunden. Da die Eigenschaften des Lieblingshotels nicht von der Person selbst bestimmt werden, ist ein Hotel am besten durch ein eigenes Schema repräsentiert, das auf einer benutzerspezifischen Klasse basiert und nicht auf [!DNL XDM Individual Profile].

Da Vereinigung-Schema nur auf Schemas basieren, die dieselbe Klasse besitzen, enthält die Aktivierung des Schemas &quot;Hotels&quot;zur Verwendung in Profil nicht das Schema &quot;Vereinigung für Felder [!DNL XDM Individual Profile]&quot;. Stattdessen müssen Sie eine Beziehung zwischen &quot;Hotels&quot; und einem anderen Schema der Vereinigung definieren. Hierzu gehört das Definieren eines **Beziehungsfelds** in einem Quell-Schema, das auf die primäre Identität eines Ziel-Schemas verweist.

Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemas in der Adobe Experience Platform-Benutzeroberfläche finden Sie im [UI-Lernprogramm für Beziehungen](../../tutorials/relationship-ui.md).
