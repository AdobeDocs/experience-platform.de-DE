---
keywords: Experience Platform;Einzelhandelsrezept;Datenwissenschafts-Workspace;beliebte Themen;Rezepte
solution: Experience Platform
title: Erstellen eines Einzelhandels-Schemas und -Datensatzes
type: Tutorial
description: Diese Anleitung beinhaltet Informationen über die Voraussetzungen und Elemente, die bei allen anderen Anleitungen für Adobe Experience Platform Data Science Workspace benötigt werden. Nach Abschluss des Vorgangs stehen Ihnen und den Mitgliedern Ihres Unternehmens das Einzelhandelsschema und die Datensätze in Experience Platform zur Verfügung.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 41%

---


# Schema und Datensatz für Einzelhandelsumsätze erstellen

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

In diesem Tutorial erhalten Sie die Voraussetzungen und Assets, die für alle anderen [!DNL Adobe Experience Platform]-[!DNL Data Science Workspace]-Tutorials erforderlich sind. Nach Abschluss des Vorgangs stehen Ihnen und den Mitgliedern Ihres Unternehmens das Einzelhandels-Schema und die Datensätze [!DNL Experience Platform] zur Verfügung.

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:

- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie in [!DNL Experience Platform] keinen Zugriff auf eine Organisation haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.
- Autorisierung zum Ausführen [!DNL Experience Platform] API-Aufrufen. Führen Sie die Anleitung zum [Authentifizieren und Aufrufen von Adobe Experience Platform-APIs](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) aus, um die folgenden Werte abzurufen, damit die Anleitung erfolgreich abgeschlossen werden kann:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Client-Geheimnis: `{CLIENT_SECRET}`
   - Client-Zertifikat: `{PRIVATE_KEY}`
- Beispieldaten und Quelldateien für das [Rezept „Einzelhandelsumsätze“](../pre-built-recipes/retail-sales.md). Laden Sie die für dieses und andere [!DNL Data Science Workspace] Tutorials erforderlichen Assets aus dem [öffentlichen Adobe-Git-Repository ](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) und die folgenden [!DNL Python]:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Ein grundlegendes Verständnis der folgenden in dieser Anleitung verwendeten Konzepte:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Grundlagen der Schema-Komposition](../../xdm/schema/field-dictionary.md)

## Schema und Datensatz für Einzelhandelsumsätze erstellen

Das Schema und die Datensätze für Einzelhandelsumsätze werden mithilfe des bereitgestellten Bootstrap-Skripts automatisch erstellt. Führen Sie folgende Schritte in der richtigen Reihenfolge aus:

### Dateien konfigurieren

1. Navigieren Sie innerhalb des [!DNL Experience Platform]-Ressourcenpakets des Tutorials zum `bootstrap` und öffnen Sie `config.yaml` mit einem entsprechenden Texteditor.
2. Geben Sie unter dem Abschnitt `Enterprise` die folgenden Werte ein:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Bearbeiten Sie die Werte, die Sie im Abschnitt `Platform` finden, wie im folgenden Beispiel:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Der Basispfad für API-Aufrufe. Ändern Sie diesen Wert nicht.
   - `ims_token`: Ihr `{ACCESS_TOKEN}` geht hierher.
   - `ingest_data`: Legen Sie für die Zwecke dieses Tutorials diesen Wert auf `"True"` fest, um die Schemata und Datensätze für den Einzelhandel zu erstellen. Beim Wert `"False"` werden nur die Schemata erstellt.
   - `build_recipe_artifacts`: Legen Sie für die Zwecke dieses Tutorials diesen Wert auf `"False"` fest, um zu verhindern, dass das Skript ein Rezept-Artefakt generiert.
   - `kernel_type`: Der Ausführungstyp des Rezeptartefakts. Lassen Sie diesen Wert unverändert bei `Python`, wenn `build_recipe_artifacts` auf `"False"` gesetzt ist; geben Sie andernfalls den entspechenden Ausführungstyp an.

4. Geben Sie unter dem Abschnitt `Titles` die folgenden Informationen für die Beispieldaten der Einzelhandelsumsätze ein; speichern und schließen Sie die Datei, nachdem Sie die Änderungen vorgenommen haben. Beispiel:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Bootstrap-Skript ausführen

1. Öffnen Sie Ihre Terminal-Anwendung und navigieren Sie zum Ressourcenverzeichnis des [!DNL Experience Platform]-Tutorials.
2. Legen Sie das `bootstrap` als aktuellen Arbeitspfad fest und führen Sie das Skript `bootstrap.py` [!DNL Python] aus, indem Sie den folgenden Befehl eingeben:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Es kann mehrere Minuten dauern, bis das Skript abgeschlossen ist.

## Nächste Schritte

Nach erfolgreichem Abschluss des Bootstrap-Skripts können die Ein- und Ausgabeschemata und Datensätze für den Einzelhandel auf [!DNL Experience Platform] angezeigt werden. Weiterführende Informationen finden Sie in der Anleitung zum [Anzeigen einer Vorschau von Schemadaten](./preview-schema-data.md).

Sie haben auch Beispieldaten zu Einzelhandelsumsätzen mithilfe des bereitgestellten Bootstrap-Skripts erfolgreich in [!DNL Experience Platform] aufgenommen.

So arbeiten Sie weiter mit den aufgenommenen Daten:

- [Daten mit Jupyter Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter-Notebooks in Data Science Workspace, um auf Ihre Daten zuzugreifen, sie zu erkunden, zu visualisieren und zu verstehen.
- [Packen von Quelldateien in ein Rezept](./package-source-files-recipe.md)
   - In diesem Tutorial erfahren Sie, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] importieren, indem Sie Quelldateien in eine importierbare Rezeptdatei packen.
