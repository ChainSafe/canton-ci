# Canton CI/CD

## 1. Install DAML

This action is used to install the DAML SDK in your `$GITHUB_WORKSPACE`

**Usage:**

```yaml
- uses: ChainSafe/canton-ci/.github/actions/install-daml@main
    with:
    # Optional (default to latest stable release)
    sdk_version: "3.4.0-snapshot.20251013.0"
```

You can run the following to verify your installation

```yaml
- name: Verify Daml SDK
    run: |
        daml version
    shell: bash
```

## 2. Install Canton

This action is used to install (Open Source) Canton in your `$GITHUB_WORKSPACE`

**Usage:**

```yaml
- uses: ChainSafe/canton-ci/.github/actions/install-canton@main
    with:
    # Optional (default to latest stable release)
    sdk_version: "3.4.0-snapshot.20251013.0"
```

You can run the following to verify your installation

```yaml
- name: Verify Canton
    run: |
        ./canton-release/bin/canton --version
    shell: bash
```

You can access your Canton installation in `./canton-release/bin/canton`.

## 3. DAML Test

This action is used to test DAML files using `daml test` command using the DAML Sandbox.

**Usage:**

```yaml
- uses: ChainSafe/canton-ci/.github/actions/daml-test@main
    with:
    # Not Required if Project Path is root of repository
      project_path: "intro-1"
```

## 4. DAML Script

This action is used to run DAML Scripts using `daml script` command using a LocalNet Canton Node.

**Usage:**

```yaml
- uses: ChainSafe/canton-ci/.github/actions/daml-script@main
    with:
        # Not Required if Project Path is root of repository
        project_path: "intro-1"

        # Port for the json api
        # Optional (defaults to 7575)
        json_api_port: 7575

        # Port for the ledger api
        # Optional (defaults to 6865)
        ledger_api_port: 6865

        # Connection attempts to the LocalNet Canton Participant Node
        # Optional (defaults to 10)
        connection_attempts: 10

        # Wait time in seconds between each connection attempt
        # Optional (defaults to 5)
        wait_time: 5
```

## Current Known Issues

- Currently Canton Installation is accessible from the installation directory, it should be accessible from anywhere using just the `canton` command.
- At the moment we don’t support **[multi-package](https://docs.daml.com/tools/assistant-build.html#overview)** DAML projects. (multiple projects in one repository)
- Some older Canton versions cause errors when running DAML scripts using a Canton node, this is due to Canton CLI syntax changes with versions.

## Planned Tools

- **Formalize Canton Enterprise**
  At the moment we’ve CI Setup only for Canton Opensource, but Canton also has a private “Enterprise” version. We’ve tested it on CI environment, however we should formalize it for reusability and configurability.
- **Canton LocalNet Participant Node Deployment**
  We think deploying a participant node is a valid use case for a Collaborative Development Environment (like a common Anvil instance or a development backend). We can streamline the process using a GitHub Action that can be triggered manually.
- **On-chain DAML Smart Contract Watcher/Defender**
  Sort of like OpenZeppelin Defender, a developer security platform to code, audit, deploy, monitor, and operate blockchain applications with confidence.
- **Marketplace**
  Publish these Actions on GitHub Marketplace for easier access and usage.
