(aliases)=
# Model aliases

LLM supports model aliases, which allow you to refer to a model by a short name instead of its full ID.

## Listing aliases

To list current aliases, run this:

```bash
llm aliases
```
Example output:

<!-- [[[cog
from click.testing import CliRunner
from llm.cli import cli
result = CliRunner().invoke(cli, ["aliases", "list"])
cog.out("```\n{}```".format(result.output))
]]] -->
```
3.5                 : gpt-3.5-turbo
chatgpt             : gpt-3.5-turbo
chatgpt-16k         : gpt-3.5-turbo-16k
3.5-16k             : gpt-3.5-turbo-16k
4                   : gpt-4
gpt4                : gpt-4
4-32k               : gpt-4-32k
gpt-4-turbo-preview : gpt-4-turbo
4-turbo             : gpt-4-turbo
4t                  : gpt-4-turbo
4o                  : gpt-4o
3.5-instruct        : gpt-3.5-turbo-instruct
chatgpt-instruct    : gpt-3.5-turbo-instruct
ada                 : ada-002 (embedding)
```
<!-- [[[end]]] -->

Add `--json` to get that list back as JSON:

```bash
llm aliases list --json
```
Example output:
```json
{
    "3.5": "gpt-3.5-turbo",
    "chatgpt": "gpt-3.5-turbo",
    "chatgpt-16k": "gpt-3.5-turbo-16k",
    "3.5-16k": "gpt-3.5-turbo-16k",
    "4": "gpt-4",
    "gpt4": "gpt-4",
    "4-32k": "gpt-4-32k",
    "ada": "ada-002"
}
```

## Adding a new alias

The `llm aliases set <alias> <model-id>` command can be used to add a new alias:

```bash
llm aliases set turbo gpt-3.5-turbo-16k
```
Now you can run the `gpt-3.5-turbo-16k` model using the `turbo` alias like this:

```bash
llm -m turbo 'An epic Greek-style saga about a cheesecake that builds a SQL database from scratch'
```
Aliases can be set for both regular models and {ref}`embedding models <embeddings>` using the same command. To set an alias of `oai` for the OpenAI `ada-002` embedding model use this:
```bash
llm aliases set oai ada-002
```
Now you can embed a string using that model like so:
```bash
llm embed -c 'hello world' -m oai
```
Output:
```
[-0.014945968054234982, 0.0014304015785455704, ...]
```

## Removing an alias

The `llm aliases remove <alias>` command will remove the specified alias:

```bash
llm aliases remove turbo
```

## Viewing the aliases file

Aliases are stored in an `aliases.json` file in the LLM configuration directory.

To see the path to that file, run this:

```bash
llm aliases path
```
To view the content of that file, run this:

```bash
cat "$(llm aliases path)"
```