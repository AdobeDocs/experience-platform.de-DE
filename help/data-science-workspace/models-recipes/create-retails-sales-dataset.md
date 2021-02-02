---
keywords: Experience Platform;Retail-Vertriebsrezept;Data Science Workspace;beliebte Themen;Rezepte
solution: Experience Platform
title: Schema und Datensatz für Einzelhandelsumsätze erstellen
topic: tutorial
type: Tutorial
description: Diese Anleitung beinhaltet Informationen über die Voraussetzungen und Elemente, die bei allen anderen Anleitungen für Adobe Experience Platform Data Science Workspace benötigt werden. Danach stehen Ihnen und den Mitgliedern Ihrer IMS-Organisation in Experience Platform das Schema „Einzelhandelsumsätze“ und entsprechende Datensätze zur Verfügung.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 65%

---


# Schema und Datensatz für Einzelhandelsumsätze erstellen

Dieses Lernprogramm enthält die Voraussetzungen und Elemente, die für alle anderen [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]-Lernprogramme erforderlich sind. Nach Abschluss des Projekts stehen Ihnen und Ihren Mitgliedern Ihres IMS-Unternehmens das Retail Sales Schema und die Datensätze unter [!DNL Experience Platform] zur Verfügung.

## Erste Schritte

Bevor Sie mit diesem Tutorial beginnen, müssen Sie folgende Voraussetzungen erfüllen:
- Zugriff auf [!DNL Adobe Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.
- Autorisierung zum Durchführen von API-Aufrufen [!DNL Experience Platform]. Führen Sie die Anleitung zum [Authentifizieren und Aufrufen von Adobe Experience Platform-APIs](https://www.adobe.com/go/platform-api-authentication-en) aus, um die folgenden Werte abzurufen, damit die Anleitung erfolgreich abgeschlossen werden kann:
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client-Geheimnis: `{CLIENT_SECRET}`
   - Client-Zertifikat: `{PRIVATE_KEY}`
- Beispieldaten und Quelldateien für das [Rezept „Einzelhandelsumsätze“](../pre-built-recipes/retail-sales.md). Laden Sie die für diese und andere [!DNL Data Science Workspace]-Tutorials erforderlichen Elemente aus dem öffentlichen Git-Repository [Adobe](https://github.com/adobe/experience-platform-dsw-reference/) herunter.
- [ >= 2.7](https://www.python.org/downloads/)[!DNL Python] und die folgenden Python-Pakete:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Ein grundlegendes Verständnis der folgenden in dieser Anleitung verwendeten Konzepte:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Grundlagen der Schemakomposition](../../xdm/schema/field-dictionary.md)

## Schema und Datensatz für Einzelhandelsumsätze erstellen

Das Schema und die Datensätze für Einzelhandelsumsätze werden mithilfe des bereitgestellten Bootstrap-Skripts automatisch erstellt. Führen Sie folgende Schritte in der richtigen Reihenfolge aus:

### Dateien konfigurieren

1. Navigieren Sie im Ressourcenpaket für [!DNL Experience Platform] zum Verzeichnis `bootstrap` und öffnen Sie `config.yaml` mit einem entsprechenden Texteditor.
2. Geben Sie unter dem Abschnitt `Enterprise` die folgenden Werte ein:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
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
   - `ims_token`: Ihr `{ACCESS_TOKEN}` gehört hier hin.
   - `ingest_data`: Setzen Sie für diese Anleitung den Wert auf `"True"`, um die Schemas und Datensätze für Einzelhandelsumsätze zu erstellen. Beim Wert `"False"` werden nur die Schemas erstellt.
   - `build_recipe_artifacts`: Setzen Sie für diese Anleitung den Wert auf `"False"`, um zu verhindern, dass das Skript ein Rezeptartefakt generiert.
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

1. Öffnen Sie die Terminalanwendung und navigieren Sie zum Ordner für [!DNL Experience Platform]-Übungsressourcen.
2. Legen Sie den Ordner `bootstrap` als aktuellen Arbeitspfad fest und führen Sie das Skript `bootstrap.py` [!DNL Python] aus, indem Sie den folgenden Befehl eingeben:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Das Skript kann mehrere Minuten in Anspruch nehmen.

## Nächste Schritte

Nach erfolgreichem Abschluss des Bootstrap-Skripts können die Retail Sales-Eingabe- und -Ausgabe-Schema und -Datensätze unter [!DNL Experience Platform] angezeigt werden. Weiterführende Informationen finden Sie in der Anleitung zum [Anzeigen einer Vorschau von Schemadaten](./preview-schema-data.md).

Sie haben auch erfolgreich Musterdaten für Einzelhandelsverkäufe in [!DNL Experience Platform] mit dem bereitgestellten Bootstrap-Skript erfasst.

So arbeiten Sie weiter mit den aufgenommenen Daten:
- [Daten mit Jupyter-Notebooks analysieren](../jupyterlab/analyze-your-data.md)
   - Verwenden Sie Jupyter Notebooks in Data Science Workspace, um auf Ihre Daten zuzugreifen, sie zu untersuchen, zu visualisieren und zu verstehen.
- [Quelldateien in einem Rezept verpacken](./package-source-files-recipe.md)
   - Folgen Sie diesem Lernprogramm, um zu erfahren, wie Sie Ihr eigenes Modell in [!DNL Data Science Workspace] durch Verpacken von Quelldateien in einer wichtigen Recipe-Datei bringen.