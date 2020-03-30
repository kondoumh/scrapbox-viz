# scrapbox-viz

scrapbox-viz (sbv) is a CLI to fetch data and visualize Scrapbox projects.

- Fetch page data (JSON format)
- Aggregate user activities (pages created, views of created page, etc.)
- Generate graph data (as GraphViz dot file)

## Initialize working directory
Data fetched via Scrapbox APIs will be stored in an existing working directory.

If you create `.sbv.yaml` at `${HOME}` and write path in th entry `workdir`, it will be set to that path.

```yaml
workdir: path/to/workdir
```

If the directory does not exist, it will be created.

Of cource, you can specify the directory every time you execute sub commands with global -d(--workdir) flag.

```
$ sbf fetch -p <project name> -d <path/to/workdir>
```

## Fetch page data of the project
Fetch page data of the Scrapbox project via [Scrapbox APIs](https://scrapbox.io/help-jp/API).

- Page list data will be saved as JSON file at `<WorkDir>/<project name>.json`.
- Each Page data will be saved as JSON file in `<WorkDir>/<project name>`.
  - The file name consists of the page ID.

```
$ sbf fetch -p <project name>
```

## Aggregate user activites in the project
Parse page data and aggregate activities of the project per user.

- Pages created
- Pages contributed
- Views of created page
- Links of created page

```
$ sbf aggregate -p <project name>
```

CSV will be created at `<WorkDir>/<project name>.csv`.

## Generate graph of the pages and users
Parse page data and generate graph of pages and users.

-  -a, --anonymize        Anonymize user
-  -i, --include          Include user node
-  -p, --project string   Name of Scrapbox project (default "help-jp")
-  -t, --threshold int    Threshold value of views to filter page

```
$ sbf graph -p <project name>
```

If you want to include user node to the graph, specify -i(--include) flag.

```
$ sbf graph -p <project name> -i=true
```

If you want to annonymize user name of user node, specify -a(--anonymize) flag.

```
$ sbf graph -p <project name> -i=true -a=true
```

You can reduce number of nodes in the graph by specifying page views as threshold value.

```
$ sbf graph -p <project name> -t 100
```

GraphViz dot file will be created at `<WorkDir>/<project name>.dot`.
