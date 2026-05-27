# RelationalDBX

RelationalDBX is a distributed relational data layer built on top of FoundationDB. It provides SQL oriented database features, JDBC connectivity, schema templates, advanced data types, transactional storage, secondary indexing, and server/CLI tooling for local development and experimentation.

The project is organized as a Gradle multi module Java codebase. It includes the core record layer, relational APIs, an embedded JDBC driver, a gRPC server, a JDBC client driver, a SQLLine based CLI, Lucene indexing support, spatial/ICU extensions, YAML based tests, examples, documentation, and Docker scripts for running a local FoundationDB cluster.

## Highlights

- SQL database layer on FoundationDB.
- Embedded JDBC connection support with `jdbc:embed:` URLs.
- gRPC server and remote JDBC client support with `jdbc:relational://` URLs.
- Schema templates for reusable multi-tenant database schemas.
- ACID transactions inherited from FoundationDB.
- Secondary indexes, aggregate indexes, rank indexes, Lucene indexes, spatial utilities, and extensibility points.
- Support for complex relational types such as structs, arrays, and vectors.
- SQLLine-based command-line client for interactive querying.
- Local FoundationDB setup through Docker Compose.
- Sphinx documentation and Java examples.

## Tech Stack

| Area | Technology |
| --- | --- |
| Language | Java 17 |
| Build tool | Gradle wrapper |
| Storage engine | FoundationDB |
| API style | JDBC, gRPC, Java APIs |
| SQL CLI | SQLLine |
| Serialization | Protocol Buffers |
| Indexing | FoundationDB indexes, Lucene |
| Docs | Sphinx |
| Local infrastructure | Docker Compose |
| Testing | JUnit, YAML SQL tests |

## Project Structure

```text
RelationalDBX/
├── README.md
├── LICENSE
├── ACKNOWLEDGEMENTS
├── build.gradle
├── settings.gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── package.json
├── vercel.json
├── public/
│   └── index.html
├── gradle/
│   ├── wrapper/
│   ├── libs.versions.toml
│   ├── root.gradle
│   ├── testing.gradle
│   ├── publishing.gradle
│   ├── proto.gradle
│   ├── antlr.gradle
│   └── sphinx.gradle
├── docs/
│   └── sphinx/
├── docker-local/
│   ├── docker-compose.yml
│   ├── relationaldbx-build.sh
│   ├── start.sh
│   └── stop.sh
├── scripts/
│   ├── YAML-SQL.xml
│   └── requirements.txt
├── actions/
│   ├── gradle-test/
│   ├── run-gradle/
│   ├── setup-base-env/
│   ├── setup-relationaldbx/
│   ├── list-recent-versions/
│   ├── publish-mixed-mode-results/
│   └── teamscale-upload/
├── examples/
│   ├── examples.gradle
│   └── src/
│       └── main/
│           ├── java/
│           ├── proto/
│           ├── resources/
│           └── javadoc/
├── relationaldbx-core/
│   ├── relationaldbx-core.gradle
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   ├── proto/
│       │   ├── resources/
│       │   └── javadoc/
│       └── test/
│           ├── java/
│           ├── proto/
│           └── resources/
├── relationaldbx-core-shaded/
│   └── relationaldbx-core-shaded.gradle
├── relationaldbx-java-annotations/
│   ├── relationaldbx-java-annotations.gradle
│   └── src/
│       └── main/
│           └── java/
├── relationaldbx-test-utils/
│   ├── relationaldbx-test-utils.gradle
│   └── src/
│       ├── main/java/
│       └── test/java/
├── relationaldbx-extensions/
│   ├── relationaldbx-extensions.gradle
│   └── src/
│       ├── main/java/
│       ├── test/java/
│       └── testFixtures/java/
├── relationaldbx-debugger/
│   ├── relationaldbx-debugger.gradle
│   └── src/
│       ├── main/java/
│       └── test/java/
├── relationaldbx-icu/
│   ├── relationaldbx-icu.gradle
│   └── src/
│       ├── main/java/
│       └── test/java/
├── relationaldbx-lucene/
│   ├── README.md
│   ├── relationaldbx-lucene.gradle
│   ├── docs/
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   ├── proto/
│       │   ├── resources/
│       │   └── javadoc/
│       └── test/java/
├── relationaldbx-spatial/
│   ├── relationaldbx-spatial.gradle
│   └── src/
│       ├── main/java/
│       └── test/
│           ├── java/
│           └── proto/
├── relationaldbx-jmh/
│   ├── relationaldbx-jmh.gradle
│   └── src/
│       └── jmh/
│           ├── java/
│           └── proto/
├── relationaldbx-relational-api/
│   ├── README.md
│   ├── relationaldbx-relational-api.gradle
│   └── src/
│       ├── main/java/
│       ├── test/
│       │   ├── java/
│       │   └── resources/
│       └── testFixtures/java/
├── relationaldbx-relational-core/
│   ├── README.md
│   ├── relationaldbx-relational-core.gradle
│   └── src/
│       ├── main/
│       │   ├── antlr/
│       │   ├── java/
│       │   └── proto/
│       ├── test/
│       │   ├── java/
│       │   └── resources/
│       ├── testFixtures/java/
│       └── jmh/java/
├── relationaldbx-relational-grpc/
│   ├── README.md
│   ├── relationaldbx-relational-grpc.gradle
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   └── proto/
│       └── test/
│           ├── java/
│           └── resources/
├── relationaldbx-relational-jdbc/
│   ├── relationaldbx-relational-jdbc.gradle
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   └── resources/
│       └── test/
│           ├── java/
│           └── resources/
├── relationaldbx-relational-server/
│   ├── relationaldbx-relational-server.gradle
│   ├── bin/
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   ├── resources/
│       │   └── dist/
│       ├── test/
│       │   ├── java/
│       │   └── resources/
│       └── testFixtures/java/
├── relationaldbx-relational-cli/
│   ├── relationaldbx-relational-cli.gradle
│   └── bin/
└── yaml-tests/
    ├── yaml-tests.gradle
    └── src/
        ├── main/
        │   ├── java/
        │   ├── proto/
        │   └── resources/
        └── test/
            ├── java/
            ├── proto/
            └── resources/
```

