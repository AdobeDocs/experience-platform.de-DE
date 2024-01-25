---
title: Beispielszenarios für die Konfiguration von Identitätseinstellungen
description: Erfahren Sie mehr über Beispielszenarien zum Konfigurieren von Identitätseinstellungen.
hide: true
hidefromtoc: true
badge: Alpha
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 3%

---

# Beispielszenarien für die Konfiguration von Regeln für die Zuordnung von Identitätsdiagrammen

>[!IMPORTANT]
>
>Verknüpfungsregeln für Identitätsdiagramme befinden sich derzeit im Alpha. Die Funktion und die Dokumentation können sich ändern.

In diesem Dokument werden Beispielszenarien beschrieben, die Sie bei der Konfiguration von Regeln für die Verknüpfung von Identitätsdiagrammen in Betracht ziehen können.

## Freigegebenes Gerät

Es gibt Fälle, in denen mehrere Anmeldungen auf einem einzelnen Gerät stattfinden können:

| Freigegebenes Gerät | Beschreibung |
| --- | --- |
| Familiencomputer und Tablets | Sowohl Ehemann als auch Ehefrau melden sich auf ihren jeweiligen Bankkonten an. |
| Öffentlicher Kiosk | Reisende an einem Flughafen, die sich mit ihrer Treuekennung anmelden, können Taschen und Bordkarten einchecken. |
| Callcenter | Die Mitarbeiter des Callcenters melden sich auf einem einzelnen Gerät im Namen von Kunden an, die den Kundensupport aufrufen, um Probleme zu lösen. |

![shared-devices](../images/identity-settings/shared-devices.png)

In diesen Fällen wird aus Diagrammsicht eine einzelne ECID mit mehreren CRM-IDs verknüpft, ohne dass Einschränkungen aktiviert sind.

Mit den Verknüpfungsregeln für Identitätsdiagramme können Sie:

* Konfigurieren Sie die für die Anmeldung verwendete ID als eindeutige Kennung. Sie können beispielsweise ein Diagramm so einschränken, dass nur eine Identität mit einem CRM-ID-Namespace gespeichert wird, und diese CRM-ID so als eindeutige Kennung eines gemeinsam genutzten Geräts definieren.
   * Dadurch können Sie sicherstellen, dass CRM-IDs nicht von der ECID zusammengeführt werden.

## Ungültige E-Mail-/Telefonszenarien

Es gibt auch Fälle von Benutzern, die bei der Registrierung falsche Werte als Telefonnummern und/oder E-Mail-Adressen angeben. Wenn in diesen Fällen Beschränkungen nicht aktiviert sind, werden telefonische/E-Mail-bezogene Identitäten letztendlich mit mehreren verschiedenen CRM-IDs verknüpft.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Mit den Verknüpfungsregeln für Identitätsdiagramme können Sie:

* Konfigurieren Sie entweder die CRM-ID, Telefonnummer oder E-Mail-Adresse als eindeutige Kennung und beschränken Sie so eine Person auf nur eine CRM-ID, Telefonnummer und/oder E-Mail-Adresse, die mit ihrem Konto verknüpft ist.

## Fehlerhafte oder falsche Identitätswerte

Es gibt Fälle, in denen nicht eindeutige, fehlerhafte Identitätswerte im System erfasst werden, unabhängig vom Namespace. Zu den Beispielen gehören:

* IDFA-Namespace mit dem Identitätswert &quot;user_null&quot;.
   * IDFA-Identitätswerte sollten 36 Zeichen enthalten: 32 alphanumerische Zeichen und vier Bindestriche.
* Namespace für Telefonnummern mit dem Identitätswert &quot;Nicht angegeben&quot;.
   * Telefonnummern dürfen keine Buchstaben enthalten.

Diese Identitäten können zu folgenden Diagrammen führen, in denen mehrere CRM-IDs mit der &quot;schlechten&quot;Identität zusammengeführt werden:

![bad-data](../images/identity-settings/bad-data.png)

Mit den Regeln zur Verknüpfung von Identitätsdiagrammen können Sie die CRM-ID als eindeutige Kennung konfigurieren, um unerwünschte Profilzusammenbrüche aufgrund dieses Datentyps zu verhindern.

## Nächste Schritte

Weitere Informationen zu Regeln zur Verknüpfung von Identitätsdiagrammen finden Sie in der folgenden Dokumentation:

* [Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen](./overview.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Identity Service und Echtzeit-Kundenprofil](../identity-and-profile.md)
* [Identitätsverknüpfungslogik](../features/identity-linking-logic.md)
