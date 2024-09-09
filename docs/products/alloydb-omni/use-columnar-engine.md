---
title: Manage the Aiven for AlloyDB Omni® columnar engine
sidebar_label: Use columnar engine
---

import ConsoleLabel from "@site/src/components/ConsoleIcons";
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Enable or disable the Aiven for AlloyDB Omni® columnar engine, and control how much RAM
it can use to leverage AI and analytics capabilities of your service.

The Aiven for AlloyDB Omni® columnar engine uses the
[Google's AlloyDB Omni® columnar engine](https://cloud.google.com/alloydb/docs/columnar-engine/about).

:::important
Any change to columnar engine settings results in restarting the service.
:::

## Prerequisites

- Aiven for AlloyDB Omni service running
- Access to the [Aiven Console](https://console.aiven.io/)

## Enable the columnar engine

The columnar engine is enabled by default but you may want to turn it back on after
disabling it.

<Tabs groupId="group1">
<TabItem value="1" label="Service settings" default>
1. Log in to the [Aiven Console](https://console.aiven.io/).
1. On the <ConsoleLabel name="Services"/> page, select a service.
1. Click <ConsoleLabel name="service settings"/>, and go to **Columnar engine**.
1. Click <ConsoleLabel name="actions"/> > **Configure engine**.
1. Set **google_columnar_engine_enabled** to `True`.
1. Click **Save configuration**.
</TabItem>
<TabItem value="2" label="Advanced configuration">
1. Log in to the [Aiven Console](https://console.aiven.io/).
1. On the <ConsoleLabel name="Services"/> page, select a service.
1. Click <ConsoleLabel name="service settings"/>, and go to **Advanced configuration**.
1. Click **Configure** > **Add configuration options**.
1. Find and add option **google_columnar_engine_enabled**.
1. Set **google_columnar_engine_enabled** to `True`.
1. Click **Save configuration**.
</TabItem>
</Tabs>

## Configure the size of the columnar data store

By default, the columnar engine is set to use up to 30% of your service's RAM. You can
modify the size of the columnar engine memory to a maximum of 50% of the service's
memory.

<Tabs groupId="group1">
<TabItem value="1" label="Service settings" default>
1. Log in to the [Aiven Console](https://console.aiven.io/).
1. On the <ConsoleLabel name="Services"/> page, select a service.
1. Click <ConsoleLabel name="service settings"/>, and go to **Columnar engine**..
1. Click <ConsoleLabel name="actions"/> > **Configure engine**.
1. Set **google_columnar_engine_memory_size_percentage** to a value between `0` and `50`.
1. Click **Save configuration**.
</TabItem>
<TabItem value="2" label="Advanced configuration">
1. Log in to the [Aiven Console](https://console.aiven.io/).
1. On the <ConsoleLabel name="Services"/> page, select a service.
1. Click <ConsoleLabel name="service settings"/>, and go to **Advanced configuration**.
1. Click **Configure** > **Add configuration options**.
1. Find and add option **google_columnar_engine_memory_size_percentage**.
1. Set **google_columnar_engine_memory_size_percentage** to a value between `0` and `50`.
1. Click **Save configuration**.
</TabItem>
</Tabs>

## Disable the columnar engine

Disabling the columnar engine reduces memory load and may improve performance.

<Tabs groupId="group1">
<TabItem value="1" label="Service settings" default>
1. Log in to the [Aiven Console](https://console.aiven.io/).
1. On the <ConsoleLabel name="Services"/> page, select a service.
1. Click <ConsoleLabel name="service settings"/>, and go to **Columnar engine**.
1. Click <ConsoleLabel name="actions"/> > **Configure engine**.
1. Set **google_columnar_engine_enabled** to `False`.
1. Click **Save configuration**.
</TabItem>
<TabItem value="2" label="Advanced configuration">
1. Log in to the [Aiven Console](https://console.aiven.io/).
1. On the <ConsoleLabel name="Services"/> page, select a service.
1. Click <ConsoleLabel name="service settings"/>, and go to **Advanced configuration**.
1. Click **Configure** > **Add configuration options**.
1. Find and add option **google_columnar_engine_enabled**.
1. Set **google_columnar_engine_enabled** to `False`.
1. Click **Save configuration**.
</TabItem>
</Tabs>
