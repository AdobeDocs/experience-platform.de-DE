---
title: Demandbase Intent
description: Erfahren Sie mehr über die Demandbase Intent-Quelle in Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: e223ea754a250956e65c3f526119a3ebd7bb067c
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 11%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] ist eine Account-basierte Marketing-Plattform, die Sie für B2B-Verkäufe und -Marketing-Erfolg verwenden können. [!DNL Demandbase Intent] ist eine Adobe Experience Platform-Quelle, mit der Sie Ihr [!DNL Demandbase]-Konto mit Experience Platform verbinden und Daten zu Ihrer Kontoabsicht integrieren können.

Mit der [!DNL Demandbase] Quelle können Sie Konten mit hohem Zinsniveau basierend auf Echtzeit-Interaktionen identifizieren. Indem Sie die Signale mit dem stärksten Intent priorisieren, können Sie präzise Segmente erstellen und extrem zielgerichtete Kampagnen bereitstellen, um sicherzustellen, dass sich Ihre Marketing-Maßnahmen auf die Konten konzentrieren, die am wahrscheinlichsten konvertiert werden. Die Aktivierung zielgerichteter Strategien ermöglicht die Optimierung der Werbeausgaben, ein höheres Engagement und einen höheren ROI.

In diesem Dokument finden Sie vorausgesetzte Informationen zur [!DNL Demandbase].

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte für erforderliche Schritte, bevor Sie [!DNL Demandbase] mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Auf die Zulassungsliste setzen Weitere Informationen finden Sie [ Seite ](../../ip-address-allow-list.md)IP-Adresse“.

### Konfigurieren von Berechtigungen für Experience Platform

Für Ihr Konto müssen sowohl **[!UICONTROL View Sources]**- als auch **[!UICONTROL Manage Sources]** aktiviert sein, um Ihr [!DNL Demandbase] mit Experience Platform verbinden zu können. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/abac/ui/permissions.md).

### Namensbeschränkungen für Dateien und Verzeichnisse

Beachten Sie die folgenden Einschränkungen beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses:

* Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
* Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
* Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
* Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
* Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

### Sammeln erforderlicher Anmeldedaten

[!DNL Demandbase] auf Experience Platform wird von [!DNL Google Cloud Storage] gehostet. Um Ihr [!DNL Demandbase]-Konto erfolgreich zu authentifizieren, müssen Sie die entsprechenden Werte für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffsschlüssel-ID | Die Kennung des [!DNL Demandbase] Zugriffsschlüssels. Dies ist eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres -Kontos bei Experience Platform erforderlich ist. |
| Geheimer Zugriffsschlüssel | Der [!DNL Demandbase] geheime Zugriffsschlüssel. Dies ist eine mit Base-64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihres -Kontos bei Experience Platform erforderlich ist. |
| Behältername | Der [!DNL Demandbase] Bucket, aus dem Daten abgerufen werden. |
| Ordnerpfad | Der Pfad zum Ordner, auf den Sie Zugriff gewähren möchten. |

