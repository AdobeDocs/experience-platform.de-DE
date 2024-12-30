---
title: Vertrauliche und persönliche Informationen in XDM
description: Erfahren Sie mehr über wichtige Aspekte zu sensiblen personenbezogenen Daten (SPI) und persönlich identifizierbaren Informationen (PII) im Experience-Datenmodell (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 302dca9a9f834dba1fd3fdac15284ea4e2fba282
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---

# Sensible und persönliche Informationen in XDM

Das Experience-Datenmodell (XDM) stellt Standarddatenstrukturen für die Verwendung in Adobe Experience Platform bereit, mit denen Sie Daten zu Kundenerlebnissen erfassen können. Zu diesen Daten können sensible personenbezogene Daten (SPI) und persönlich identifizierbare Informationen (PII) wie die E-Mail-Adresse, der Name, die Konto-ID und andere Datenfelder eines Kunden gehören.

Organisatorische Regeln und rechtliche Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) erzwingen Einschränkungen hinsichtlich der Art und Weise, wie SPI und PII erfasst, gespeichert, verwendet und freigegeben werden können. Daher ist es wichtig, zu überlegen, welche Felder sensible oder persönliche Informationen in Ihrem Datenmodell darstellen, und sicherzustellen, dass Ihre Vorgänge den organisatorischen und rechtlichen Richtlinien entsprechen.

In diesem Dokument werden wichtige Überlegungen zu vertraulichen und personenbezogenen Daten in XDM behandelt.

## Festlegen, welche Felder sensible oder personenbezogene Daten enthalten

Was SPI und PII ausmacht, ist sehr kontextspezifisch. Daher müssen Sie Ihr Datenmodell, Ihre Geschäftsvorgänge und die geltenden Vorschriften verstehen, um zu bestimmen, welche Schemafelder sensible oder persönliche Daten darstellen.

Beispielsweise hat die rechtliche Zuständigkeit Ihrer Kunden eine direkte Auswirkung darauf, welche Informationen als sensibel betrachtet werden. Die DSGVO enthält robuste Definitionen für SPI und PII, aber für Kunden außerhalb des Europäischen Wirtschaftsraums (EWR) können andere Definitionen und Einschränkungen gelten.

## Umgang mit sensiblen und personenbezogenen Daten

Ähnlich wie bei den Definitionen für vertrauliche und personenbezogene Daten selbst sind auch die Einschränkungen für den Umgang mit diesen Daten kontextspezifisch.

Die Einwilligung des Kunden ist oft ein entscheidender Faktor dafür, welche Daten zu welchen Zwecken erfasst und verarbeitet werden können. Abhängig von der Rechtszuständigkeit, der Ihre Kunden unterliegen, kann eine ausdrückliche Einwilligung erforderlich sein, damit ihre sensiblen und personenbezogenen Daten erfasst werden. Selbst in Fällen, in denen keine ausdrückliche Einwilligung erforderlich ist, gelten Datenverarbeitungsbeschränkungen weiterhin, je nachdem, was die Datenschutzerklärung dem Kunden sagt.

Wenden Sie sich an Ihre Rechtsabteilung, um zu bestimmen, wie sensible und personenbezogene Daten für Ihre geschäftlichen Anwendungsfälle verarbeitet werden sollten.

## Einschränkung der Verwendung sensibler und personenbezogener Daten

XDM bietet eine Vielzahl von Standardfeldgruppen und -datentypen, um relevante, häufig verwendete Datenstrukturen zu beschreiben, die Kundenerlebnisse verbessern. Wenn eine empfohlene Standardressource eingeschränkte Felder enthält, die Sie nicht in Ihre Schemata aufnehmen möchten, müssen Sie diese Ressource jedoch nicht verwenden.

Platform ermöglicht es Ihnen, eigene benutzerdefinierte Feldergruppen und Datentypen zu definieren, sodass Sie umfassend steuern können, wie Ihre Daten strukturiert sind, wenn verfügbare Standardressourcen Ihre Anforderungen nicht erfüllen. Weitere Informationen dazu, wie Sie diese benutzerdefinierten Ressourcen definieren, finden Sie in der folgenden Dokumentation:

* [Erstellen einer benutzerdefinierten Feldgruppe](../ui/resources/field-groups.md#create)
* [Erstellen eines benutzerdefinierten Datentyps](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI und PII sollten nur in den Klassen [XDM Individual Profile](../classes/individual-profile.md) und [XDM ExperienceEvent](../classes/experienceevent.md) gespeichert werden. Speichern Sie SPI und PII nicht in anderen benutzerdefinierten oder standardmäßigen XDM-Klassen, da dies die Best Practice für die Datenlöschung sowie für Datenschutz- und Governance-Zwecke ist.

## Nächste Schritte

In diesem Dokument wurden wichtige Überlegungen zu vertraulichen und personenbezogenen Daten in XDM behandelt. Weitere Informationen zur Modellierung Ihrer Schemata für Ihre geschäftlichen Anwendungsfälle finden Sie im Handbuch zu [Best Practices für die Datenmodellierung](./best-practices.md).

Weitere Informationen zu den Data Governance- und Datenschutzfunktionen in Experience Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit](../../landing/governance-privacy-security/overview.md).
