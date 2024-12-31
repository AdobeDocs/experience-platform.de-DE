---
title: Identity Service und Echtzeit-Kundenprofil
description: Erfahren Sie mehr über die Beziehung zwischen Identity Service und Echtzeit-Kundenprofil
exl-id: 09961b8e-f736-4fcc-ac53-88b55cca7d55
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Beziehung zwischen Identity Service und Echtzeit-Kundenprofil

>[!IMPORTANT]
>
>Auf dieser Seite wird davon ausgegangen, dass die Zusammenführungsrichtlinie das Identitätsdiagramm verwendet. Weitere Informationen zu Zusammenführungsrichtlinien im Echtzeit-Kundenprofil finden Sie in der Dokumentation unter [Zusammenführungsrichtlinien und Identitätszuordnung](../profile/merge-policies/overview.md#identity-stitching).

Sie können zwar Identity Service und Echtzeit-Kundenprofil gleichzeitig verwenden, aber die beiden Funktionen von Adobe Experience Platform sind nicht von Natur aus identisch.

* Sie können Identity Service verwenden, um das Identitätsdiagramm zu generieren und zu pflegen, das die unterschiedlichen Identitäten eines einzelnen Kunden zusammenführt.
* Sie können das Echtzeit-Kundenprofil verwenden, um unterschiedliche Profilfragmente zusammenzuführen und ein zusammengeführtes Profil zu erstellen. Dieser Prozess erfordert die Verwendung des Identitätsdiagramms.

In diesem Dokument werden die Ähnlichkeiten, Unterschiede und die Beziehung zwischen Identity Service und dem Echtzeit-Kundenprofil beschrieben.

## Identity Service im Vergleich zu Echtzeit-Kundenprofil

Die wichtigsten Unterschiede zwischen Identity Service und Echtzeit-Kundenprofil sind:

| | Identity Service | Echtzeit-Kundenprofil |
| --- | --- |--- |
| **Zweck** | <ul><li>Sie können Identity Service verwenden, um Identitätsdiagramme zu erstellen und zu verwalten.</li></ul> | Sie können das Echtzeit-Kundenprofil für Folgendes verwenden: <ul><li>Erstellen Sie eine 360-Grad-Ansicht eines Kundenprofils.</li><li>Anzeigen und Verwalten von Profilen</li></ul> |
| **Eingabe** | <ul><li>Um Identity Service zu verwenden, müssen Sie Datensatzdaten oder Zeitreihenereignisse aufnehmen, die mindestens zwei als Identität markierte Felder enthalten. Die Felder, die Sie als Identität markieren, werden dann in Identity Service aufgenommen.</li></ul> | <ul><li>Profilfragmente: stellen eine eindeutige primäre Identität und die entsprechenden Datensätze oder Ereignisdaten für diese ID in einem bestimmten Datensatz dar.</li><li>Identitätsdiagramme: Das Profil verweist auf das Identitätsdiagramm für ein bestimmtes Kundenprofil, um alle Profilfragmente mit denselben primären Identitäten zu identifizieren.</li></ul> |
| **Prozess** | <ul><li>Nachdem Sie mindestens zwei Identitäten aufgenommen haben, verknüpft Identity Service diese Identitäten miteinander.</li></ul> | <ul><li>Das Echtzeit-Kundenprofil führt Profilfragmente zusammen und verweist dabei auf die entsprechenden Identitätsdiagramme.</li></ul> |
| **Ausgabe** | <ul><li>Das Ergebnis ist ein Identitätsdiagramm, d. h. ein Satz von Identitäten, die sich auf eine Person beziehen.</li></ul> | <ul><li>Das Ergebnis ist ein zusammengeführtes Profil, das eine einzige und umfassende Ansicht eines bestimmten Kunden darstellt. Dieses Profil kann sich dann für ein Segment qualifizieren.</li></ul> |

{style="table-layout:auto"}

## Erstellung eines zusammengeführten Profils

Lesen Sie die folgenden Schritte, um ein besseres Verständnis für den Prozess der Erstellung eines zusammengeführten Profils zu erhalten:

* Zunächst verweist das Echtzeit-Kundenprofil auf ein Identitätsdiagramm und ruft alle Identitäten ab.
* Als Nächstes ruft das Profil Profilfragmente mit primären Identitäten im Identitätsdiagramm ab.
* Nach erfolgreichem Abschluss führt das Profil alle vorhandenen Ereignisse und Attribute zusammen.
   * Wenn Attributinformationen miteinander in Konflikt stehen, werden die Attribute anhand der Zusammenführungsmethode ausgewählt. Weitere Informationen finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../profile/merge-policies/overview.md).

![Flussdiagramm, in dem die Funktionsweise von Identity Service und Profilzusammenführung beschrieben wird.](./images/merge-profile-process.png)

## Bestimmen eines Felds als Identität

Im Experience-Datenmodell (XDM) ist das Markieren oder Festlegen eines Felds als Identität eine Anweisung für das Experience Platform, dieses bestimmte Feld in Identity Service aufzunehmen. Diese Bezeichnung ermöglicht dann die Zusammenführung von Profilfragmenten im Echtzeit-Kundenprofil. Wenn keine Profilfragmente mit der Identität verknüpft sind, weisen Sie sie nicht als Identität zu.

### Grundlagen zu primären und sekundären Identitäten

Nachdem Sie Felder als Identitäten markiert haben, können sie entweder als primäre oder sekundäre Identitäten definiert werden. Primäre und sekundäre Identitätskonzepte sind Teil des Echtzeit-Kundenprofils.

* Die primäre Identität (manchmal auch als „Primärschlüssel“ bezeichnet) ist die Identität, in der Profilfragmente gespeichert werden.
* Wenn in einer Datenzeile nur eine Identität vorhanden ist, wird diese einzelne Identität als primär gekennzeichnet.
* Wenn zwei oder mehr Identitäten vorhanden sind, wird eine als primär und die andere als sekundär gekennzeichnet.

Identity Service stellt Links zwischen Identitäten her, solange mindestens zwei Felder als Identität markiert sind. Identity Service speichert keine Informationen darüber, ob eine Identität primär oder sekundär ist.

