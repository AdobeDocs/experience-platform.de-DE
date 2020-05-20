---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 1%

---


# Übersicht über Identitäts-Namensraum

Identitätskennungen sind eine Komponente des [Identitätsdienstes](./home.md) , die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert &quot;name<span>@email.com&quot;als E-Mail-Adresse oder &quot;443522&quot;als numerische CRM-ID.

## Erste Schritte

Die Arbeit mit Identitäts-Namensräumen erfordert ein Verständnis der verschiedenen beteiligten Adobe Experience Platform-Dienste. Bevor Sie mit der Arbeit mit Namensräumen beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Identitätsdienst](./home.md): Profitieren Sie von einer besseren Ansicht einzelner Kunden und deren Verhalten, indem Sie Identitäten zwischen Geräten und Systemen überbrücken.
- [Datenschutzdienst](../privacy-service/home.md): Identitäts-Namensraum werden zur Einhaltung der Allgemeinen Datenschutzverordnung (GDPR) verwendet, in der GDPR-Anfragen für einen Namensraum gestellt werden können.

## Identitäts-Namensräume

Eine voll qualifizierte Identität umfasst einen ID-Wert und einen Namensraum. Bei der Zuordnung von Datensatzdaten zu Profil-Fragmenten, z. B. beim Zusammenführen von Profil-Daten in Echtzeit, müssen sowohl der Identitätswert als auch der Namensraum übereinstimmen.

Zwei Profil-Fragmente können z. B. unterschiedliche primäre IDs enthalten, für den Namensraum &quot;E-Mail&quot;jedoch denselben Wert verwenden. Daher kann Platform erkennen, dass diese Fragmente eigentlich dieselbe Person sind und die Daten im Identitätsdiagramm für die Einzelperson zusammenführen.

![](images/identity-service-stitching.png)

### Identitätstypen

Daten können mit verschiedenen Identitätstypen identifiziert werden. Der Identitätstyp wird zum Zeitpunkt der Erstellung des Identitäts-Namensraums angegeben und steuert, ob die Daten im Identitätsdiagramm beibehalten werden, sowie spezielle Anleitungen zum Umgang mit diesen Daten.

Die folgenden Identitätstypen sind in Platform verfügbar:

| Identitätstyp | Beschreibung |
| --- | --- |
| Cookie | Diese Identitäten sind für die Erweiterung von entscheidender Bedeutung und bilden den Großteil des Identitätsdiagramms. Sie verfallen jedoch naturgemäß schnell und verlieren mit der Zeit ihren Wert. Das Löschen von Cookies wird speziell im Identitätsdiagramm behandelt. |
| Geräteübergreifend | Dies deutet darauf hin, dass Identitätsdienst dies als eine starke Personennummer betrachten und somit für immer erhalten sollte. Beispiele sind eine Anmelde-ID, CRM-ID, Loyalität-ID usw. |
| Gerät | Umfasst IDFA-, GAID- und andere IOT-IDs. Diese können auch von Menschen in Haushalten geteilt werden. |
| E-Mail  | Identitäten dieser Art beinhalten persönlich identifizierbare Informationen (PII). Dies ist ein Hinweis an den Identitätsdienst, um den Wert sensibel zu behandeln. |
| Mobil | Zu diesen Identitäten gehören PII. Dies ist ein Hinweis an den Identitätsdienst, um den Wert sensibel zu behandeln. |
| Nichtpersonen | Dient zum Speichern von Identifikatoren, die Namensraum benötigen, aber nicht an einen Personenzusammenschnitt gebunden sind. Diese Bezeichner werden dann aus dem Identitätsdiagramm gefiltert. Mögliche Anwendungsfälle sind Daten zu Produkten, Organisationen, Geschäften usw. (Zum Beispiel eine Produkt-SKU.) |
| Telefon | Zu diesen Identitäten gehören PII. Dies ist ein Hinweis an den Identitätsdienst, um den Wert sensibel zu behandeln. |

### Standard-Namensraum

Adobe Experience Platform bietet verschiedene Identitäts-Namensraum, die für alle Unternehmen verfügbar sind. Diese werden als Standard-Namensraum bezeichnet und sind mit der Identitätsdienst-API oder über die Plattform-Benutzeroberfläche sichtbar.

Klicken Sie auf der linken Leiste auf &quot; **Identitäten** &quot;und dann auf die Registerkarte &quot; *Durchsuchen* &quot;, um die Namensraum &quot;Ansicht Standard&quot;in der Benutzeroberfläche aufzurufen. Alle Identitätskennungen, auf die Ihr Unternehmen zugreifen kann, werden angezeigt. Als Inhaber gilt jedoch &quot;Standard&quot;als Standard-Namensraum.

Sie können dann auf einen der Namensraum klicken, die in den Details zur Ansicht aufgeführt sind.

![](./images/standard-namespace-detail.png)

## Verwalten von Namensräumen in Ihrer Organisation

Je nach Ihren Organisationsdaten und Anwendungsfällen benötigen Sie möglicherweise benutzerdefinierte Namensraum.

Diese sind in der Benutzeroberfläche als Namensraum mit &quot;Benutzerdefiniert&quot;als &quot;Inhaber&quot;sichtbar. Benutzerspezifische Namensraum können mit der Identitätsdienst-API oder über die Benutzeroberfläche erstellt werden.

Um einen benutzerspezifischen Namensraum mithilfe der Benutzeroberfläche zu erstellen, klicken Sie auf **Identitäts-Namensraum** erstellen, füllen Sie das Dialogfeld aus und klicken Sie auf **Erstellen**.

Namensraum, die Sie definieren, sind für Ihr Unternehmen privat und benötigen ein eindeutiges &quot;Identitätssymbol&quot;(oder &quot;Code&quot;, wenn Sie die API verwenden), um erfolgreich erstellt zu werden.

![](./images/create-identity-namespace.png)

Ähnlich wie bei Standard-Namensräumen können Sie auf einen benutzerspezifischen Namensraum auf der Registerkarte &quot; *Durchsuchen* &quot;klicken, um dessen Details Ansicht. Bei einem benutzerspezifischen Namensraum können Sie jedoch auch dessen Anzeigenamen und -beschreibung im Detailbereich bearbeiten.

>[!NOTE] Nachdem ein Namensraum erstellt wurde, kann er nicht gelöscht werden und sein &quot;Identitätssymbol&quot;(oder &quot;Code&quot; in der API) und &quot;Typ&quot; können nicht mehr geändert werden.

## Namensraum in Identitätsdaten

Die Angabe des Namensraums für eine Identität hängt von der Methode ab, mit der Sie Identitätsdaten bereitstellen. Einzelheiten zur Bereitstellung von Daten-Identitätsdaten finden Sie im Abschnitt zur [Bereitstellung von Identitätsdaten](./home.md#supplying-identity-data-to-identity-service) in der Übersicht über den Identitätsdienst.
