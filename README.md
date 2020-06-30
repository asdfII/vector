<p align="center">
  <strong>
    <a href="https://vector.dev/components/">Components<a/>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="https://vector.dev/guides/">Guides<a/>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="https://vector.dev/docs/">Docs<a/>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="https://vector.dev/blog/">Blog<a/>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="https://vector.dev/releases/latest/download/">Download v0.9.2<a/>
  </strong>
</p>

---

<p align="center">
  <img src="./website/static/img/readme_diagram.svg" alt="Vector">
</p>


<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the template located at:

     README.md.erb
-->

## What is Vector?

Vector is a lightweight, ultra-fast, [open-source][urls.vector_repo] tool for
building observability pipelines. Compared to Logstash and friends, Vector
[improves throughput by ~10X while significanly reducing CPU and memory
usage][urls.vector_performance].

### Principles

* **Reliability First.** - Built in [Rust][urls.rust], Vector's primary design goal is reliability.
* **One Tool. All Data.** - One simple tool gets your [logs][docs.data-model.log], [metrics][docs.data-model.metric], and traces (coming soon) from A to B.
* **Single Responsibility.** - Vector is a _data router_, it does not plan to become a distributed processing framework.

### Who should use Vector?

* You _SHOULD_ use Vector to replace Logstash, Fluent*, Telegraf, Beats, or similar tools.
* You _SHOULD_ use Vector as a [daemon][docs.strategies#daemon] or [sidecar][docs.strategies#sidecar].
* You _SHOULD_ use Vector as a Kafka consumer/producer for observability data.
* You _SHOULD_ use Vector in resource constrained environments (such as devices).
* You _SHOULD NOT_ use Vector if you need an advanced distributed stream processing framework.
* You _SHOULD NOT_ use Vector to replace Kafka. Vector is designed to work with Kafka!
* You _SHOULD NOT_ use Vector for non-observability data such as analytics data.

### Community

* Vector is **downloaded over 100,000 times per day**.
* Vector's largest user **processes over 10TB daily**.
* Vector is **used by multiple fortune 500 companies** with stringent production requirements.
* Vector has **over 15 active contributors** and growing.


## [Documentation](https://vector.dev/docs/)

### About

* [**Concepts**][docs.concepts]
* [**Data model**][docs.data_model] - [log event][docs.data-model.log], [metric event][docs.data-model.metric]
* [**Guarantees**][docs.guarantees]

### Setup

* [**Installation**][docs.installation] - [operating systems][docs.operating_systems], [package managers][docs.package_managers], [platforms][docs.platforms], [from archives][docs.from-archives], [from source][docs.from-source]
* [**Configuration**][docs.configuration]
* [**Deployment**][docs.deployment] - [strategies][docs.strategies], [topologies][docs.topologies]

### Reference

* [**Sources**][docs.sources] - [docker][docs.sources.docker], [file][docs.sources.file], [http][docs.sources.http], [journald][docs.sources.journald], [kafka][docs.sources.kafka], [socket][docs.sources.socket], and [8 more...][docs.sources]
* [**Transforms**][docs.transforms] - [filter][docs.transforms.filter], [json_parser][docs.transforms.json_parser], [log_to_metric][docs.transforms.log_to_metric], [logfmt_parser][docs.transforms.logfmt_parser], [lua][docs.transforms.lua], [regex_parser][docs.transforms.regex_parser], and [19 more...][docs.transforms]
* [**Sinks**][docs.sinks] - [aws_cloudwatch_logs][docs.sinks.aws_cloudwatch_logs], [aws_s3][docs.sinks.aws_s3], [clickhouse][docs.sinks.clickhouse], [elasticsearch][docs.sinks.elasticsearch], [gcp_cloud_storage][docs.sinks.gcp_cloud_storage], [gcp_pubsub][docs.sinks.gcp_pubsub], and [26 more...][docs.sinks]

### Administration

* [**Process management**][docs.process-management]
* [**Monitoring**][docs.monitoring]
* [**Updating**][docs.updating]
* [**Validating**][docs.validating]

### Resources

* [**Community**][urls.vector_community] - [chat][urls.vector_chat], [@vectordotdev][urls.vector_twitter], [mailing list][urls.mailing_list]
* [**Releases**][urls.vector_releases] - [v0.9.2 (latest)][urls.v0.9.2]
* [**Roadmap**][urls.vector_roadmap] - [vote on new features][urls.vote_feature]
* **Policies** - [Security][urls.vector_security_policy], [Privacy][urls.vector_privacy_policy], [Code of Conduct][urls.vector_code_of_conduct]


## Performance

The following performance tests demonstrate baseline performance between
common protocols with the exception of the Regex Parsing test.

| Test | Vector | Filebeat | FluentBit | FluentD | Logstash | SplunkUF | SplunkHF |
| ---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [TCP to Blackhole](https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_blackhole_performance) | _**86mib/s**_ | n/a | 64.4mib/s | 27.7mib/s | 40.6mib/s | n/a | n/a |
| [File to TCP](https://github.com/timberio/vector-test-harness/tree/master/cases/file_to_tcp_performance) | _**76.7mib/s**_ | 7.8mib/s | 35mib/s | 26.1mib/s | 3.1mib/s | 40.1mib/s | 39mib/s |
| [Regex Parsing](https://github.com/timberio/vector-test-harness/tree/master/cases/regex_parsing_performance) | 13.2mib/s | n/a | _**20.5mib/s**_ | 2.6mib/s | 4.6mib/s | n/a | 7.8mib/s |
| [TCP to HTTP](https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_http_performance) | _**26.7mib/s**_ | n/a | 19.6mib/s | <1mib/s | 2.7mib/s | n/a | n/a |
| [TCP to TCP](https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_tcp_performance) | 69.9mib/s | 5mib/s | 67.1mib/s | 3.9mib/s | 10mib/s | _**70.4mib/s**_ | 7.6mib/s |

To learn more about our performance tests, please see the [Vector test harness][urls.vector_test_harness].


## Correctness

The following correctness tests are not exhaustive, but they demonstrate
fundamental differences in quality and attention to detail:

| Test | Vector | Filebeat | FluentBit | FluentD | Logstash | Splunk UF | Splunk HF |
| ---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [Disk Buffer Persistence](https://github.com/timberio/vector-test-harness/tree/master/cases/disk_buffer_persistence_correctness) | ✅ | ✅ | ❌ | ❌ | ⚠️ | ✅ | ✅ |
| [File Rotate (create)](https://github.com/timberio/vector-test-harness/tree/master/cases/file_rotate_create_correctness) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| [File Rotate (copytruncate)](https://github.com/timberio/vector-test-harness/tree/master/cases/file_rotate_truncate_correctness) | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ |
| [File Truncation](https://github.com/timberio/vector-test-harness/tree/master/cases/file_truncate_correctness) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| [Process (SIGHUP)](https://github.com/timberio/vector-test-harness/tree/master/cases/sighup_correctness) | ✅ | ❌ | ❌ | ❌ | ⚠️ | ✅ | ✅ |
| [JSON (wrapped)](https://github.com/timberio/vector-test-harness/tree/master/cases/wrapped_json_correctness) | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |

To learn more about our correctness tests, please see the [Vector test harness][urls.vector_test_harness].


## The Little Details

### Data Model

* **All data types** - [Logs][docs.data-model.log], [metrics][docs.data-model.metric], and traces (coming soon).
* **Customizable log schema** - [Change Vector's log schema][docs.global-options#log_schema] to anything you like.
* **Rich type system** - Support for [JSON primitive types][docs.data-model.log#types] and [timestamps][docs.data-model.log#timestamps].
* **Metrics interoperability** - A [sophisticated metrics data model][docs.data-model.metric] ensures _correct_ interoperability between systems.
* **Metrics aggregation** - Aggregated [histgorams][docs.data-model.metric#aggregated_histogram] and [summaries][docs.data-model.metric#aggregated_summary] reduce volume without loss of precision.

### Control Flow

* **Pipelining** - A [directed acyclic graph processing model][docs.configuration] allows for flexible topologies.
* **Control-flow** - Transforms like the [`swimlanes` transform][docs.transforms.swimlanes] allow for complex control-flow logic.
* **Dynamic partitioning** - Create [dynamic partitions on the fly][docs.sinks.aws_s3#partitioning] with Vector's [templating syntax][docs.reference.templating].

### Data Processing

* **Programmable transforms** - [Lua][docs.transforms.lua], [Javascript (coming soon)][urls.pr_721], and [WASM (coming soon)][urls.issue_1802] transforms.
* **Rich parsing** - [Regex][docs.transforms.regex_parser], [Grok][docs.transforms.grok_parser], and [more][urls.vector_parsing_transforms] allow for rich parsing.
* **Smart timestamp coercion** - All [parsing transforms][urls.vector_parsing_transforms] implement a [`types` option][docs.transforms.regex_parser#types] that can automatically parse timestamps.
* **Context enrichment** - [Enrich data with environment context][urls.vector_enriching_transforms].
* **Metrics derivation** - [Derive logs from metrics][docs.transforms.log_to_metric].
* **Multi-line merging** - [Merge multi-line logs][docs.sources.file#multiline] into one event, such as stacktraces.

### Operations

* **Hot reload** - [Reload configuration on the fly][docs.process-management#reloading] without disrupting data flow.
* **Zero delay start** - [Starts and restarts][docs.administration.process-management] without a delay.
* **Multi-platform** - [Linux, MacOS, Windows, x86_64, ARM64, and ARMv7][docs.installation].
* **CI friendly** - [Config validating][docs.administration.validating] and [unit tests][guides.advanced.unit-testing] make Vector CI friendly.
* **Configurable concurrency** - All CPU cores ([service][docs.strategies#service]) or just one ([daemon][docs.strategies#daemon]) via the [`--threads` flag][docs.process-management#starting].
* **Custom DNS** - [Custom DNS][docs.global-options#dns_servers] makes service discovery possible.
* **Optional static binary** - [Optional MUSL static binaries][pages.releases] mean zero required dependencies.
* **TLS support** - All relevant Vector components offer TLS options for secure communication.

### Reliability

* **Memory safety** - Vector is built in Rust and is [memory safe][urls.rust_memory_safety], avoiding a large class of memory related errors.
* **Decoupled buffer design** - Buffers are per-[sink][docs.sinks]; a bad sink won't bring the entire pipeline to a halt.
* **Intelligent retries** - A fibonacci backoff algorithsm with jitter makes Vector a good citizen during outages.
* **Backpressure & load shedding** - Buffers can be configured to provide backpressure or shed load.
* **Rate-limited internal logging** - Vector's internal logging is rate-limited avoiding IO saturation if errors occur.
* **Sink healthchecks** - Healthchecks provide startup safety and prevent deploys with bad configuration.
* **Robust disk buffering** - Vector uses `leveldb` for robust data durability across restarts.

### UX

* **Clear Guarantees** - A [guarantee support matrix][docs.guarantees] helps you make the appropriate tradeoffs with components.
* **Config unit tests** - [Develop Vector config files like code][guides.advanced.unit-testing]. Avoid the frustrating dev style required by other tools.
* **Config linting** - [Quickly lint][docs.administration.validating] Vector config files to spot errors and prevent bad configs in CI.
* **Thoughtful docs** - [Quality documentation][docs.what-is-vector] that respects your time and reduces communication overhead.


## Installation

Run the following in your terminal, then follow the on-screen instructions.

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.vector.dev | sh
```

Or use your own [preferred method][docs.installation].

## Deploy

We taught [Vic](https://vector.dev/vic/) how to deploy Vector on Heroku (and to sink Logplex to CloudWatch)! What a good flying squirrel!

Want to spin one up? Hit the button and fill in the boxes.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/timberio/vector/tree/heroku-button&env[VECTOR_TOML_URL]=https://raw.githubusercontent.com/timberio/vector-heroku-buildpack/master/vector.toml)

Then:

```bash
heroku drains:add https://${VECTOR_INSTANCE_NAME}.herokuapp.com/events -a ${YOUR_APP}
```

## Latest Highlights

* [2020/04/20 - Improved Shutdown](https://vector.dev/highlights/2020-04-20-improved-shutdown/) - available in [0.9.0][urls.vector_download]
* [2020/04/17 - 4 New Sinks!](https://vector.dev/highlights/2020-04-17-new-sinks/) - available in [0.9.0][urls.vector_download]
* [2020/04/09 - Set the Lua transform `search_dirs` option to Vector's config dir by default](https://vector.dev/highlights/2020-04-09-set-search_dirs-to-config-dirs-by-default/) - available in [0.9.0][urls.vector_download]
* [2020/04/09 - ACL is now optional for the Google Cloud Storage sink](https://vector.dev/highlights/2020-04-09-make-acl-optional/) - available in [0.9.0][urls.vector_download]
* [2020/04/07 - The Vector Source Now Accepts Metrics](https://vector.dev/highlights/2020-04-07-vector-to-vector-metrics/) - available in [0.9.0][urls.vector_download]

[view all...][urls.vector_highlights]

---

<p align="center">
  Developed with ❤️ by <strong><a href="https://timber.io">Timber.io</a></strong> - <a href="https://github.com/timberio/vector/security/policy">Security Policy</a> - <a href="https://github.com/timberio/vector/blob/master/PRIVACY.md">Privacy Policy</a>
</p>


[docs.administration.process-management]: https://vector.dev/docs/administration/process-management/
[docs.administration.validating]: https://vector.dev/docs/administration/validating/
[docs.concepts]: https://vector.dev/docs/about/concepts/
[docs.configuration]: https://vector.dev/docs/setup/configuration/
[docs.data-model.log#timestamps]: https://vector.dev/docs/about/data-model/log/#timestamps
[docs.data-model.log#types]: https://vector.dev/docs/about/data-model/log/#types
[docs.data-model.log]: https://vector.dev/docs/about/data-model/log/
[docs.data-model.metric#aggregated_histogram]: https://vector.dev/docs/about/data-model/metric/#aggregated_histogram
[docs.data-model.metric#aggregated_summary]: https://vector.dev/docs/about/data-model/metric/#aggregated_summary
[docs.data-model.metric]: https://vector.dev/docs/about/data-model/metric/
[docs.data_model]: https://vector.dev/docs/about/data-model/
[docs.deployment]: https://vector.dev/docs/setup/deployment/
[docs.from-archives]: https://vector.dev/docs/setup/installation/manual/from-archives/
[docs.from-source]: https://vector.dev/docs/setup/installation/manual/from-source/
[docs.global-options#dns_servers]: https://vector.dev/docs/reference/global-options/#dns_servers
[docs.global-options#log_schema]: https://vector.dev/docs/reference/global-options/#log_schema
[docs.guarantees]: https://vector.dev/docs/about/guarantees/
[docs.installation]: https://vector.dev/docs/setup/installation/
[docs.monitoring]: https://vector.dev/docs/administration/monitoring/
[docs.operating_systems]: https://vector.dev/docs/setup/installation/operating-systems/
[docs.package_managers]: https://vector.dev/docs/setup/installation/package-managers/
[docs.platforms]: https://vector.dev/docs/setup/installation/platforms/
[docs.process-management#reloading]: https://vector.dev/docs/administration/process-management/#reloading
[docs.process-management#starting]: https://vector.dev/docs/administration/process-management/#starting
[docs.process-management]: https://vector.dev/docs/administration/process-management/
[docs.reference.templating]: https://vector.dev/docs/reference/templating/
[docs.sinks.aws_cloudwatch_logs]: https://vector.dev/docs/reference/sinks/aws_cloudwatch_logs/
[docs.sinks.aws_s3#partitioning]: https://vector.dev/docs/reference/sinks/aws_s3/#partitioning
[docs.sinks.aws_s3]: https://vector.dev/docs/reference/sinks/aws_s3/
[docs.sinks.clickhouse]: https://vector.dev/docs/reference/sinks/clickhouse/
[docs.sinks.elasticsearch]: https://vector.dev/docs/reference/sinks/elasticsearch/
[docs.sinks.gcp_cloud_storage]: https://vector.dev/docs/reference/sinks/gcp_cloud_storage/
[docs.sinks.gcp_pubsub]: https://vector.dev/docs/reference/sinks/gcp_pubsub/
[docs.sinks]: https://vector.dev/docs/reference/sinks/
[docs.sources.docker]: https://vector.dev/docs/reference/sources/docker/
[docs.sources.file#multiline]: https://vector.dev/docs/reference/sources/file/#multiline
[docs.sources.file]: https://vector.dev/docs/reference/sources/file/
[docs.sources.http]: https://vector.dev/docs/reference/sources/http/
[docs.sources.journald]: https://vector.dev/docs/reference/sources/journald/
[docs.sources.kafka]: https://vector.dev/docs/reference/sources/kafka/
[docs.sources.socket]: https://vector.dev/docs/reference/sources/socket/
[docs.sources]: https://vector.dev/docs/reference/sources/
[docs.strategies#daemon]: https://vector.dev/docs/setup/deployment/strategies/#daemon
[docs.strategies#service]: https://vector.dev/docs/setup/deployment/strategies/#service
[docs.strategies#sidecar]: https://vector.dev/docs/setup/deployment/strategies/#sidecar
[docs.strategies]: https://vector.dev/docs/setup/deployment/strategies/
[docs.topologies]: https://vector.dev/docs/setup/deployment/topologies/
[docs.transforms.filter]: https://vector.dev/docs/reference/transforms/filter/
[docs.transforms.grok_parser]: https://vector.dev/docs/reference/transforms/grok_parser/
[docs.transforms.json_parser]: https://vector.dev/docs/reference/transforms/json_parser/
[docs.transforms.log_to_metric]: https://vector.dev/docs/reference/transforms/log_to_metric/
[docs.transforms.logfmt_parser]: https://vector.dev/docs/reference/transforms/logfmt_parser/
[docs.transforms.lua]: https://vector.dev/docs/reference/transforms/lua/
[docs.transforms.regex_parser#types]: https://vector.dev/docs/reference/transforms/regex_parser/#types
[docs.transforms.regex_parser]: https://vector.dev/docs/reference/transforms/regex_parser/
[docs.transforms.swimlanes]: https://vector.dev/docs/reference/transforms/swimlanes/
[docs.transforms]: https://vector.dev/docs/reference/transforms/
[docs.updating]: https://vector.dev/docs/administration/updating/
[docs.validating]: https://vector.dev/docs/administration/validating/
[docs.what-is-vector]: https://vector.dev/docs/about/what-is-vector/
[guides.advanced.unit-testing]: https://vector.dev/guides/advanced/unit-testing/
[pages.releases]: https://vector.dev/releases/
[urls.issue_1802]: https://github.com/timberio/vector/issues/1802
[urls.mailing_list]: https://vector.dev/community/
[urls.pr_721]: https://github.com/timberio/vector/pull/721
[urls.rust]: https://www.rust-lang.org/
[urls.rust_memory_safety]: https://hacks.mozilla.org/2019/01/fearless-security-memory-safety/
[urls.v0.9.2]: https://vector.dev/releases/0.9.2/download
[urls.vector_chat]: https://chat.vector.dev
[urls.vector_code_of_conduct]: https://github.com/timberio/vector/blob/master/CODE_OF_CONDUCT.md
[urls.vector_community]: https://vector.dev/community/
[urls.vector_download]: https://vector.dev/releases/latest/download/
[urls.vector_enriching_transforms]: https://vector.dev/components/?functions%5B%5D=enrich
[urls.vector_highlights]: https://vector.dev/highlights/
[urls.vector_parsing_transforms]: https://vector.dev/components/?functions%5B%5D=parse
[urls.vector_performance]: https://vector.dev/#performance
[urls.vector_privacy_policy]: https://github.com/timberio/vector/blob/master/PRIVACY.md
[urls.vector_releases]: https://vector.dev/releases/latest/
[urls.vector_repo]: https://github.com/timberio/vector
[urls.vector_roadmap]: https://github.com/timberio/vector/milestones?direction=asc&sort=due_date&state=open
[urls.vector_security_policy]: https://github.com/timberio/vector/security/policy
[urls.vector_test_harness]: https://github.com/timberio/vector-test-harness/
[urls.vector_twitter]: https://twitter.com/vectordotdev
[urls.vote_feature]: https://github.com/timberio/vector/issues?q=is%3Aissue+is%3Aopen+sort%3Areactions-%2B1-desc+label%3A%22Type%3A+New+Feature%22
