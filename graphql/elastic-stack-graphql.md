# Elastic Stack GraphQL Schema

This GraphQL schema provides a conceptual representation of the Elastic Stack APIs, covering Elasticsearch search and indexing, Kibana visualization, Logstash data processing, and Beats data shipping capabilities.

## Overview

The Elastic Stack (formerly ELK Stack) is a collection of open-source products from Elastic designed to help users search, analyze, and visualize data in real-time. This schema captures the core domain concepts exposed through the Elasticsearch REST API and related stack components.

**Source Documentation:** https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html
**GitHub Organization:** https://github.com/elastic

## Schema File

- [elastic-stack-schema.graphql](elastic-stack-schema.graphql)

## Type Categories

### Index and Storage
- `Index`, `IndexDetails`, `IndexMapping`, `IndexSettings`, `IndexAlias`, `IndexStats` — Index lifecycle, configuration, mappings, and statistics.

### Documents
- `Document`, `DocumentSource`, `DocumentMeta`, `DocumentFields` — Document structure and metadata within an Elasticsearch index.

### Search
- `SearchResult`, `SearchHit`, `HitDetails` — Search response wrappers and hit details.
- `SearchQuery`, `QueryClause` — Query composition structures.
- `BoolQuery`, `TermQuery`, `MatchQuery`, `RangeQuery`, `GeoQuery`, `NestedQuery`, `ScriptQuery`, `PercolateQuery` — Specific query types.

### Aggregations
- `Aggregation`, `BucketAggregation`, `MetricAggregation`, `PipelineAggregation` — Aggregation abstractions.
- `Terms`, `DateHistogram`, `RangeAgg`, `Nested`, `Reverse` — Bucket aggregation types.
- `Bucket`, `BucketDetails`, `BucketFilter`, `SubAggregation` — Bucket result structures.

### Mappings and Fields
- `Mapping`, `MappingField`, `FieldType`, `FieldMapping` — Index mapping definitions and field type configurations.

### Scripting
- `Script`, `ScriptDetails` — Painless script definitions used for custom scoring, transformations, and ingest processing.

### Ingest and Pipelines
- `Pipeline`, `PipelineProcessor`, `IngestPipeline` — Ingest pipeline definitions for pre-processing documents before indexing.

### Cluster and Node Management
- `Cluster`, `ClusterDetails`, `NodeDetails`, `ShardInfo`, `SegmentInfo` — Cluster health, node statistics, shard allocation, and segment information.

### Alerting and Watcher
- `Watch`, `WatchDetails`, `WatchAction`, `AlertCondition` — Elasticsearch Watcher definitions for alerts and automated actions.

### Machine Learning
- `MachineLearning`, `Anomaly`, `Forecast` — Elasticsearch ML job configurations and results.

### Snapshots
- `Snapshot` — Repository-backed index snapshot definitions for backup and restore.

### Security
- `APIKey`, `Token` — API key and token-based authentication objects.

## Usage Notes

This schema is conceptual and maps to the Elasticsearch REST API surface. In a production GraphQL layer over Elasticsearch, resolvers would proxy to the appropriate REST endpoints:

- Index operations: `GET /<index>`, `PUT /<index>`, `DELETE /<index>`
- Document CRUD: `GET /<index>/_doc/<id>`, `PUT /<index>/_doc/<id>`, `DELETE /<index>/_doc/<id>`
- Search: `POST /<index>/_search`
- Aggregations: Nested within `_search` request body
- Cluster APIs: `GET /_cluster/health`, `GET /_nodes`
- Ingest: `PUT /_ingest/pipeline/<id>`, `GET /_ingest/pipeline`
- Security: `POST /_security/api_key`, `GET /_security/api_key`
- Machine Learning: `PUT /_ml/anomaly_detectors/<id>`, `GET /_ml/anomaly_detectors`
- Watcher: `PUT /_watcher/watch/<id>`, `GET /_watcher/watch/<id>`
- Snapshots: `PUT /_snapshot/<repo>/<snapshot>`, `GET /_snapshot/<repo>/<snapshot>`
