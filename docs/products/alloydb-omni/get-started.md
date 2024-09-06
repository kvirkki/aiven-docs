---
title: Get started with Aiven for AlloyDB Omni®
sidebar_label: Get started
keywords: [quick start]
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import ConsoleLabel from "@site/src/components/ConsoleIcons"
import CreateService from "@site/static/includes/create-service-console.md"
import Help from "@site/static/includes/cli-help.md"

Start using Aiven for AlloyDB Omni® by creating and configuring a service, connecting to it, and playing with sample data.

## Prerequisites

- [Aiven CLI](https://github.com/aiven/aiven-client) installed
- Access to the [Aiven Console](https://console.aiven.io)

## Create an Aiven for AlloyDB Omni® service

<Tabs groupId="group1">
<TabItem value="1" label="Console" default>

<CreateService serviceType="AlloyDB Omni®"/>

</TabItem>
<TabItem value="2" label="CLI">

1. Determine the service specifications, including plan, cloud provider, region,
   and project name.

1. Run the following command to create an Aiven for AlloyDB Omni service named
   `demo-alloydb-omni`:

   ```bash
    avn service create demo-alloydb-omni     \
    --service-type alloydb-omni              \
    --cloud CLOUD_AND_REGION                 \
    --plan PLAN                              \
    --project PROJECT_NAME
   ```

   Parameters:

    - `avn service create demo-alloydb-omni`: Command to create new Aiven service
      named `demo-alloydb-omni`.
    - `--service-type alloydb-omni`: Specifies the service type as Aiven for AlloyDB Omn.
    - `--cloud CLOUD_AND_REGION`: Specifies the cloud provider and region for deployment.
    - `--plan PLAN`: Specifies the service plan or tier.
    - `--project PROJECT_NAME`: Specifies the project where the service will be created.

<Help/>

</TabItem>
</Tabs>

## Configure the service

You can change your service settings by updating the service configuration.

:::tip
See configuration options in
[Advanced parameters for Aiven for AlloyDB Omni®](/docs/products/alloydb-omni/advanced-params).
:::

<Tabs groupId="group1">
<TabItem value="1" label="Console" default>
1. Select the new service from the list of services on
   the <ConsoleLabel name="Services"/> page.
1. On the <ConsoleLabel name="overview"/> page, select <ConsoleLabel name="service settings"/>
   from the sidebar.
1. In the **Advanced configuration** section, make changes to the service configuration.
</TabItem>
<TabItem value="2" label="CLI">
</TabItem>
</Tabs>

## Connect to the service{#connect-to-service}

<Tabs groupId="group1">
<TabItem value="1" label="Console" default>
1. Log in to the [Aiven Console](https://console.aiven.io/), and go to your
   organization > project > Aiven for AlloyDB Omni service.
1. On the <ConsoleLabel name="overview"/> page of your service, click
   **Quick connect**.
1. In the **Connect** window, select a tool or language to connect to your service, follow
   the connection instructions, and click **Done**.

</TabItem>
<TabItem value="2" label="CLI">
</TabItem>
</Tabs>

:::tip
Discover more tools for connecting to Aiven for AlloyDB Omni in
[Connect to Aiven for AlloyDB Omni®](/docs/products/alloydb-omni/connect/connect-services).
:::

## Load data into Aiven for AlloyDB Omni

## Read data from Aiven for AlloyDB Omni

## Related pages

- [Supported Aiven for AlloyDB Omni versions](/docs/platform/reference/eol-for-major-versions)
- [Aiven for AlloyDB Omni backups](/docs/platform/concepts/service_backups)