Weitere Informationen zu diesen Anmeldeinformationen finden Sie im [[!DNL Google Cloud Storage] Handbuch zu HMAC-Schlüsseln](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihres eigenen Zugriffsschlüssels finden Sie im [Handbuch zu Voraussetzungen in der  [!DNL Google Cloud Storage] -Übersicht](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Schema [!DNL Demandbase]

>[!IMPORTANT]
>
>Stellen Sie beim Erstellen eines Absichtsschemas für ein B2B-Demandbase-Konto in der Experience Platform-Benutzeroberfläche sicher, dass Sie die Profilaufnahme für das Schema aktivieren. Weitere Informationen finden sich im Handbuch unter [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../../xdm/ui/resources/schemas.md).

In diesem Abschnitt finden Sie Informationen zum [!DNL Demandbase] und zur Datenstruktur.

Das [!DNL Demandbase]-Schema heißt &quot;**B2B Demandbase Account Intent**. Es handelt sich dabei um die wöchentlichen Intent-Informationen (anonyme B2B-Käuferforschung und Inhaltsnutzung) zu bestimmten Konten und Schlüsselwörtern. Die Daten sind im Parquet-Format.

* Klasse - XDM-[!DNL Demandbase Account Intent]
* Namespace - B2B-[!DNL Demandbase Account Intent]
* Primäre Identität - `intentID`
* Beziehungen - B2B-Konto

| Feldname | Datentyp | Beschreibung |
|--------------------------|-----------|-------------------------------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJEKT | Dieses Feld enthält Systemüberwachungsinformationen aus der externen Quelle. |
| `_id` | STRING | Dies ist die eindeutige Systemkennung für den Datensatz. |
| `accountDomain` | STRING | Dieses Feld enthält die Konto-Domain. |
| `accountID` | STRING | Dies ist die B2B-Konto-ID, mit der dieser Absichtsdatensatz verknüpft ist. |
| `demandbaseAccountID` | STRING | Dies ist die Unternehmens-ID in [!DNL Demandbase]. |
| `durationType` | STRING | Dieses Feld gibt den Typ des Gültigkeitszeitraums für die Absicht an, z. B. „Woche“. |
| `endDate` | DATE | Dies ist das Enddatum des Gültigkeitszeitraums der Absicht. |
| `intentID` | STRING | Dies ist ein vom System generierter eindeutiger Wert für den Absichtsdatensatz. |
| `intentStrength` | STRING | Dieses Feld gibt den Typ des Gültigkeitszeitraums für die Absicht an, z. B. „TAG“, „WOCHE“ oder „MONAT“. |
| `isTrending` | BOOLEAN | Dieses Feld gibt an, ob das Keyword im Trend liegt, wobei die möglichen Werte Niedrig, Medium oder Hoch sind. |
| `keyword` | STRING | Dieses Feld enthält das Keyword oder die Phrase, die eine Absicht von [!DNL Demandbase] angibt. |
| `keywordSetID` | STRING | Dies ist die Kennung für den Schlüsselwortsatz. |
| `keywordSetName` | STRING | Dies ist der Name des Schlüsselwortsatzes. |
| `numTrendingDays` | INTEGER | Dieses Feld gibt die Anzahl der Tage an, nach denen das Keyword einen Trend aufweist. |
| `partitionDate` | DATE | Dies ist das Partitionsdatum für den Datensatz. |
| `peopleResearchingCount` | INTEGER | Dieses Feld gibt die Anzahl der Personen an, die das Keyword durchsuchen. |
| `startDate` | DATE | Dies ist das Startdatum des Gültigkeitszeitraums der Absicht. |
| `trendingScore` | INTEGER | Dieses Feld enthält den Trendwert für das Keyword. |

{style="table-layout:auto"}

>[!TIP]
>
>Alle Änderungen am Schema werden Adobe im Voraus mitgeteilt. Um eine nahtlose Schemaentwicklung zu unterstützen, ist die Beibehaltung der Abwärtskompatibilität unerlässlich. Experience Platform erzwingt einen rein additiven Versionierungsansatz und stellt sicher, dass alle Aktualisierungen am Schema zerstörungsfrei sind. Dies bedeutet, dass umfassende Änderungen streng verboten sind und nur Änderungen zulässig sind, die das vorhandene Schema erweitern oder erweitern.

## Verbinden Ihres [!DNL Demandbase]-Kontos mit Experience Platform über die Benutzeroberfläche

Nachdem Sie die erforderliche Einrichtung abgeschlossen haben, lesen Sie das Tutorial [Verbinden Ihres - [!DNL Demandbase]  mit Experience Platform](../../tutorials/ui/create/data-partners/demandbase.md), um Ihre Integration zu starten.

## Häufig gestellte Fragen {#faq}

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zur [!DNL Demandbase].

### Muss ich über einen bestehenden Vertrag mit [!DNL Demandbase] verfügen, um die Daten zur Kontoabsicht in Real-Time CDP B2B edition verwenden zu können?

+++Antwort

Ja, Sie müssen über einen aktiven Vertrag mit [!DNL Demandbase] verfügen, um in Experience Platform und Real-Time CDP B2B edition auf deren Absichtsdaten zugreifen und diese verwenden zu können. Die Integration nutzt Ihre bestehende Vereinbarung mit dem [!DNL Demandbase], um Account-Intent-Signale in Experience Platform und Real-Time CDP aufzunehmen und zu aktivieren.

+++

### Werden benutzerdefinierte Felder aus [!DNL Demandbase] in dieser Integration unterstützt?

+++Antwort

Derzeit können Sie nur standardmäßige [!DNL Demandbase] für die Aufnahme und Aktivierung verwenden. Um die Liste der unterstützten Felder anzuzeigen, lesen Sie das [[!DNL Demandbase] Schema-Handbuch](#schema) für die Details zur Feldverfügbarkeit.

+++

### Kann ich Daten von [!DNL Demandbase] auf Ad-hoc-Basis in Experience Platform aufnehmen?

+++Antwort

Ja, Sie können Daten aus [!DNL Demandbase] ad hoc aufnehmen. Sie können einen neuen Datenfluss erstellen, um die Daten mit der neuesten Absicht aufzunehmen, sofern neue Daten aus [!DNL Demandbase] vorhanden sind. Sie können jedoch jeweils nur einen aktiven Datenfluss haben. Stellen Sie daher sicher, dass Sie den vorhandenen Datenfluss löschen, bevor Sie einen neuen erstellen.

+++

### Was ist der Validierungsprozess für Intent-Daten und wie kann ich überprüfen, welche Intent-Daten mit einem bestimmten Konto verknüpft sind?

+++Antwort

Um Absichtsdaten zu validieren und zu ermitteln, welche Absichtssignale mit bestimmten Konten verknüpft sind, verwenden Sie [Adobe Experience Platform Query Service](../../../query-service/home.md) von AccountID.

+++

### Wie kann ich eine Absicht für ein bestimmtes Unternehmen nachschlagen?

+++Antwort

Führen Sie eine SQL-Abfrage in [Abfrage-Service](../../../query-service/home.md) aus, um mithilfe des Firmennamens oder der Konto-ID nach Absichtsdaten zu suchen. Um alle Absichtsdaten für ein bestimmtes Unternehmen anzuzeigen, können Sie eine SQL-Abfrage im Abfrage-Service mit dem Firmennamen oder der Konto-ID ausführen, um alle zugehörigen Absichtssignale abzurufen.

+++


### Ich habe ein Problem mit dem Prozess zum Abgleichen von Konten in Experience Platform gefunden. Was soll ich tun?

+++Antwort

Die Lösung hängt von der spezifischen Anfrage ab:

* **Falsche oder fehlende Unternehmens-Domain in Experience Platform**: Wenn das Problem von einem falschen Wert für die Unternehmens-Domain in den Kontodaten herrührt, aktualisieren Sie das Feld „Unternehmens-Domain“ in Experience Platform, um eine genaue Zuordnung sicherzustellen.
* **Falsche Feldzuordnung im Datenfluss**: Wenn das Problem auf einen falschen Feldpfad für die Unternehmens-Domain im Datenfluss zurückzuführen ist, aktualisieren Sie die Datenflusskonfiguration, um auf den richtigen Feldpfad zu verweisen.

+++

### Wie lösche ich Absichtsdaten in Experience Platform?

+++Antwort

Sie müssen [Datensatz löschen](../../../catalog/datasets/user-guide.md#delete-a-dataset) um Absichtsdaten in Experience Platform löschen zu können.

+++

### Welches Feld wird verwendet, um Konten von [!DNL Demandbase] mit Experience Platform abzugleichen?

+++Antwort

Das Feld `accountOrganization.domain` wird für den Abgleich von Konten verwendet. Wenn Ihr Unternehmen zum Speichern des Website-Namens ein anderes benutzerdefiniertes Feld verwendet, stellen Sie sicher, dass Sie den richtigen Feldpfad für eine genaue Zuordnung angeben.

+++

### Was passiert, wenn eine Unternehmens-Domain in Experience Platform aktualisiert wird?

+++Antwort

Wenn eine Unternehmens-Domain aktualisiert wird, wird der neue Domain-Wert bei der nächsten Datenflussausführung angewendet. Dadurch wird Folgendes sichergestellt:

* Die zukünftige beabsichtigte Datenaufnahme verwendet die aktualisierte Domain für die Kontozuordnung.
* Alle zuvor nicht übereinstimmenden Absichtssignale können jetzt korrekt mit dem beabsichtigten Konto übereinstimmen.
* An früheren aufgenommenen Daten werden keine rückwirkenden Änderungen vorgenommen. Neue und eingehende Daten spiegeln die Aktualisierung wider.

+++

### Wie funktioniert der Domain-Abgleich?

+++Antwort

Der Domain-Abgleich in Experience Platform basiert auf einer exakten Übereinstimmung des bereinigten Domain-Feldwerts. Experience Platform entfernt automatisch Präfixe (z. B. https:/<span>/www.) und behält die Domain auf oberster Ebene (z. B. adobe.com) bei. Für den Abgleich ist ein exakter Domain-Wert erforderlich, ohne Unterstützung für Fuzzy-Abgleich oder Subdomains.

+++

### Wo kann ich Absichtsdaten verwenden?

+++Antwort

Absichtsdaten können in &quot;[-Zielgruppen“ verwendet werden, ](../../../segmentation/types/account-audiences.md) Targeting, Segmentierung und Personalisierung zu verbessern. Durch die Nutzung von Absichtssignalen können Unternehmen Konten identifizieren und mit ihnen interagieren, die ein hohes Interesse an bestimmten Themen zeigen, und so Marketing- und Verkaufsaktivitäten optimieren

+++
