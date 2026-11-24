---
sidebar_position: 3
title: Switch Document Engine
sidebar_label: Switch Document Engine
slug: /switch_doc_engine
sidebar_custom_props: {
  categoryIcon: LucideShuffle
}
---
# Switch Document Engine

Switch your doc engine from Elasticsearch to Infinity.

---

The supplied Docker Compose configuration uses [Infinity](https://github.com/infiniflow/infinity/) by default to store full text and vectors. Follow these steps for an existing deployment that uses Elasticsearch:

1. Back up the existing deployment before switching engines. Switching engines creates a new document-index store; reindex the documents after startup.

2. Stop the Go deployment:

   ```bash
   docker compose --env-file docker/.env -f docker/docker-compose.yml down
   ```

:::caution WARNING
Do not add `-v` unless you intentionally want to delete the deployment's data volumes.
:::

3. Set `DOC_ENGINE=infinity` in **docker/.env**.

4. Start the Go deployment:

   ```bash
   docker compose --env-file docker/.env -f docker/docker-compose.yml up -d
   ```

5. Reindex the documents and verify retrieval before retiring the previous document-engine data.
