---
keywords: Experience Platform;Startseite;beliebte Themen;segmentierung;Segmentierung;Segment Match;segment match
solution: Experience Platform
title: Übersicht zu Segment Match
description: Segment Match ist ein Service zur Segmentfreigabe in Adobe Experience Platform, mit dem zwei oder mehr Platform-Benutzende Segmentdaten auf sichere, geregelte und datenschutzsensible Weise austauschen können.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: b82bbdf7957e5a8d331d61f02293efdaf878971c
workflow-type: tm+mt
source-wordcount: '1968'
ht-degree: 98%

---

# [!DNL Segment Match] – Übersicht

Adobe Experience Platform Segment Match ist ein Service zur Segmentfreigabe, mit dem zwei oder mehr Platform-Benutzende Segmentdaten auf sichere, geregelte und datenschutzsensible Weise austauschen können. [!DNL Segment Match] verwendet Platform-Datenschutzstandards und persönliche IDs wie Hash-E-Mails, Hash-Telefonnummern und Geräte-IDs wie IDFAs und GAIDs.

Mit [!DNL Segment Match] können Sie:

* die Identitätsüberschneidung verwalten,
* Schätzungen vor der Freigabe anzeigen,
* Datennutzungs-Kennzeichnungen anwenden, um zu steuern, ob Daten für Partner freigegeben werden können,
* nach der Veröffentlichung eines Feeds das freigegebene Zielgruppen-Lebenszyklus-Management pflegen und den dynamischen Datenaustausch durch Funktionen zum Hinzufügen, Löschen und Aufheben der Freigabe fortsetzen.

[!DNL Segment Match] verwendet einen Identitätsüberschneidungsprozess, um sicherzustellen, dass die Segmentfreigabe auf sichere und datenschutzorientierte Weise erfolgt. Eine **Identität mit Überschneidung** ist eine Identität, die sowohl in Ihrem Segment als auch im Segment Ihres ausgewählten Partners eine Übereinstimmung enthält. Vor der Freigabe eines Segments zwischen Absendenden und Empfangenden wird im Prozess zur Identitätsüberschneidung geprüft, ob Überschneidungen bei Namespaces und Einverständnisprüfungen zwischen Absendenden und Empfangenden vorhanden sind. Beide Überschneidungsprüfungen müssen bestanden werden, damit ein Segment freigegeben werden kann.

In den folgenden Abschnitten finden Sie weitere Informationen zu [!DNL Segment Match], einschließlich Details zum Setup und seinem End-to-End-Workflow.

## Einrichten

In den folgenden Abschnitten wird beschrieben, wie Sie [!DNL Segment Match] einrichten und konfigurieren:

### Einrichten von Identitätsdaten und Namespaces {#namespaces}

Um [!DNL Segment Match] zu verwenden, müssen Sie als Erstes sicherstellen, dass Sie Daten mit den unterstützten Identity-Namespaces aufnehmen.

Identity-Namespaces sind eine Komponente von [Adobe Experience Platform Identity Service](../../../identity-service/home.md). Jede Kundenidentität enthält einen zugehörigen Namespace, der den Kontext der Identität angibt. Ein Namespace unterscheidet beispielsweise den Wert von „name<span>@email.com“ als E-Mail-Adresse oder „443522“ als numerische CRM-ID.

Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. Bei der Zuordnung von Datensatzdaten zu Profilfragmenten (z. B. beim Zusammenführen von Profildaten durch das [!DNL Real-Time Customer Profile]) müssen sowohl Identitätswert als auch Namespace übereinstimmen.

Im Kontext von [!DNL Segment Match] werden Namespaces bei der Datenfreigabe im Überschneidungsprozess verwendet.

Folgende Namespaces werden unterstützt:

