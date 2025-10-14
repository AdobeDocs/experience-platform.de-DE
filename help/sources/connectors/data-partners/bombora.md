---
title: Bombora Intent
description: Erfahren Sie mehr über die Bombora Intent-Quelle auf Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=de#rtcdp-editions newtab=true"
badgeB2P: label="B2P-Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=de#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 8a5fdcfcf503df1b9d5aa338ff530181a2d03b5d
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 10%

---

# [!DNL Bombora Intent]

[!DNL Bombora] ist eine umfassende Audience-Lösung, die auf B2B-Intent-Daten spezialisiert ist. [!DNL Bombora Intent] ist eine Adobe Experience Platform-Quelle, mit der Sie Ihr [!DNL Bombora]-Konto mit Experience Platform verbinden und Daten zu Ihrer Kontoabsicht integrieren können.

Mit der [!DNL Bombora Intent] Quelle können Sie Daten zum [!DNL Bombora's] des Unternehmens integrieren, um Konten zu identifizieren, die aktiv Ihre Produkte oder Services recherchieren. Verwenden Sie [!DNL Bombora], um marktinterne Konten zu priorisieren, um präzise Segmente zu erstellen und extrem zielgerichtete ABM-Kampagnen auszuführen, um sicherzustellen, dass sich Ihre Marketing-Maßnahmen auf die Konten konzentrieren, die am wahrscheinlichsten konvertieren. Darüber hinaus können Sie zielorientierte Strategien nutzen, um Anzeigenausgaben zu optimieren, die Interaktion zu steigern und den ROI zu maximieren.

In diesem Dokument finden Sie vorausgesetzte Informationen zur [!DNL Bombora].

## Anwendungsfälle {#use-cases}

Im Folgenden finden Sie Anwendungsbeispiele, die Sie auf die [!DNL Bombora] anwenden können.

### Integration von Demand-Side Platform (DSP)

Als B2B-Marketing-Experte können Sie in Real-Time CDP eine Account-Liste erstellen, Unternehmen identifizieren, die besonders auf Ihre Produkte achten, und diese Liste dann in [!DNL Bombora] aktivieren. Diese Liste lässt sich direkt in DSPs integrieren, sodass Sie zielgerichtete programmgesteuerte Anzeigenkampagnen mit [!DNL Bombora's] ausführen können. Dadurch wird sichergestellt, dass sich Ihre Werbeausgaben auf Unternehmen konzentrieren, die am ehesten konvertieren.

### Account-Based Marketing (ABM)-Funktionen

Als B2B-Marketing-Experte können Sie eine Account-Liste erstellen, die auf Absichtssignalen von Erst- und Drittanbietern basiert. Sie können diese Liste dann in [!DNL Bombora] aktivieren, wo die ABM-Funktionen es Ihnen ermöglichen, Mitarbeiter bei diesen Accounts gezielt anzusprechen, um sicherzustellen, dass Ihre Anzeigen Entscheidungsträger und nicht ein breites Publikum erreichen.

### Mehrkanal-ABM-Aktivierung

Als B2B-Marketing-Experte können Sie in Real-Time CDP eine Account-Liste erstellen, Unternehmen mit hohen Absichten identifizieren und aktivieren, [!DNL Bombora] zielgerichtete Kampagnen über mehrere Kanäle auszuführen. In bezahlten sozialen Medien können Sie auf Plattformen wie [!DNL Linkedin] und [!DNL Facebook] personalisierte Anzeigen für Fachleute auf Zielkonten schalten.

Mit nativen Anzeigenplattformen können Sie sicherstellen, dass Ihre Inhalte Entscheidungsträger in relevanten Kontexten erreichen. Sie können Kampagnen auch auf das erweiterte Fernsehen ausweiten und Anzeigen an Schlüsselkonten senden. Dieser Multi-Channel-Ansatz sorgt für konsistentes Messaging über Plattformen hinweg und maximiert Interaktions- und Konversionsraten.

## Voraussetzungen {#prerequisites}

Lesen Sie die folgenden Abschnitte für erforderliche Schritte, bevor Sie [!DNL Bombora] mit Experience Platform verbinden.

### Zulassungsliste von IP-Adressen

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Auf die Zulassungsliste setzen Weitere Informationen finden Sie [&#x200B; Seite &#x200B;](../../ip-address-allow-list.md)IP-Adresse“.

### Konfigurieren von Berechtigungen für Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Bombora]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/abac/ui/permissions.md).

### Namensbeschränkungen für Dateien und Verzeichnisse

Beachten Sie die folgenden Einschränkungen beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses:

* Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
* Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
* Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
* Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
* Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

### Sammeln erforderlicher Anmeldedaten

[!DNL Bombora] auf Experience Platform wird von [!DNL Google Cloud Storage] gehostet. Um Ihr [!DNL Bombora]-Konto erfolgreich zu authentifizieren, müssen Sie die entsprechenden Werte für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffsschlüssel-ID | Die Kennung des [!DNL Bombora] Zugriffsschlüssels. Dies ist eine 61-stellige alphanumerische Zeichenfolge, die zur Authentifizierung Ihres -Kontos bei Experience Platform erforderlich ist. |
| Geheimer Zugriffsschlüssel | Der [!DNL Bombora] geheime Zugriffsschlüssel. Dies ist eine mit Base-64 verschlüsselte Zeichenfolge mit 40 Zeichen, die zum Authentifizieren Ihres -Kontos bei Experience Platform erforderlich ist. |
| Behältername | Der [!DNL Bombora] Bucket, aus dem Daten abgerufen werden. |

Weitere Informationen zu diesen Anmeldeinformationen finden Sie im [[!DNL Google Cloud Storage] Handbuch zu HMAC-Schlüsseln](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Anweisungen zum Generieren Ihres eigenen Zugriffsschlüssels finden Sie im [Handbuch zu Voraussetzungen in der  [!DNL Google Cloud Storage] -Übersicht](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Schema [!DNL Bombora] {#schema}

In diesem Abschnitt finden Sie Informationen zum [!DNL Bombora] und zur Datenstruktur.

Das [!DNL Bombora]-Schema heißt **B2B Bombora Account Intent**. Es handelt sich dabei um die wöchentlichen Intent-Informationen (anonyme B2B-Käuferforschung und Inhaltsnutzung) zu bestimmten Accounts und Themen. Die Daten sind im Parquet-Format.

* Klasse - XDM-[!DNL Bombora Account Intent]
* Namespace - B2B-[!DNL Bombora Account Intent]
* Primäre Identität - `intentID`
* Beziehungen - B2B-Konto

| Feldname | Datentyp | Beschreibung |
|------------------------|-----------|----------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OBJEKT | Dieses Feld wird vom System für das Auditing des Quellsystems verwendet. |
| `_id` | STRING | Dieses Feld wird vom System als eindeutige Kennung verwendet. |
| `accountDomain` | STRING | Dieses Feld enthält die Konto-Domain. |
| `accountID` | STRING | Dieses Feld enthält die B2B-Konto-ID, mit der dieser Intent-Datensatz verknüpft ist. |
| `bomboraAccountName` | STRING | Dieses Feld enthält die Firmenkennung von Bombora. |
| `clusterID` | STRING | Dieses Feld enthält die Cluster-ID. |
| `clusterName` | STRING | Dieses Feld enthält den Cluster-Namen. |
| `compositeScore` | INTEGER | Dieses Feld enthält die zusammengesetzte Bewertung der Absicht. |
| `intentID` | STRING | Dieses Feld enthält einen vom System generierten eindeutigen Wert. |
| `partitionDate` | DATE | Dieses Feld enthält das Partitionsdatum. Dies erfolgt wöchentlich am Ende der Woche in `mm/dd/yyyy` Format. |
| `topicID` | STRING | Dieses Feld enthält die Absichtsthema-ID aus Bombora. |
| `topicName` | STRING | Dieses Feld enthält den Namen des Intent-Themas aus Bombora. |

{style="table-layout:auto"}

>[!TIP]
>
>Alle Änderungen am Schema werden Adobe im Voraus mitgeteilt. Um eine nahtlose Schemaentwicklung zu unterstützen, ist die Beibehaltung der Abwärtskompatibilität unerlässlich. Experience Platform erzwingt einen rein additiven Versionierungsansatz und stellt sicher, dass alle Aktualisierungen am Schema zerstörungsfrei sind. Dies bedeutet, dass umfassende Änderungen streng verboten sind und nur Änderungen zulässig sind, die das vorhandene Schema erweitern oder erweitern.

## Verbinden Ihres [!DNL Bombora]-Kontos mit Experience Platform über die Benutzeroberfläche

Nachdem Sie die erforderliche Einrichtung abgeschlossen haben, lesen Sie das Tutorial [Verbinden Ihres - [!DNL Bombora]  mit Experience Platform](../../tutorials/ui/create/data-partners/bombora.md), um Ihre Integration zu starten.

## Häufig gestellte Fragen {#faq}

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zur [!DNL Bombora].

### Muss ich über einen bestehenden Vertrag mit [!DNL Bombora] verfügen, um die Daten zur Kontoabsicht in Real-Time CDP B2B edition verwenden zu können?

+++Antwort

Ja, Sie müssen über einen aktiven Vertrag mit [!DNL Bombora] verfügen, um in Experience Platform und Real-Time CDP B2B edition auf deren Absichtsdaten zugreifen und diese verwenden zu können. Die Integration nutzt Ihre bestehende Vereinbarung mit dem [!DNL Bombora], um Account-Intent-Signale in Experience Platform und Real-Time CDP aufzunehmen und zu aktivieren.

+++

### Werden benutzerdefinierte Felder aus [!DNL Bombora] in dieser Integration unterstützt?

+++Antwort

Derzeit können Sie nur standardmäßige [!DNL Bombora] für die Aufnahme und Aktivierung verwenden. Um die Liste der unterstützten Felder anzuzeigen, lesen Sie das [[!DNL Bombora] Schema-Handbuch](#schema) für die Details zur Feldverfügbarkeit.

+++

### Kann ich Daten von [!DNL Bombora] auf Ad-hoc-Basis in Experience Platform aufnehmen?

+++Antwort

Ja, Sie können Daten aus [!DNL Bombora] ad hoc aufnehmen. Sie können einen neuen Datenfluss erstellen, um die Daten mit der neuesten Absicht aufzunehmen, sofern neue Daten aus [!DNL Bombora] vorhanden sind. Sie können jedoch jeweils nur einen aktiven Datenfluss haben. Stellen Sie daher sicher, dass Sie den vorhandenen Datenfluss löschen, bevor Sie einen neuen erstellen.

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

### Welches Feld wird verwendet, um Konten von [!DNL Bombora] mit Experience Platform abzugleichen?

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

Absichtsdaten können in &quot;[-Zielgruppen“ verwendet werden, &#x200B;](../../../segmentation/types/account-audiences.md) Targeting, Segmentierung und Personalisierung zu verbessern. Durch die Nutzung von Intent-Signalen können Unternehmen Accounts identifizieren und mit ihnen interagieren, die ein hohes Interesse an bestimmten Themen zeigen, und so Marketing- und Verkaufsaktivitäten optimieren.

+++
