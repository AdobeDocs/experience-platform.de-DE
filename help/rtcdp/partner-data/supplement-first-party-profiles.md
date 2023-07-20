---
title: (Beta) Ergänzung von Erstanbieterprofilen mit von Partnern bereitgestellten Attributen
description: Erfahren Sie, wie Sie Erstanbieterprofile mit Attributen vertrauenswürdiger Datenpartner ergänzen, um Ihre Datenbasis zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und die Zielgruppenoptimierung zu verbessern.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 486e1390dfa0602bef15d196d4a1a5befdc9ff23
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Ergänzung von Erstanbieterprofilen mit von Partnern bereitgestellten Attributen

>[!AVAILABILITY]
>
>* Diese Betafunktion steht Kunden zur Verfügung, die Real-Time CDP (App Service), Adobe Experience Platform Activation, Echtzeit-Kundendatenplattform, Real-Time CDP Prime und Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie im Abschnitt [Produktbeschreibungen](https://helpx.adobe.com/legal/product-descriptions.html) und wenden Sie sich für weitere Informationen an Ihren Kundenbetreuer.

Ergänzung von Erstanbieterprofilen mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datenbasis zu verbessern, neue Einblicke in Ihre Kundenbasis zu erhalten und eine bessere Zielgruppenoptimierung zu erzielen.

![Anreichern von Profilen mit von Partnern bereitgestellten Attributen - Überblick über die Anwendungsfälle auf hoher Ebene.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Voraussetzungen und Planung {#prerequisites-and-planning}

Wenn Sie erwägen, Ihre eigenen Erstanbieterprofile mit Attributen von Datenpartnern zu ergänzen, sollten Sie die folgenden Details zur Dateneranreicherungsschleife mit dem Datenpartner besprechen und ansprechen:

* Denken Sie an den Ort, an dem die Zielgruppenliste aus Real-Time CDP exportiert und für den Datenanbieter freigegeben wird. Dieser Speicherort muss den Dateiexport unterstützen.
* Welche Kennungen werden vom Datenanbieter erwartet, damit sie sich auf zusätzliche Attribute beziehen können?
* Wie wird die Datei mit von Partnern bereitgestellten Attributen wieder in die Echtzeit-Kundendatenplattform aufgenommen? Beispielsweise können die Dateien über Cloud-Speicher-Quell-Connectoren wie [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) oder [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Wie häufig erwarten Sie, dass von Partnern bereitgestellte Attribute wieder in Real-Time CDP integriert und aktualisiert werden?

>[!WARNING]
>
>Die zusätzlichen von den Partnern bereitgestellten Attribute, die in Real-Time CDP erfasst werden, wirken sich auf Ihre *Durchschnittliche Profilreichweite*. Lesen Sie die [Real-time Customer Data Platform-Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) für weitere Informationen über den Reichtum der Profile.

## So erreichen Sie den Anwendungsfall: Übersicht auf hoher Ebene {#achieve-the-use-case-high-level}

![Anreichern von Profilen mit von Partnern bereitgestellten Attributen - Überblick über die Anwendungsfälle auf hoher Ebene.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Als **customer**, lizenzieren Sie Attribute aus dem **Datenpartner**.
2. Als **customer**, erweitern Sie Ihre Profildaten und Ihr Governance-Modell um **Partner**-bereitgestellte Attribute.
3. Als **customer**, integrieren Sie die Zielgruppen, die mit dem Datenpartner angereichert werden sollen. Im Allgemeinen werden diese Zielgruppen von Eingabe-IDs wie PII-Elementen (Personally Identifiable Information, PII) wie E-Mail, Name, Adresse usw. abgeleitet.
4. Die **Partner** hängt lizenzierte Attribute für die Profile an, mit denen sie übereinstimmen können. Optional kann ein [Partner-ID](/help/identity-service/namespaces.md) kann in den Partner-Scoped-ID-Namespace eingeschlossen und darin aufgenommen werden.
5. Als **customer**, laden Sie Attribute vom Datenpartner in Kundenprofile in Real-Time CDP.

## So erreichen Sie den Anwendungsfall: Schrittweise Anleitungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte durch, die Links zur weiteren Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Lizenzattribute des Partners {#license-attributes-from-partner}

Dieser Schritt wird im Abschnitt [Voraussetzungen](#prerequisites-and-planning) und Adobe setzt voraus, dass Sie über die richtigen vertraglichen Vereinbarungen mit vertrauenswürdigen Datenanbietern verfügen, um Ihre Erstanbieterprofile zu ergänzen.

### Erweitern Sie Ihre Profildaten und Ihr Governance-Modell, um von Partnern bereitgestellte Attribute aufzunehmen. {#extend-governance-model}

An dieser Stelle erweitern Sie Ihr Data-Management-Framework in Real-Time CDP, um von Partnern bereitgestellte Attribute aufzunehmen.

Sie haben die Möglichkeit, ein neues Schema der **[!UICONTROL XDM Individual Profile]** -Klasse oder erweitern Sie ein vorhandenes Schema desselben Typs, um von Partnern bereitgestellte Attribute einzuschließen. Adobe empfiehlt dringend, ein neues Schema mit einem neuen Satz von Feldergruppen zu erstellen, die die zusätzlichen Attribute des Datenanbieters am besten darstellen. Dadurch wird sichergestellt, dass Ihre Datenschemata sauber sind und unabhängig voneinander entwickelt werden können.

Um von Partnern bereitgestellte Attribute in ein Schema einzuschließen, können Sie entweder eine neue Feldergruppe mit den erwarteten Attributen erstellen oder eine der von Adobe bereitgestellten vorkonfigurierten Feldergruppen verwenden.

Weitere Informationen finden Sie auf den folgenden Dokumentationsseiten:

* [Grundlagen der Schemakomposition](/help/xdm/schema/composition.md)
* [Übersicht über die [!UICONTROL XDM Individual Profile] class](/help/xdm/classes/individual-profile.md)
* [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](/help/xdm/ui/resources/schemas.md)
* [Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Überlegen Sie in diesem Schritt außerdem, wie sich Ihr Data Governance-Modell ändert, wenn Sie Ihre Data-Management-Strategie erweitern und Daten von Drittanbietern einschließen, die vom Partner bereitgestellt werden. Beachten Sie die Überlegungen in den folgenden Links zur Dokumentation:

* (**In Kürze verfügbar**) Halten Sie Drittanbieterdaten in einem separaten Datensatz, damit das Löschen und Rückgängigmachen von Integrationen einfach ist.
* (**In Kürze verfügbar**) Verwenden Sie die [Datensatzablauf](/help/hygiene/ui/dataset-expiration.md) für Kunden, die das Data Hygiene-Add-on erworben haben.
* (**In Kürze verfügbar**) Gehen Sie beim Erstellen abgeleiteter Datensätze, die Daten von Drittanbietern abrufen, vorsichtig vor, da die einzige Lösung zum Entfernen der Daten von Drittanbietern darin besteht, den gesamten abgeleiteten Datensatz zu löschen.

>[!TIP]
>
>Wenn Sie Ihre Kundenprofile durch eine personenbasierte Kennung des Datenanbieters ergänzen möchten, können Sie einen neuen Identitätstyp des Typs **[[!UICONTROL Partner-ID]](/help/identity-service/namespaces.md)**.
>
>Weitere Informationen zur Partner-ID finden Sie im Abschnitt [Identitätstypen-Abschnitt](/help/identity-service/namespaces.md).
>Informationen [Identitätsfelder definieren](/help/xdm/ui/fields/identity.md) in der Experience Platform-Benutzeroberfläche.

### Zielgruppen exportieren, die bei der Eingabe von personenbezogenen Daten (PII) oder Hash-PII angereichert werden sollen {#export-audiences}

Exportieren Sie die Zielgruppen, die der Partner anreichern soll. Verwenden Sie die von der Echtzeit-Kundendatenplattform bereitgestellten Cloud-Speicher-Ziele, z. B. Amazon S3 oder SFTP. Lesen Sie die folgenden Dokumentationsseiten, um diesen Schritt abzuschließen:

* [Amazon S3-Ziel](/help/destinations/catalog/cloud-storage/amazon-s3.md) Dokumentationsseite
* [SFTP-Ziel](/help/destinations/catalog/cloud-storage/sftp.md) Dokumentationsseite
* Anleitung [Verbindung zu einem Ziel herstellen](/help/destinations/ui/connect-destination.md)
* Anleitung [Exportieren von Daten in ein Cloud-Speicher-Ziel](/help/destinations/ui/activate-batch-profile-destinations.md)

### Ihr Datenpartner hängt lizenzierte Attribute für die Profile an, mit denen er übereinstimmen kann {#partner-appends-attributes}

In diesem Schritt hängt Ihr Datenpartner lizenzierte Attribute für die exportierte Zielgruppe an. Die Ausgabe ist im Allgemeinen als flache Datei verfügbar, die wieder in Real-Time CDP aufgenommen werden kann. Mehr dazu [Erfassen von Dateien in Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP hängt angereicherte Attribute an das Kundenprofil an {#ingest-data}

Jetzt müssen Sie Daten vom Partner über einen Quell-Connector erfassen, um die angereicherten Daten wieder in Real-Time CDP zu bringen und Ihre Profile mit von Partnern bereitgestellten Daten zu ergänzen.

Zu diesem Zweck werden u. U. einige Quell-Connectoren empfohlen:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Einschränkungen und Fehlerbehebung {#limitations-and-troubleshooting}

Beachten Sie die folgenden Einschränkungen, wenn Sie den auf dieser Seite beschriebenen Anwendungsfall untersuchen:

* Wenn Sie sich für die Verwendung von Partner-IDs entscheiden, beachten Sie, dass diese IDs beim Erstellen Ihrer [Identitätsdiagramm](/help/identity-service/ui/identity-graph-viewer.md).

## Andere Anwendungsfälle, die durch die Partnerdatenunterstützung erreicht werden {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die über die Unterstützung von Partnerdaten in Real-Time CDP aktiviert wurden:

* (**In Kürze verfügbar**) [!BADGE Beta]{type=Informative}**Partnerbezogene Anerkennung** für die Personalisierung von Erlebnissen vor Ort während des Besuchs und für die Offsite-Retargeting nach dem Besuch, ohne dass der Benutzer sich authentifiziert oder über einen früheren Verlauf mit Ihrer Marke verfügt.
* (**In Kürze verfügbar**) [!BADGE Beta]{type=Informative}**Erweiterte Aktivierung** Verwendung von Partner-IDs zum Veröffentlichen von Ökosystemen, die keine PII oder Hash-PII akzeptieren.