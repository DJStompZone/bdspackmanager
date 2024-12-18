# BdsPackManager

**BdsPackManager** is a command-line tool designed for managing resource and behavior packs on a Minecraft Bedrock Dedicated Server (BDS). It allows you to easily add, validate, update, and manage packs, ensuring your server is always up-to-date with the latest content.

## Features

- **Add Packs**: Supports adding `.mcpack`, `.mcaddon`, and directories containing valid `manifest.json` files.
- **Automatic Unzipping**: Automatically extracts and processes `.mcpack` and `.mcaddon` files.
- **Validation**: Ensures consistency between the packs listed in your server's configuration files and the actual content in the `resource_packs` and `behavior_packs` directories.
- **Version Updates**: Update the `@minecraft/server` dependency version in `behavior_packs` manifests to ensure compatibility with your server version.
- **Selective Updates**: Use `--update-only` to update versions for packs in a specific folder, including `.mcpack` files.
- **Configurable**: Specify the server directory using command-line arguments, a `.env` file, or `~/.bdspackrc` for a global configuration.
- **Interactive or Automatic**: Prompt for overwrites or use the `--force` flag to skip confirmation and automate updates.

## Installation

1. **Install via pip**:

    ```bash
    pip install bdspackmanager
    ```

2. **Set up your environment**:
    - Optionally, create a `.env` file in your project directory or a `~/.bdspackrc` file for global configuration:

      ```yaml
      BDS_DIRECTORY=/path/to/your/bedrock_server
      ```

    - The tool prioritizes the following configuration sources:
      1. Command-line arguments
      2. Environment variables from `.env` in the project directory
      3. Environment variables from `~/.bdspackrc`

## Usage

### Command-line Arguments

```bash
python -m bdspackmanager [OPTIONS] [PACKS...]
```

#### Options

- `PACKS...`: One or more paths to `.mcpack`, `.mcaddon`, or directories containing a valid `manifest.json`.
- `--bds-dir`: Specify the path to the Bedrock Dedicated Server directory (overrides `.env` and `~/.bdspackrc`).
- `--validate`: Validate and rescan JSON files for consistency with the actual content in the `resource_packs` and `behavior_packs` directories.
- `--update`: Update `@minecraft/server` dependency versions in all `behavior_packs`.
- `--update-only <dir>`: Update `@minecraft/server` dependency versions for packs in the specified folder, including `.mcpack` files.
- `--version <version>`: Specify the target version for `@minecraft/server` when using `--update` or `--update-only`.
- `--force`: Skip confirmation prompts when overwriting existing packs.

### Example Usage

1. **Adding a Pack**:

   ```bash
   python -m bdspackmanager /path/to/your_pack.mcpack 
   ```

2. **Validating Pack Consistency**:

   ```bash
   python -m bdspackmanager --validate 
   ```

3. **Updating All Behavior Packs**:

   ```bash
   python -m bdspackmanager --update --version "1.16.0-beta" 
   ```

4. **Updating Packs in a Specific Folder**:

   ```bash
   python -m bdspackmanager --update-only /path/to/pack_folder --version "1.16.0-beta"
   ```

---

### Global Configuration Support

BdsPackManager supports global configuration through the `~/.bdspackrc` file. This file behaves like `.env` and allows you to set environment variables for the tool. For example:

```bash
BDS_DIRECTORY=/path/to/your/bedrock_server
```

When present, `~/.bdspackrc` is automatically loaded and used as a fallback if a `.env` file is not found in the project directory. You can override these settings with command-line arguments.
