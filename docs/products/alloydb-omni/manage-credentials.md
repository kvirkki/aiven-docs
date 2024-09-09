---
title: Manage Google service account credentials in Aiven for AlloyDB Omni®
sidebar_label: Manage Google credentials
---

import ConsoleLabel from "@site/src/components/ConsoleIcons";
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Store and manage Google service account credentials in Aiven for AlloyDB Omni® to use them for AI integration purposes.

Add, update, or delete your Google service account credentials in Aiven for AlloyDB Omni
using either the [Aiven Console](https://console.aiven.io) or the
[Aiven CLI client](/docs/tools/cli).

## Prerequisites

- Aiven for AlloyDB Omni service running
- Access to the [Aiven Console](https://console.aiven.io)
- [Aiven CLI client](/docs/tools/cli) installed
- [Service account created with Google Cloud](https://cloud.google.com/iam/docs/service-accounts-create)
- [Google service account key created and downloaded](https://cloud.google.com/iam/docs/keys-create-delete#creating)

## Manage Google credentials in Aiven

### Add a key

<Tabs groupId="group1">
<TabItem value="1" label="Aiven Console" default>
1. Go to the [Aiven Console](https://console.aiven.io) and your Aiven for AlloyDB Omni service.
1. Go to <ConsoleLabel name="generativeai"/> > **Goolge service account key**.
1. Click **Upload file**, browse for the JSON file including your Google service
   account key, and click **Upload file**.
</TabItem>
<TabItem value="2" label="Aiven CLI client">
Run the following command:

```bash
avn service alloydbomni google-cloud-private-key set --service SERVICE_NAME --private-key-file PRIVATE_KEY_FILE
```

Replace the following:

- `SERVICE_NAME` with the name of your service
- `PRIVATE_KEY_FILE` with the path to your key file

</TabItem>
</Tabs>

### Update a key

<Tabs groupId="group1">
<TabItem value="1" label="Aiven Console" default>
1. Go to the [Aiven Console](https://console.aiven.io) and your Aiven for AlloyDB Omni service.
1. Go to <ConsoleLabel name="generativeai"/> > **Goolge service account key**.
1. Click <ConsoleLabel name="actions"/> > **Replace file**, browse for the JSON file
   including your new Google service account key, and click **Replace file**.
</TabItem>
<TabItem value="2" label="Aiven CLI client">
Run the following command:

```bash
avn service alloydbomni google-cloud-private-key set --service SERVICE_NAME --private-key-file PRIVATE_KEY_FILE
```

Replace the following:

- `SERVICE_NAME` with the name of your service
- `PRIVATE_KEY_FILE` with the path to your new key file

</TabItem>
</Tabs>

### Delete a key

<Tabs groupId="group1">
<TabItem value="1" label="Aiven Console" default>
1. Go to the [Aiven Console](https://console.aiven.io) and your Aiven for AlloyDB Omni service.
1. Go to <ConsoleLabel name="generativeai"/> > **Goolge service account key**.
1. Click <ConsoleLabel name="actions"/> > **Delete file** > **Delete**.
</TabItem>
<TabItem value="2" label="Aiven CLI client">
Run the following command:

```bash
avn service alloydbomni google-cloud-private-key delete --service SERVICE_NAME
```

</TabItem>
</Tabs>

## Check key details

Check the key ID or the client email for your key.

<Tabs groupId="group1">
<TabItem value="1" label="Aiven Console" default>
1. Go to the [Aiven Console](https://console.aiven.io) and your Aiven for AlloyDB Omni service.
1. Go to <ConsoleLabel name="generativeai"/> > **Goolge service account key**.
</TabItem>
<TabItem value="2" label="Aiven CLI client">
Run the following command:

```bash
avn service alloydbomni google-cloud-private-key show --service SERVICE_NAME
```

</TabItem>
</Tabs>