## Requirements

Before running the project locally, install:

- JDK 17 or newer.
- Docker Desktop or another Docker-compatible runtime.
- Bash-compatible shell for `gradlew` and `docker-local` scripts.
- Internet access for first-time Gradle dependency and wrapper downloads.

On macOS or Linux, make scripts executable if needed:

```bash
chmod +x gradlew
chmod +x docker-local/*.sh
```

## Quick Start

Unzip the project and enter the root directory:

```bash
unzip RelationalDBX.zip
cd RelationalDBX
```

Start a local FoundationDB cluster:

```bash
./docker-local/start.sh
```

This script starts FoundationDB through Docker Compose and writes local connection files such as:

```text
fdb-environment.properties
fdb-environment.yaml
run/docker.cluster
```

Build and package the project:

```bash
./gradlew clean build
```

For a quicker packaging-oriented build:

```bash
./gradlew package
```

Stop the local FoundationDB container when finished:

```bash
./docker-local/stop.sh
```

## Using The Embedded JDBC Driver

The embedded driver uses `jdbc:embed:` URLs and runs in the same JVM as the application.

Example system catalog connection:

```java
String url = "jdbc:embed:/__SYS?schema=CATALOG";
Connection conn = DriverManager.getConnection(url);
```

Example application database connection:

```java
String url = "jdbc:embed:/FRL/shop?schema=SHOP";
Connection conn = DriverManager.getConnection(url);
```

## Basic SQL Example

```sql
CREATE SCHEMA TEMPLATE shop_template
    CREATE TABLE products (
        id BIGINT,
        name STRING,
        category STRING,
        price BIGINT,
        stock BIGINT,
        PRIMARY KEY(id)
    )
    CREATE INDEX product_category_price AS
        SELECT category, price FROM products ORDER BY category, price;

CREATE DATABASE "/FRL/shop";
CREATE SCHEMA "/FRL/shop/SHOP" WITH TEMPLATE shop_template;

INSERT INTO products VALUES (1, 'Keyboard', 'Accessories', 2999, 50);
INSERT INTO products VALUES (2, 'Mouse', 'Accessories', 999, 80);

SELECT * FROM products WHERE category = 'Accessories' ORDER BY price;
```

## Running The CLI

Build the CLI distribution:

```bash
./gradlew :relationaldbx-relational-cli:installDist
```

Run SQLLine against the embedded catalog database:

```bash
./relationaldbx-relational-cli/.out/install/relationaldbx-relational-sqlline/bin/relationaldbx-relational-sqlline \
  -u "jdbc:embed:/__SYS?schema=CATALOG"
```

You can also connect to an application database:

