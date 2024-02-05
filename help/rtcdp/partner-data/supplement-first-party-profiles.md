---
title: Ergänzen von Erstanbieterprofilen mit von Partnern bereitgestellten Attributen
description: Erfahren Sie, wie Sie Erstanbieterprofile mit Attributen vertrauenswürdiger Datenpartner ergänzen, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: 9737508bd8435f4edf0e60a3559c1b4352ccb29f
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 79%

---

# Ergänzen von Erstanbieterprofilen mit von Partnern bereitgestellten Attributen

>[!AVAILABILITY]
>
>* Diese Funktion steht Kunden zur Verfügung, die Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate lizenziert haben. Weitere Informationen zu diesen Paketen finden Sie in den [Produktbeschreibungen](https://helpx.adobe.com/de/legal/product-descriptions.html) und erhalten Sie von Ihrem Adobe-Support-Team.

Ergänzen Sie Erstanbieterprofile mit Attributen von vertrauenswürdigen Datenpartnern, um Ihre Datengrundlage zu verbessern, neue Einblicke in Ihre Kundenbasis zu gewinnen und eine bessere Zielgruppenoptimierung zu erzielen.

![Anreichern von Profilen mit von Partnern bereitgestellten Attributen – allgemeine Übersicht über Anwendungsfälle.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Warum sollten Sie diesen Anwendungsfall beachten? {#why-this-use-case}

Die meisten Marken, selbst diejenigen, die reich an Erstanbieterdaten sind, können von der Optimierung ihrer Daten und einem differenzierteren Verständnis von Kunden, deren Verhalten, Mustern und Präferenzen profitieren.

Adobe Real-time Customer Data Platform kann Marken dabei helfen, ihre Erstanbieterdaten mit wertvollen Einblicken, Kennungen und Attributen eines oder mehrerer vertrauenswürdiger Partner verantwortungsbewusst zu ergänzen.

Adobe versteht, dass es keinen einheitlichen Ansatz gibt und eine nahtlose Interoperabilität mit Daten- und Identitätspartnern ermöglicht, um eine individuelle und durchdachte Interaktion in allen Phasen des Kundenlebenszyklus zu fördern. Diese Funktionen werden durch ein vertrauenswürdiges Data Governance-Framework unterstützt, das eine differenzierte Kontrolle darüber ermöglicht, wo und wie Partnerdaten verwendet werden. Sie können beispielsweise von Partnern bereitgestellte Einblicke für die Segmentierung, aber nicht für die Personalisierung verwenden.

Führen Sie beispielsweise die in diesem Anwendungsbeispiel beschriebenen Schritte aus, wenn Sie Ihre Kundendatensätze mit demografischen und Intent-Signalen anreichern möchten.

## Voraussetzungen und Planung

Wenn Sie Ihre eigenen Erstanbieterprofile mit Attributen von Datenpartnern ergänzen möchten, sollten Sie die folgenden Details zur Dateneranreicherungsschleife mit dem Datenpartner erörtern und besprechen:

* Denken Sie über den Speicherort nach, an dem die Zielgruppenliste aus Real-Time CDP exportiert und für den Datenanbieter freigegeben wird. Dieser Speicherort muss Dateiexporte unterstützen.
* Welche Kennungen erwartet der Datenanbieter, damit Bezug auf zusätzliche Attribute genommen werden kann?
* Wie wird die Datei mit den von Partnern bereitgestellten Attributen wieder in Real-Time CDP aufgenommen? Beispielsweise können die Dateien über Cloud-Speicher-Quell-Connectoren wie [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) oder [SFTP](/help/sources/connectors/cloud-storage/sftp.md) aufgenommen werden.
* Wie häufig werden von Partnern bereitgestellte Attribute voraussichtlich wieder nach Real-Time CDP zurückgeholt und aktualisiert?

>[!WARNING]
>
>Die zusätzlichen von den Partnern bereitgestellten Attribute, die in Real-Time CDP aufgenommen werden, wirken sich auf Ihren *durchschnittlichen Profilumfang* aus. Weitere Informationen zum Profilumfang finden Sie in der [Real-time Customer Data Platform-Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html).

## Videoeinführung {#video-walkthrough}

Sehen Sie sich das Video-Tutorial unten an, um sich einen Überblick darüber zu verschaffen, wie Erstanbieter-Zielgruppen mit von Partnern bereitgestellten Attributen ergänzt werden:

>[!VIDEO](https://video.tv.adobe.com/v/3423075/?learn=on)

## Erreichen des Anwendungsfalls: Allgemeine Übersicht {#achieve-the-use-case-high-level}

![Anreichern von Profilen mit von Partnern bereitgestellten Attributen – allgemeine Übersicht über Anwendungsfälle.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Als **Kundin oder Kunde** lizenzieren Sie Attribute vom **Datenpartner**.
2. Als **Kundin oder Kunde** erweitern Sie Ihre Profildaten und Ihr Governance-Modell für vom **Partner** bereitgestellte Attribute.
3. Als **Kundin oder Kunde** integrieren Sie die Zielgruppen, die mithilfe des Datenpartners angereichert werden sollen. Im Allgemeinen handelt es sich bei diesen Zielgruppen um verschlüsselte Eingabekennungen wie Elemente personenbezogener Daten (Personally Identifiable Information, PII). Beispiele hierfür sind die E-Mail-Adresse, der Name oder die Adresse.
4. Der **Partner** hängt lizenzierte Attribute für die Profile an, bei denen ein Abgleich möglich ist. Optional kann eine [Partner-ID](/help/identity-service/features/namespaces.md) in den partnerbezogenen ID-Namespace eingeschlossen und darin aufgenommen werden.
5. Als **Kundin oder Kunde** laden Sie Attribute vom Datenpartner in Kundenprofile in Real-Time CDP.

## Erreichen des Anwendungsfalls: Schrittweise Anweisungen {#step-by-step-instructions}

Lesen Sie die folgenden Abschnitte, die Links zu weiterführender Dokumentation enthalten, um die einzelnen Schritte in der oben stehenden allgemeinen Übersicht auszuführen.

### Lizenzattribute vom Partner {#license-attributes-from-partner}

Dieser Schritt wird im Abschnitt [Voraussetzungen](#prerequisites-and-planning) beschrieben. Adobe geht dabei davon aus, dass Sie über die richtigen vertraglichen Vereinbarungen mit vertrauenswürdigen Datenanbietern verfügen, um Ihre Erstanbieterprofile zu ergänzen.

### Erweitern Sie Ihre Profildaten und Ihr Governance-Modell für von Partnern bereitgestellte Attribute. {#extend-governance-model}

An diesem Punkt erweitern Sie Ihr Daten-Management-Framework in Real-Time CDP für von Partnern bereitgestellte Attribute.

Sie haben die Möglichkeit, ein neues Schema der Klasse **[!UICONTROL XDM Individual Profile – XDM-Profil für Einzelpersonen]** zu erstellen oder ein vorhandenes Schema desselben Typs um von Partnern bereitgestellte Attribute zu erweitern. Adobe empfiehlt ausdrücklich, ein neues Schema mit neuen Feldgruppen zu erstellen, die die zusätzlichen Attribute des Datenanbieters am besten darstellen. Dadurch wird sichergestellt, dass Ihre Datenschemata einwandfrei sind und sich unabhängig voneinander entwickeln können.

Um von Partnern bereitgestellte Attribute in ein Schema einzuschließen, können Sie entweder eine neue Feldgruppe mit den erwarteten Attributen erstellen oder eine der von Adobe bereitgestellten vorkonfigurierten Feldgruppen verwenden.

Weitere Informationen finden Sie auf den folgenden Dokumentationsseiten:

* [Grundlagen der Schemakomposition](/help/xdm/schema/composition.md)
* [Klasse [!UICONTROL XDM Individual Profile – XDM-Profil für Einzelpersonen] – Übersicht](/help/xdm/classes/individual-profile.md)
* [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](/help/xdm/ui/resources/schemas.md)
* [Erstellen und Bearbeiten von Schemafeldgruppen in der Benutzeroberfläche](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Überlegen Sie in diesem Schritt außerdem, wie sich Ihr Data-Governance-Modell ändert, wenn Sie Ihre Daten-Management-Strategie erweitern und vom Partner bereitgestellte Drittanbieterdaten einschließen. Machen Sie sich mit den Hinweisen in den folgenden Links zur Dokumentation vertraut:

* (**In Kürze verfügbar**) Halten Sie Drittanbieterdaten in einem separaten Datensatz, damit Integrationen auf einfache Weise gelöscht und rückgängig gemacht werden können.
* (**In Kürze verfügbar**) Verwenden Sie die Funktion [Datensatzgültigkeit](/help/hygiene/ui/dataset-expiration.md) für den Datensatz bei Kundinnen und Kunden, die das Datenhygiene-Add-on erworben haben.
* (**In Kürze verfügbar**) Gehen Sie beim Erstellen abgeleiteter Datensätze, die Daten von Drittanbietern abrufen, vorsichtig vor. Denn einmal vermischt, besteht die einzige Lösung zum Entfernen der Daten von Drittanbietern darin, den gesamten abgeleiteten Datensatz zu löschen.

>[!TIP]
>
>Wenn Sie Ihre Kundenprofile mit einer personenbasierten Kennung des Datenanbieters ergänzen möchten, können Sie einen neuen Identitätstyp vom Typ **[[!UICONTROL Partner-ID]](/help/identity-service/features/namespaces.md)** erstellen.
>
>Weitere Informationen zur Partner-ID finden Sie im Abschnitt [Identitätstypen](/help/identity-service/features/namespaces.md).
>Lesen Sie die Anweisungen zum [Definieren von Identitätsfeldern](/help/xdm/ui/fields/identity.md) in der Experience Platform-Benutzeroberfläche.

### Exportieren von anzureichernden Zielgruppen bei verschlüsselten oder gehashten personenbezogenen Daten (PII) {#export-audiences}

Exportieren Sie die Zielgruppen, die vom Partner angereichert werden sollen. Verwenden Sie die von Real-Time CDP bereitgestellten Cloud-Speicher-Ziele, z. B. Amazon S3 oder SFTP. Weitere Informationen zum Abschließen dieses Schrittes finden Sie auf den folgenden Dokumentationsseiten:

* Dokumentationsseite für [Amazon S3-Ziele](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* Dokumentationsseite für [SFTP-Ziele](/help/destinations/catalog/cloud-storage/sftp.md)
* [Verbinden mit einem Ziel](/help/destinations/ui/connect-destination.md)
* [Exportieren von Daten in ein Cloud-Speicher-Ziel](/help/destinations/ui/activate-batch-profile-destinations.md)

### Ihr Datenpartner hängt lizenzierte Attribute für die Profile an, bei denen ein Abgleich möglich ist {#partner-appends-attributes}

In diesem Schritt hängt Ihr Datenpartner lizenzierte Attribute für die exportierte Zielgruppe an. Die Ausgabe ist im Allgemeinen als Flatfile verfügbar, die wieder in Real-Time CDP aufgenommen werden kann. Weitere Informationen finden Sie unter [Aufnehmen von Dateien in Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP hängt angereicherte Attribute an das Kundenprofil an {#ingest-data}

Nun müssen Sie Daten vom Partner über einen Quell-Connector aufnehmen, um die angereicherten Daten wieder nach Real-Time CDP zurückzuholen und Ihre Profile mit den vom Partner bereitgestellten Daten zu ergänzen.

Zu diesem Zweck werden etwa diese Quell-Connectoren empfohlen:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Einschränkungen und Fehlerbehebung {#limitations-and-troubleshooting}

Beachten Sie die folgenden Einschränkungen, wenn Sie sich den auf dieser Seite beschriebenen Anwendungsfall ansehen:

* Wenn Sie sich für die Verwendung von Partner-IDs entscheiden, beachten Sie, dass diese IDs beim Erstellen Ihres [Identitätsdiagramms](/help/identity-service/features/identity-graph-viewer.md) nicht verwendet werden.

## Andere durch Partnerdatenunterstützung ermöglichte Anwendungsfälle {#other-use-cases}

Erkunden Sie weitere Anwendungsfälle, die durch die Unterstützung von Partnerdaten in Real-Time CDP ermöglicht werden:

* Verwenden Sie die Unterstützung von Drittanbieterdaten in Real-Time CDP, damit Sie [Ihre Profilbasis mit potenziellen Profilen von Datenpartnern erweitern und mit ihnen interagieren können, um neue Kundinnen und Kunden zu gewinnen oder zu erreichen](/help/rtcdp/partner-data/prospecting.md).
* [Personalisieren von Onsite-Erlebnissen für unbekannte Besucher mithilfe der von Partnern unterstützten Besuchererkennung](/help/rtcdp/partner-data/onsite-personalization.md) während des Besuchs, ohne dass sich der Benutzer authentifiziert oder über einen früheren Verlauf mit Ihrer Marke verfügt.
* [Erweiterte Aktivierung von Interessenten- und Interessenten-Zielgruppen](/help/destinations/ui/activate-prospect-audiences.md) , um Ziele auszuwählen.
