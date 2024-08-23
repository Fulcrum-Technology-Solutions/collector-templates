# Rapid7 REST Collector

This README covers how to configure Cribl Stream REST Collectors and Event Breakers to gather data from the Rapid7 cloud security platform. To do this, the REST Collectors will communicate with APIs that your organization's Rapid7 portal exposes. You'll create and configure four REST Collectors, one for each of these Rapid7 APIs: Assets, Vulnerabilities and Assets_Vulnerabilities.

When creating REST Collectors, you'll replace a few values in the configuration with values from your Rapid7 portal. The Manage as JSON approach is faster and less error-prone than clicking your way through the relevant UIs, especially since the configurations required to interact with the Rapid7 APIs are quite complicated.

You will need the below values for Rapid7 to complete the integration:

| Item                                | Value                                                  |
| ----------------------------------- | ------------------------------------------------------ |
| Region                              | The Rapid7 Region (i.e. us, us2, us3, eu, ca, au, ap)  |
| Rapid7 API Key                      | The Rapid7 API Key                                     |
| Rapid7 Region for the host metadata | The Rapid7 Region (i.e. us, us2, us3, eu, ca, au, ap)r |
| Index                               | The index to send the events to                        |

## Downloading Configuration Files

Download the required event breaker and REST Collector JSON configuration files from [this Cribl repo](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7). You will import these in the below steps.

## Configuring the Event Breaker

Although you will create four REST Collectors, you only need to import a single Event Breaker included in the [repo](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7), whose ruleset contains one rule per API. All four REST Collectors will use that Event Breaker. Each Rapid7 REST Collector configuration contained in the [repo](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7) will already be configured to use the event breaker (breaker.json) also contained in the [repo](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7).

The Event Breaker splits the stream into individual events. You will have a single event for each unique record.

1. Navigate to **Manage > Processing > Knowledge > Event Breaker Rules**.
2. Click **Add Ruleset**.
3. Click **Manage as JSON** at lower left.
4. Click **Import** at top right.
5. Select the breaker.json file you downloaded from [here](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7).
6. Click **OK**.

## Importing and Configuring each REST Collector

> You'll need to complete the procedure in this section for each of the 3 Rapid7 Collectors contained in the [repo](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7).

> To learn more about REST Collectors, see our [Collector Scheduling and Running page](https://docs.cribl.io/stream/collectors-schedule-run/).

> To learn more about using placeholders in the Collector Import process, see [this](https://docs.cribl.io/stream/collectors/#importing-json).

From the top nav of a Cribl Stream instance or Group, select **Data > Sources**, then select **Collectors > REST** from the **Data Sources** page's tiles or the **Sources** left nav. Click **Add Collector** to open the **REST > New Collector** modal.

1. Click **Manage as JSON** to open the configuration editor.
2. Select **Import** from the top right and choose one of the 3 configuration files (named collector\_\*.json) you downloaded from the [repo](https://github.com/criblio/collector-templates/tree/main/collectors/rest/rapid7).
3. Click **OK**
4. A modal will open and prompt you for the four values that are specific to your Organization. Populate the form fields for `Region`, `Rapid7 API Key`, `Rapid7 Region for the host metadata`, and `Index`. Tooltips are available for each field, and you can add or modify them later if you prefer.
5. Click **Replace Values**.
6. Click **OK**.
7. Click **Save**.

Once you've created all four REST Collectors, you'll be ready to start collecting from the Rapid7 APIs.

## Discovering and Collecting

You can perform the procedures in this section with any of the four REST Collectors you've created. To configure time ranges, you'll use **Earliest** and **Latest** values.

- If you enter **Earliest** and **Latest values**, Cribl Stream will pass them into the API query.
- If you leave these fields blank, Cribl Stream will query the API for 24 hours before the job is scheduled to run.

### Automating your Collector Runs

1. On the **Manage REST Collectors** page, click **Schedule** in the **Actions** column for your new Collector. The **Run** Collector modal will open.
2. Toggle **Enable** on and configure the scheduling options as desired.
3. Click **Save**.

## Author

FTSC - cribl-dev@ftsc.com
