---
title: Sensible und persönliche Informationen in XDM
description: Erfahren Sie mehr über die wichtigsten Aspekte bezüglich sensibler personenbezogener Daten (SPI) und persönlich identifizierbarer Informationen (PII) im Experience-Datenmodell (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 302dca9a9f834dba1fd3fdac15284ea4e2fba282
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---

# Sensible und persönliche Informationen in XDM

Das Experience-Datenmodell (XDM) bietet standardmäßige Datenstrukturen zur Verwendung in Adobe Experience Platform, mit denen Sie Daten zu Kundenerlebnissen erfassen können. Diese Daten können vertrauliche persönliche Daten (SPI) und persönlich identifizierbare Informationen (PII) wie die E-Mail-Adresse, den Namen, die Konto-ID und andere Datenfelder eines Kunden umfassen.

Organisationsregeln und rechtliche Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) erzwingen Einschränkungen hinsichtlich der Art und Weise, wie SPI und personenbezogene Daten erfasst, gespeichert, verwendet und freigegeben werden können. Daher ist es wichtig zu berücksichtigen, welche Felder in Ihrem Datenmodell sensible oder personenbezogene Daten darstellen, und sicherzustellen, dass Ihre Vorgänge unter die organisatorischen und rechtlichen Richtlinien fallen.

In diesem Dokument werden wichtige Aspekte bezüglich sensibler und personenbezogener Daten in XDM behandelt.

## Bestimmen, welche Felder sensible oder personenbezogene Daten enthalten

Was SPI und PII ausmacht, ist sehr kontextspezifisch. Daher liegt es an Ihnen, Ihr Datenmodell, Ihre Geschäftsabläufe und die anwendbaren Vorschriften zu verstehen, um zu bestimmen, welche Schemafelder sensible oder personenbezogene Daten darstellen.

Beispielsweise hat die rechtliche Zuständigkeit Ihrer Kunden direkte Auswirkungen darauf, welche Informationen als vertraulich betrachtet werden. Die DSGVO enthält solide Definitionen für SPI und PII, doch können Kunden außerhalb des Europäischen Wirtschaftsraums (EWR) unterschiedlichen Definitionen und Beschränkungen unterliegen.

## Umgang mit sensiblen und personenbezogenen Daten

Ähnlich wie die Definitionen für vertrauliche und personenbezogene Daten selbst sind auch die Einschränkungen für die Verarbeitung dieser Daten kontextspezifisch.

Die Einwilligung des Kunden ist häufig ein entscheidender Faktor dafür, welche Daten erfasst und verarbeitet werden können und für welche Zwecke. Abhängig von der gesetzlichen Gerichtsbarkeit, der Ihre Kunden unterliegen, kann eine ausdrückliche Einwilligung erforderlich sein, damit ihre sensiblen und personenbezogenen Daten erfasst werden können. Selbst in Fällen, in denen keine ausdrückliche Einwilligung erforderlich ist, gelten je nach dem, was der Datenschutzhinweis dem Kunden sagt, weiterhin Einschränkungen hinsichtlich der Datenverarbeitung.

Wenden Sie sich an Ihr Rechtsteam, um zu bestimmen, wie vertrauliche und personenbezogene Daten für Ihre geschäftlichen Anwendungsfälle verarbeitet werden sollen.

## Beschränkung der Verwendung sensibler und personenbezogener Daten

XDM bietet eine Vielzahl von Standardfeldgruppen und Datentypen, um relevante, häufig verwendete Datenstrukturen zu beschreiben, mit denen Kundenerlebnisse optimiert werden können. Wenn eine empfohlene Standardressource eingeschränkte Felder enthält, die Sie nicht in Ihre Schemas aufnehmen möchten, müssen Sie diese Ressource nicht verwenden.

Mit Platform können Sie eigene benutzerdefinierte Feldergruppen und Datentypen definieren, sodass Sie die Struktur Ihrer Daten vollständig steuern können, wenn verfügbare Standardressourcen Ihren Anforderungen nicht entsprechen. Weitere Informationen zum Definieren dieser benutzerdefinierten Ressourcen finden Sie in der folgenden Dokumentation:

* [Erstellen einer benutzerdefinierten Feldgruppe](../ui/resources/field-groups.md#create)
* [Erstellen eines benutzerdefinierten Datentyps](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI und PII sollten nur in den Klassen [XDM Individual Profile](../classes/individual-profile.md) und [XDM ExperienceEvent](../classes/experienceevent.md) gespeichert werden. Als Best Practice für das Löschen von Daten sowie Datenschutz und Governance sollten Sie SPI und PII nicht in anderen benutzerdefinierten oder standardmäßigen XDM-Klassen speichern.

## Nächste Schritte

In diesem Dokument wurden wichtige Aspekte bezüglich sensibler und personenbezogener Daten in XDM behandelt. Weitere Informationen dazu, wie Sie Ihre Schemas modellieren, um Ihre geschäftlichen Anwendungsfälle am besten zu erfüllen, finden Sie im Handbuch zu [Best Practices für die Datenmodellierung](./best-practices.md).

Weitere Informationen zu Data Governance- und Datenschutzfunktionen in Experience Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit](../../landing/governance-privacy-security/overview.md).