```bash
./relationaldbx-relational-cli/.out/install/relationaldbx-relational-sqlline/bin/relationaldbx-relational-sqlline \
  -u "jdbc:embed:/FRL/shop?schema=SHOP"
```

## Running The gRPC Server

Build the server distribution:

```bash
./gradlew :relationaldbx-relational-server:installDist
```

Start the server with an explicit gRPC and metrics port:

```bash
./relationaldbx-relational-server/.out/install/relationaldbx-relational-server/bin/relationaldbx-relational-server \
  --clusterFile run/docker.cluster \
  --grpcPort 7243 \
  --httpPort 7244
```

Connect through the remote JDBC driver:

```java
String url = "jdbc:relational://localhost:7243/__SYS?schema=CATALOG";
Connection conn = DriverManager.getConnection(url);
```

## Running Examples

The `examples` module contains sample Java code and JDBC snippets.

Run the main example module:

```bash
./gradlew :examples:run
```

Useful example files include:

| File | Purpose |
| --- | --- |
| `examples/src/main/java/com/apple/foundationdb/record/sample/Main.java` | Basic record-layer sample entry point. |
| `examples/src/main/java/com/apple/foundationdb/relational/jdbc/examples/ProductManagerEmbedded.java` | Embedded JDBC product-management example. |
| `examples/src/main/java/com/apple/foundationdb/relational/jdbc/examples/ComplexTypesEmbedded.java` | Struct, array, and complex type example. |
| `examples/src/main/java/com/apple/foundationdb/relational/jdbc/examples/BasicSnippets.java` | Basic JDBC query/update examples. |
| `examples/src/main/java/com/apple/foundationdb/relational/jdbc/examples/AdvancedSnippets.java` | Advanced JDBC usage snippets. |

## Tests

Run all tests:

```bash
./gradlew test
```

Run tests for a single module:

```bash
./gradlew :relationaldbx-relational-core:test
```

Run static checks and tests:

```bash
./gradlew check
```

Some tests require a working FoundationDB cluster. Start it first with:

```bash
./docker-local/start.sh
```

## Documentation

Documentation source lives in:

```text
docs/sphinx/source
```

Build the Sphinx documentation:

```bash
./gradlew sphinxDocs
```

Important documentation files:

| File | Description |
| --- | --- |
| `docs/sphinx/source/GettingStarted.md` | Getting started guide. |
| `docs/sphinx/source/Overview.md` | RelationalDBX overview and concepts. |
| `docs/sphinx/source/SQL_Reference.md` | SQL reference entry point. |
| `docs/sphinx/source/SchemaEvolution.md` | Schema evolution notes. |
| `docs/sphinx/source/Building.md` | Development/build setup. |
| `docs/sphinx/source/FAQ.md` | Common questions. |

## Common Gradle Commands

| Command | Description |
| --- | --- |
| `./gradlew clean` | Remove generated build outputs. |
| `./gradlew build` | Build all modules. |
| `./gradlew package` | Create module package artifacts. |
| `./gradlew test` | Run tests. |
| `./gradlew check` | Run checks and tests. |
| `./gradlew :examples:run` | Run the examples module. |
| `./gradlew :relationaldbx-relational-cli:installDist` | Build CLI distribution. |
| `./gradlew :relationaldbx-relational-server:installDist` | Build server distribution. |
| `./gradlew sphinxDocs` | Build documentation. |

## Development Notes

- The root project name is `relationaldbx`.
- The project version is defined in `gradle.properties`.
- Java source and Javadoc are configured to use UTF-8.
- Build output is configured under `.out` instead of the default `build` directory for modules.
- Local FoundationDB configuration is generated by `docker-local/start.sh`.
- The default FoundationDB API version is configured in `gradle.properties`.
- The remote relational server exposes gRPC and an HTTP metrics endpoint.

## Troubleshooting

### Gradle cannot download dependencies

Check that your internet connection is working, then retry:

```bash
./gradlew --refresh-dependencies build
```

### FoundationDB connection fails

Start or restart the local FoundationDB container:

```bash
./docker-local/stop.sh
./docker-local/start.sh
```

Confirm that the generated cluster file exists:

```bash
cat run/docker.cluster
```

### Permission denied when running scripts

Make scripts executable:

```bash
chmod +x gradlew docker-local/*.sh
```

### Server port already in use

Run the server with different ports:

```bash
./relationaldbx-relational-server/.out/install/relationaldbx-relational-server/bin/relationaldbx-relational-server \
  --clusterFile run/docker.cluster \
  --grpcPort 7250 \
  --httpPort 7251
```
