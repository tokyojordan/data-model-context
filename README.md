# Data Model Context

Generate Appian record type context markdown from recordTypeHaul XML exports.

## What this does

This repo includes two scripts that parse Appian recordTypeHaul XML and produce a markdown reference with:
- record type reference
- fields and field references
- relationships and relationship references
- record actions and action references

## Requirements

- Python 3.x

## Scripts

### Single XML file

`xml_to_appian_recordtype_md.py` converts one XML file to one markdown file.

```bash
python xml_to_appian_recordtype_md.py path\to\record.xml
```

Optional flags:
- `-o` / `--out`: output markdown path (defaults to `<input>.md`)
- `--title`: H1 title override

Example:

```bash
python xml_to_appian_recordtype_md.py recordtype-xml\example.xml -o out\example.md --title "Example Record Type Context Reference"
```

### Directory of XML files or Zipped Appian Application Export

`map_xml_to_appian_recordtype_md.py` converts all `*.xml` files from either a directory or a zipped Appian application export to markdown files.

**For a directory:**
```bash
python map_xml_to_appian_recordtype_md.py recordtype-xml
```

**For a zipped Appian application export:**
```bash
python map_xml_to_appian_recordtype_md.py path\to\application-export.zip
```

Optional flags:
- `-o` / `--output_dir`: output directory (defaults to the input directory for directories, or current directory for zip files)
- `-f` / `--folder`: specific folder path within the zip file to search for recordType XML files (only used when input is a zip file)

Output filenames follow the pattern:

```
data-model-context-<record_type_name_in_snake_case>.md
```

## Input format

The scripts expect Appian recordTypeHaul XML exports. If a file does not contain a `<recordType>` element, it will be skipped with an error message.

## Output format

The generated markdown includes `<available_record_types>` and per-record tags to make the output easy to parse or embed in other documentation.

## Notes

- Data types are normalized to friendly names (for example, `Int` and `Long` map to `Integer`).
- Relationship types are normalized to `one-to-many`, `many-to-one`, `one-to-one`, or `many-to-many` when possible.