| Namespace | Beschreibung |
| --------- | ----------- |
| E-Mails (SHA256, in Kleinbuchstaben) | Ein Namespace für vorab gehashte E-Mail-Adressen. In diesem Namespace angegebene Werte werden vor dem Hashing mit SHA256 in Kleinbuchstaben umgewandelt. Vor der Normalisierung einer E-Mail-Adresse müssen vorangestellte und nachfolgende Leerzeichen abgeschnitten werden. Diese Einstellung kann nachträglich nicht mehr geändert werden. Platform bietet zwei Methoden zur Unterstützung von Hashing bei der Datenerfassung: durch [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) und [Datenvorbereitung](../../../data-prep/functions.md#hashing). |
| Phone (SHA256_E.164) | Ein Namespace, der unformatierte Telefonnummern darstellt, die mit dem SHA256- und E.164-Format gehasht werden müssen. |
| ECID | Ein Namespace, der einen Experience Cloud ID (ECID)-Wert darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weiterführende Informationen dazu finden Sie in der [ECID-Übersicht](../../../identity-service/features/ecid.md). |
| Apple IDFA (ID für Advertiser) | Ein Namespace, der die Apple ID für Advertiser darstellt. Weiteführende Informationen finden Sie im folgenden Dokument zu [Interessensbasierten Anzeigen](https://support.apple.com/de-de/HT202074). |
| Google Ad-ID | Ein Namespace, der eine Google Advertising ID darstellt. Weiterführende Informationen finden Sie im folgenden Dokument zu [Google Advertising IDs](https://support.google.com/googleplay/android-developer/answer/6048248?hl=de). |

### Einrichten der Einverständniskonfiguration

Sie müssen eine Einverständniskonfiguration bereitstellen und deren Standardwert auf `opt-in` oder `opt-out` festlegen, um eine Einverständnisprüfung durchzuführen.

Die Opt-in- und Opt-out-Einverständnisprüfung bestimmt, ob Sie basierend auf dem Einverständnis, Benutzerdaten standardmäßig freigeben dürfen. Wenn die Einverständniskonfiguration standardmäßig auf `opt-out` festgelegt ist, können Benutzerdaten freigegeben werden, es sei denn, Benutzende schließen die Freigabe ausdrücklich aus. Wenn der Standardwert auf `opt-in` festgelegt ist, können Benutzerdaten nicht freigegeben werden, es sei denn, Benutzende lassen dies ausdrücklich zu.

Die standardmäßige Einverständniskonfiguration für [!DNL Segment Match] ist auf `opt-out` festgelegt. Um ein Opt-in-Modell für Ihre Daten zu erzwingen, senden Sie eine E-Mail-Anfrage an das Adobe-Accountteam.

Weitere Informationen über `share` -Attribut, das zum Festlegen des Zustimmungswerts für die Datenweitergabe verwendet wird, finden Sie in der folgenden Dokumentation unter [Feldergruppe &quot;Datenschutz und Einverständnis&quot;](../../../xdm/field-groups/profile/consents.md). Informationen zu der spezifischen Feldergruppe, mit der das Verbrauchereinverständnis zur Sammlung und Verwendung von Daten im Zusammenhang mit Datenschutz-, Personalisierungs- und Marketing-Voreinstellungen erfasst wird, finden Sie im folgenden [GitHub-Beispiel zu den Voreinstellungen für das Einverständnis für Datenschutz, Personalisierung und Marketing](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Konfigurieren von Datennutzungskennzeichnungen

Als letzte Voraussetzung müssen Sie eine neue Datennutzungskennzeichnung konfigurieren, um die Datenfreigabe zu verhindern. Mithilfe von Datennutzungskennzeichnungen können Sie verwalten, welche Daten über [!DNL Segment Match] freigegeben werden dürfen.

Mit Datennutzungsbeschriftungen können Sie Datensätze anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in Experience Platform oder ab dem Zeitpunkt ihrer Nutzbarkeit in Platform mit einer Beschriftung zu versehen.

[!DNL Segment Match] verwendet die C11-Kennzeichnung, eine [!DNL Segment Match]-spezifische Kennzeichnung von Verträgen, die Sie manuell zu allen Datensätzen oder Attributen hinzufügen können, um sicherzustellen, dass sie aus dem [!DNL Segment Match]-Partnerfreigabeprozess ausgeschlossen werden. Die Bezeichnung „C11“ bezeichnet Daten, die nicht in [!DNL Segment Match]-Prozessen verwendet werden sollten. Nachdem Sie ermittelt haben, welche Datensätze und/oder Felder Sie aus [!DNL Segment Match] ausschließen möchten, und die C11-Kennzeichnung entsprechend hinzugefügt haben, wird die Kennzeichnung automatisch vom [!DNL Segment Match]-Workflow durchgesetzt. [!DNL Segment Match] aktiviert automatisch die Kernrichtlinie [!UICONTROL Datenfreigabe beschränken]. Spezifische Anweisungen zum Anwenden von Datennutzungskennzeichnungen auf Datensätze finden Sie im Tutorial zum [Verwalten von Datennutzungskennzeichnungen in der Benutzeroberfläche](../../../data-governance/labels/user-guide.md).

Eine Liste der Datennutzungskennzeichnungen und ihrer Definitionen finden Sie im [Glossar zu Datennutzungskennzeichnungen](../../../data-governance/labels/reference.md). Informationen zu Datennutzungsrichtlinien finden Sie in der [Übersicht zu Datennutzungsrichtlinien](../../../data-governance/policies/overview.md).

### Grundlegendes zu [!DNL Segment Match]-Berechtigungen

Es gibt zwei Berechtigungen, die mit [!DNL Segment Match] verknüpft sind:

| Berechtigung | Beschreibung |
| --- | --- |
| Verbindungen für Zielgruppenfreigaben verwalten | Mit dieser Berechtigung können Sie den Partner-Handshake-Prozess abschließen, der zwei Organisationen verbindet, um [!DNL Segment Match]-Flüsse zu aktivieren. |
| Zielgruppenfreigaben verwalten | Mit dieser Berechtigung können Sie Feeds (das für [!DNL Segment Match] verwendete Datenpaket) für aktive Partner (Partner, die vom Administrationspersonal mit Zugriff auf **[!UICONTROL Verbindungen für Zielgruppenfreigaben]** verbunden wurden) erstellen, bearbeiten und veröffentlichen. |

Weiterführende Informationen zu Zugriffssteuerung und Berechtigungen finden Sie in der [Übersicht zur Zugriffssteuerung](../../../access-control/home.md).

## [!DNL Segment Match]-End-to-End-Workflow

Nachdem Sie Ihre Identitätsdaten und Namespaces, die Einverständniskonfiguration und die Datennutzungskennzeichnung eingerichtet haben, können Sie [!DNL Segment Match] und die zugehörigen Funktionen verwenden.

### Verwalten von Partnern

Wählen Sie im linken Navigationsbereich der Platform-Benutzeroberfläche die Option **[!UICONTROL Segmente]** und dann in der oberen Zeile **[!UICONTROL Feeds]** aus.

![segments-feed.png](./images/segments-feed.png)

Die Seite [!UICONTROL Feeds] enthält eine Liste der Feeds, die von Partnern empfangen wurden, sowie der Feeds, die Sie freigegeben haben. Um eine Liste der vorhandenen Partner anzuzeigen oder eine Verbindung mit einem neuen Partner herzustellen, wählen Sie **[!UICONTROL Partner verwalten]** aus.

![manage-partners.png](./images/manage-partners.png)

Eine Verbindung zwischen zwei Partnern ist ein „bidirektionaler Handshake“, der als Self-Service-Methode dient, mit der Benutzende ihre Platform-Organisationen auf Sandbox-Ebene miteinander verbinden können. Die Verbindung ist erforderlich, um Platform darüber zu informieren, dass eine Vereinbarung getroffen wurde, und das Teilen von Services zwischen Ihnen und Ihren Partnern durch Platform zu ermöglichen.

>[!NOTE]
>
>Der „bidirektionale Handshake“ zwischen Ihnen und Ihrem Partner ist ausschließlich eine Verbindung. Während dieses Vorgangs werden keine Daten ausgetauscht.

Sie können eine Liste der Verbindungen zu vorhandenen Partnern in der Hauptoberfläche des Bildschirms [!UICONTROL Partner verwalten] anzeigen. In der rechten Leiste gibt es das Bedienfeld [!UICONTROL Freigabeeinstellung], über das Sie eine neue [!UICONTROL Verbindungs-ID] sowie ein Eingabefeld zur Eingabe der [!UICONTROL Verbindungs-ID] des Partners generieren können.

![establish-connection.png](./images/establish-connection.png)

Um eine neue [!UICONTROL Verbindungs-ID] zu erstellen, wählen Sie unter [!UICONTROL Freigabeeinstellung] die Option **[!UICONTROL Erneut generieren]** und dann das Kopiersymbol neben der neu generierten ID aus.

![share-setting.png](./images/share-setting.png)

Um einen Partner über seine [!UICONTROL Verbindungs-ID] zu verbinden, geben Sie den Wert seiner eindeutigen ID in das Eingabefeld unter [!UICONTROL Partner verbinden] ein und wählen Sie dann **[!UICONTROL Anfrage]** aus.

![connect-partner.png](./images/connect-partner.png)

### Erstellen eines Feeds {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Eingeschränkte Marketing-Anwendungsfälle"
>abstract="Eingeschränkte Marketing-Anwendungsfälle helfen Ihren Partnern dabei, sicherzustellen, dass freigegebene Segmente gemäß Ihren Data-Governance-Beschränkungen ordnungsgemäß verwendet werden."
>text="Learn more in documentation"

Bei einem **Feed** handelt es sich um eine Gruppierung von Daten (Segmenten), die Regeln, wie diese Daten bereitgestellt oder verwendet werden können, und die Konfigurationen, die bestimmen, wie Ihre Daten mit den Daten Ihrer Partner abgeglichen werden. Ein Feed kann unabhängig verwaltet und mit anderen Platform-Benutzenden über [!DNL Segment Match] ausgetauscht werden.

Um einen neuen Feed zu erstellen, wählen Sie aus dem Dashboard [!UICONTROL Feeds] die Option **[!UICONTROL Feed erstellen]** aus.

![create-feed.png](./images/create-feed.png)

Die grundlegende Einrichtung eines Feeds umfasst einen Namen, eine Beschreibung und Konfigurationen zu Marketing-Anwendungsfällen und Identitätseinstellungen. Geben Sie einen Namen und eine Beschreibung für Ihren Feed ein und wenden Sie dann die Marketing-Anwendungsfälle an, von denen Ihre Daten ausgeschlossen werden sollen. Sie können mehr als einen Anwendungsfall aus einer Liste auswählen, die Folgendes enthält:

* [!UICONTROL Analytics]
* [!UICONTROL Kombination mit PII]
* [!UICONTROL Site-übergreifendes Targeting]
* [!UICONTROL Datenwissenschaft]
* [!UICONTROL E-Mail-Targeting]
* [!UICONTROL Export an Dritte]
* [!UICONTROL Onsite-Werbung]
* [!UICONTROL Onsite-Personalisierung]
* [!UICONTROL Segment Match]
* [!UICONTROL Personalisierung für eine einzelne Identität]

Wählen Sie abschließend die entsprechenden Identity-Namespaces für Ihren Feed aus. Informationen zu den spezifischen Namespaces, die von [!DNL Segment Match] unterstützt werden, finden Sie in der [Identitätsdaten- und Namenspaces-Tabelle](#namespaces). Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus.

![audience-sharing.png](./images/audience-sharing.png)

Nachdem Sie die Einstellungen für Ihren Feed festgelegt haben, wählen Sie die Segmente aus, die Sie aus Ihrer Liste der Erstanbieter-Segmente freigeben möchten. Sie können mehr als ein Segment aus der Liste auswählen und die rechte Leiste verwenden, um Ihre Liste der ausgewählten Segmente zu verwalten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus.

![select-segments.png](./images/select-segments.png)

Die Seite [!UICONTROL Freigeben] wird angezeigt und stellt eine Oberfläche zur Auswahl der Partner, für die Sie Ihren Feed freigeben möchten, bereit. Während dieses Schritts können Sie auch den Bericht mit den Überschneidungsschätzungen vor der Freigabe anzeigen und die nach Namespace sortierte Anzahl der Identitäten mit Überschneidungen zwischen Ihnen und Ihrem Partner sowie die Anzahl der Identitäten mit Überschneidungen sehen, die mit der Datenfreigabe einverstanden sind.

Wählen Sie **[!UICONTROL Nach Segment analysieren]** aus, um den Schätzbericht anzuzeigen.

![analyze.png](./images/analyze.png)

Der Bericht mit den Überschneidungsschätzungen ermöglicht es Ihnen, Überschneidungen und Einverständnisprüfungen pro Partner und Segment zu verwalten, bevor Sie Ihren Feed freigeben.

| Metriken | Beschreibung |
| ------- | ----------- |
| Geschätzte Identitäten mit Einverständnis | Die Gesamtzahl der Identitäten mit Überschneidungen, die die für Ihre Organisation konfigurierten Einverständnisanforderungen erfüllen. |
| Geschätzte Identitäten mit Überschneidungen | Die Anzahl der Identitäten, die sich für das ausgewählte Segment qualifizieren und auch dem ausgewählten Partner entsprechen. Diese Identitäten werden nach Namespace angezeigt und stellen keine individuellen Profilidentitäten dar. Die Überschneidungsschätzungen basieren auf Profilskizzen. |

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Schließen]** aus.

![overlap-report.png](./images/overlap-report.png)

Nachdem Sie Ihre Partner ausgewählt und den Bericht mit den Überschneidungsschätzungen angezeigt haben, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![share.png](./images/share.png)

Der Schritt [!UICONTROL Überprüfung] wird angezeigt, sodass Sie Ihren neuen Feed vor der Freigabe und Veröffentlichung überprüfen können. Dieser Schritt enthält Details zur angewendeten Identitätseinstellung sowie Informationen zu den von Ihnen ausgewählten Marketing-Anwendungsfällen, Segmenten und Partnern.

Wählen Sie **[!UICONTROL Beenden]** aus, um fortzufahren.

![review.png](./images/review.png)

### Aktualisieren eines Feeds

Um Segmente hinzuzufügen oder zu entfernen, wählen Sie auf der Seite [!UICONTROL Feeds] die Option **[!UICONTROL Feed erstellen]** und dann **[!UICONTROL Vorhandener Feed]** aus. Wählen Sie in der angezeigten Liste der vorhandenen Feeds den Feed aus, den Sie aktualisieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![feed-list](./images/feed-list.png)

Die Liste der Segmente wird angezeigt. Von hier aus können Sie neue Segmente zu Ihrem Feed hinzufügen und über die rechte Leiste alle Segmente entfernen, die Sie nicht mehr benötigen. Nachdem Sie mit der Verwaltung der Segmente in Ihrem Feed fertig sind, wählen Sie **[!UICONTROL Weiter]** aus und führen Sie dann die oben beschriebenen Schritte aus, um den aktualisierten Feed abzuschließen.

![Aktualisieren](./images/update.png)

>[!NOTE]
>
>Wenn Sie ein Segment zu einem freigegebenen Feed hinzufügen oder daraus entfernen, muss der empfangende Partner die Änderung bestätigen, indem er den [!DNL Profile]-Umschalter in der Liste der empfangenen Feeds erneut aktiviert.

### Akzeptieren eines eingehenden Feeds

Um einen eingehenden Feed anzuzeigen, wählen Sie in der Kopfzeile der Seite [!UICONTROL Feeds] die Option **[!UICONTROL Erhalten]** und dann den Feed aus der Liste aus, der angezeigt werden soll. Um den Feed zu akzeptieren, wählen Sie **[!UICONTROL Für Profil aktivieren]** aus und warten Sie einen Augenblick, bis sich der Status von [!UICONTROL Ausstehend] zu [!UICONTROL Aktiviert] ändert.

![received.png](./images/received.png)

Sobald Sie einen freigegebenen Feed akzeptiert haben, können Sie mit der Verwendung der freigegebenen Daten beginnen, um neue Segmente zu erstellen.

## Nächste Schritte

Durch dieses Dokument haben Sie einen Einblick in [!DNL Segment Match], seine Funktionen und seinen End-to-End-Workflow gewonnen. Weitere Informationen zu anderen Platform-Services finden Sie in den folgenden Dokumenten:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] – Übersicht](../../../profile/home.md)
