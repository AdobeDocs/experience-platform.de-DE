---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 8. April 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: c3166bea873572fe6ee2e63dfd13bc64d81e252b

---


# Adobe Experience Platform – Versionshinweise

## Veröffentlichungsdatum: 8. April 2020

## Privacy Service

Die neuen gesetzlichen und organisatorischen Vorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten auf Anfrage aus Ihren Datenspeichern zuzugreifen oder sie zu löschen. Der Datenschutzdienst für Adobe Experience Platform stellt eine RESTful-API und eine Benutzeroberfläche bereit, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit dem Datenschutzdienst können Sie Anfragen zum Zugriff auf und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| PDPA-Unterstützung | Datenschutzanforderungen können nun im Rahmen des Datenschutzgesetzes (PDPA) in Thailand erstellt und nachverfolgt werden. Bei Datenschutzanforderungen in der API akzeptiert das `regulation` Array den Wert &quot;pdpa_tha&quot;. |
| Namensraum-Typen in der Benutzeroberfläche | Sie können jetzt im Anforderungs-Builder in der Benutzeroberfläche des Datenschutzdienstes verschiedene Namensraum angeben. Weitere Informationen finden Sie im [Benutzerhandbuch](../../privacy-service/ui/user-guide.md) . |
| Alter Endpunktverfall | Der alte API-Endpunkt (`data/privacy/gdpr`) wurde nicht mehr unterstützt. |

Bekannte Probleme

* Keine

Weitere Informationen zum Datenschutzdienst finden Sie in der Übersicht über den [Datenschutzdienst](../../privacy-service/home.md).

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->