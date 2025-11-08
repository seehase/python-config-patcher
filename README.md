# Config Patcher

This script provides a way to patch configuration files, allowing you to update or add settings without manually editing the original file. It is particularly useful for managing configurations in environments where you need to maintain a base configuration and apply specific changes for different setups.

The script merges a source configuration file with a patch file, applying the following logic:

-   **Update Existing Keys**: If a key from the patch file already exists in the source file, its value will be updated.
-   **Add New Keys**: If a key from the patch file does not exist in the source file, it will be added to the end of its respective section.
-   **Add New Sections**: If a section from the patch file does not exist in the source file, the entire section, including its keys, will be added.

## Usage

To use the script, run it from the command line with the following arguments:

```bash
./config_patcher.py [source_file] [patch_file] -o [output_file]
```

-   `source_file`: The original configuration file.
-   `patch_file`: The file containing the changes to apply.
-   `output_file` (optional): The file to write the patched configuration to. If not provided, the source file will be overwritten.

### Example

```bash
./config_patcher.py source.conf source.conf.patch -o out.conf
```

## Before vs. After

Here is an example of how the script transforms a configuration file.

### `source.conf`

```ini
[Extras]
    [[Header]]
        description =
        keywords = weather,weewx,neowx-material
        current_nav_link = yes
        yesterday_nav_link = yes
```

### `source.conf.patch`

```ini
[Extras]
    [[Header]]
        description = My personal weather station
        new_label = does not exist
```

### `out.conf` (Expected Output)

```ini
[Extras]
    [[Header]]
        description = My personal weather station
        keywords = weather,weewx,neowx-material
        current_nav_link = yes
        yesterday_nav_link = yes
        new_label = does not exist
```
