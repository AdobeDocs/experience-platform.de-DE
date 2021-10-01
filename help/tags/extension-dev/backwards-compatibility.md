---
title: Abwärtskompatibilitätsstandard
description: Erfahren Sie mehr über den Abwärtskompatibilitätsstandard in Adobe Experience Platform, der sicherstellt, dass aktualisierte Versionen von Tag-Erweiterungen mit früheren Versionen kompatibel sind.
exl-id: 325390f1-88c7-4b9e-a484-5442ca649bdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 100%

---

# Abwärtskompatibilitätsstandard

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Aktualisierungen einer Tag-Erweiterung in Adobe Experience Platform müssen abwärtskompatibel mit früheren Versionen der Erweiterung sein. Das bedeutet:

* Änderungen an den Primärkomponenten der Erweiterungen müssen mit früheren Versionen kompatibel sein. Dazu gehören Erweiterungskonfiguration, Ereignistypen, Bedingungstypen, Aktionstypen, Datenelementtypen und gemeinsame Module.
* Komponenten, die ein User mit der älteren Erweiterungsversion erstellt hat, müssen die Tauglichkeitsprüfung für die Schemas bestehen können, die von der neueren Version erstellt werden.
* Wenn ein Benutzer von Adobe Experience Platform eine aktualisierte Version Ihrer Erweiterung installiert, sollten alle bisherigen Funktionen unverändert bleiben, bis er absichtlich Änderungen vornimmt.

## Zulässige Änderungen

Die folgenden Arten von Änderungen an Ihrer Erweiterung sind zulässig:

1. Sie können neue Komponenten hinzufügen (Ereignistypen, Bedingungstypen usw.).
1. Sie können Ihren Erweiterungskonfigurationseinstellungen neue optionale Felder hinzufügen.
1. Sie können erforderliche Felder in optionale Felder ändern.

## Verbotene Änderungen

Die folgenden Arten von Änderungen an Ihrer Erweiterung sind nicht zulässig:

1. Eine Komponente darf nicht umbenannt werden.
1. Eine Komponente darf nicht entfernt werden.
1. Sie dürfen nicht ein Feld aus einer Komponente entfernen.
1. Sie dürfen optionale Felder nicht in erforderliche Felder ändern.
1. Sie dürfen keine neuen erforderlichen Felder hinzufügen.
1. Sie dürfen die API vorhandener freigegebener Module nicht ändern.

Wenn Sie eine dieser Änderungen vornehmen, hat jeder Benutzer, der Ihre Erweiterung in seiner Eigenschaft installiert hat, sofort Probleme wie etwa:

* Regeln werden nicht mehr korrekt ausgeführt, da eine der Regelkomponenten nach einer nicht vorhandenen Komponente sucht
* Alle Builds schlagen fehl, da die Bibliothek eine Upstream-Ressource enthält, die nicht mehr in der Erweiterung vorhanden ist
* Alle Builds schlagen fehl, da die Bibliothek eine Ressource mit Einstellungen enthält, die bei der Tauglichkeitsprüfung für das neue Schema fehlschlagen

Vor allem in diesem zweiten Fall kann es passieren, dass Benutzer ohne Abhilfe und ohne Möglichkeit zurückgelassen werden, ihre Eigenschaft so zu korrigieren, dass sie erneut veröffentlichen können.

## Entfernen von Funktionen

Es kann Situationen geben, in denen Sie einen gültigen Geschäftsgrund haben und glauben, dass Sie wirklich eine verbotene Änderung vornehmen müssen (siehe oben). Dies ist zwar weiterhin nicht möglich, aber stattdessen können Sie Folgendes tun:

1. Ich möchte eine Komponente entfernen => Eine neue Komponente erstellen und die alte für veraltet erklären
1. Ich möchte ein Feld aus einer Komponente entfernen => Eine neue Komponente ohne dieses Feld erstellen und die alte für veraltet erklären
1. Ich möchte ein optionales Feld so ändern, dass es erforderlich wird => Erstellen Sie eine neue Komponente, die das gewünschte Feld erfordert, und erklären Sie die alte für veraltet
1. Ich möchte die API eines gemeinsames Moduls ändern => Erstellen Sie ein neues gemeinsames Modul und erklären Sie das alte für veraltet

Möglicherweise greifen Sie einen allgemeinen Thread auf. Das ist gut. Wenn Sie eine alte Komponente einstellen, sollten Sie die Benutzer Ihrer Erweiterung darüber informieren, dass sie veraltet ist und sie zu einer neuen Erweiterung wechseln müssen.  Einige Vorschläge zur Kommunikation mit Benutzern:

* Aktualisieren Sie den Anzeigenamen der alten Komponente durch den Zusatz „(nicht mehr unterstützt)“.
* Aktualisieren Sie die Ansicht für die alte Komponente durch einen großen Warnhinweis in rot, der besagt, dass diese Komponente nicht mehr unterstützt wird und der Benutzer zur neuen Komponente wechseln sollte.
* Aktualisieren Sie den Code Ihres Moduls so, dass Hinweise auf die veraltete Komponente in der Konsole protokolliert werden.  Denken Sie daran, dass diese Meldungen den Endbenutzern angezeigt werden, also halten Sie sie sauber und etwas allgemein.
* Senden Sie nette, freundliche E-Mail-Nachrichten von Ihrem CRM-System.

In Fällen, in denen eine alte Funktion nicht nur unerwünscht, sondern in Ihrer Lösung überhaupt nicht mehr vorhanden ist, gibt es einen weiteren Schritt, den Sie tun können – aber Sie sollten dies erst tun, nachdem Sie Ihre Benutzer informiert und ihnen genug Zeit zur Aktualisierung gegeben haben.

* Aktualisieren Sie den Inhalt Ihres Moduls so, dass es gar nichts tut. Dadurch werden zwar die Funktionen im nächsten Build aus der bereitgestellten Bibliothek des Benutzers entfernt, aber keine Regeln verletzt oder Builds des Benutzers beschädigt.

### Wiederherstellen entfernter Funktionen

Wenn Sie bereits Funktionen entfernt haben und von Benutzern hören, dass dadurch Dinge kaputt gehen, müssen Sie eine neue Version Ihrer Erweiterung veröffentlichen, die die entfernten Komponenten wiederherstellt.

Es ist in Ordnung, sie in einem veralteten Zustand wie oben beschrieben wiederherzustellen, aber sie müssen existieren.

Nehmen wir an, Sie haben eine Version 1.0 mit Komponente XYZ, die von Benutzern verwendet wird. Dann veröffentlichen Sie eine Version 1.1, die keine Komponente XYZ mehr enthält. Sie hören von Ihren Benutzern, dass Ihre Erweiterung ihre Eigenschaften beschädigt hat, und Sie müssen das reparieren. Sie müssen eine Version 1.2 veröffentlichen, die die Komponente XYZ zurückbringt (möglicherweise in einem veralteten Zustand, was Ihnen obliegt), und Ihre Benutzer auf Version 1.2 aktualisieren lassen, damit die Dinge wieder funktionieren.
