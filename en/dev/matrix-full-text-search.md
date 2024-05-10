# Full text search implementation on matrix based messengers

## Synapse

### Overview

* https://github.com/matrix-org/synapse/blob/c1ddbbde4fb948cf740d4c59869157943d3711c6/synapse/storage/databases/main/search.py#L50
* https://www.postgresql.org/docs/9.1/textsearch-controls.html
* https://rob.conery.io/2019/10/29/fine-tuning-full-text-search-with-postgresql-12/

> sql = ( "INSERT INTO event_search" " (event_id, room_id, key, vector, stream_ordering, origin_server_ts)" " VALUES (?,?,?,to_tsvector('english', ?),?,?)"

### Stopwords

* These words are ignored in both messages and your query:
* https://www.postgresql.org/docs/9.1/textsearch-dictionaries.html#TEXTSEARCH-STOPWORDS
* https://github.com/postgres/postgres/blob/master/src/backend/snowball/stopwords/english.stop

### Stemming

* It supports a kind of dumb and buggy stemming by default (that also returns `Paris` for `pari`)
* https://www.postgresql.org/docs/13/textsearch-dictionaries.html#TEXTSEARCH-SIMPLE-DICTIONARY
* https://github.com/postgres/postgres/blob/master/src/backend/snowball/libstemmer/stem_UTF_8_english.c

### Tokenizer

* Rules for breaking down text into searchable words. Mainly (`[0-9a-zA-Z_-]+`) is considered a word (`man isalnum`)
* https://github.com/postgres/postgres/blob/c30f54ad732ca5c8762bb68bbe0f51de9137dd72/src/backend/tsearch/wparser_def.c#L449
* Certain foreign language Unicode characters and lots of different zero width combiners are also considered part of the word
* https://github.com/postgres/postgres/blob/c30f54ad732ca5c8762bb68bbe0f51de9137dd72/src/backend/tsearch/wparser_def.c#L678

### Irregular words

Hyphens are specially supported: they don't completely break the word, but any subpart of a hyphenated word will also become searchable itself, along with the entire amalgamation and any continuous subsequence of hyphen-delimited words within it.

* https://www.postgresql.org/docs/13/textsearch-parsers.html
* https://stackanswers.net/questions/postgresql-full-text-search-tokenizer

A strict syntax subset of certain special token types are handled, such as email address, URL, host, scientific notation, version number (also fits IPv4 address), decimal numbers and file path. Whitespace, the protocol of a URI, XML tags and XML entities are explicitly ignored.

You can only index and search for email of the form `([0-9a-zA-Z_./-]+@)+host.domain.tld`. Any other character, such as a `:` is treated as a token delimiter. Accents are disallowed, otherwise the local part and the domain will be indexed separately.

Local file paths are roughly composed of words (`.` and accents usually allowed) separated by `/`. It may also contain `~`, but only in the beginning or right after a `/`.

In practical terms, certain characters surrounded by alphanumeric characters amalgamate the whole string into a single word if they resemble one of the above listed special token types. For normal text, this is roughly: `^([0-9a-zA-Z_]|[0-9a-zA-Z_/][0-9a-zA-Z_/@.-]?([0-9a-zA-Z_/.-][0-9a-zA-Z_/@.-]?)*([0-9a-zA-Z_])$`.

### URL

Only URL obeying strict syntax is indexed, but the allowed character set is much wider than word characters in any other token. You can only search for it either in full or separately for its domain part and its trailing path part including the leading `/` (but only indexed if the trailing part honors the local file path syntax itself!). The domain part must contain at least one dot. When searching, you mustn't type in its protocol - i.e., start it with the domain name. The following characters are explicitly disallowed in code:

```
"<>\\^`{|}
```

The following characters don't seem to work either in practice: `!&:()`. The overall approximate range of characters allowed in the URL path, query and anchor is thus: `[][#$%'*+,./0-9;=?@A-Z_a-z~-]` Note that you can percentile encode a URL before submission for indexing, but servers will have difficulties with `&`. If the trailing part contains invalid characters, only the domain will be indexed.

### Query

* a search returns exactly those messages which contain all of the search words listed in the query
* putting words in quotation marks works to search for phrases

### Edits

As of 2024, Synapse can only find text present in the original message, not any newer edited version.

* https://github.com/element-hq/synapse/issues/8686
* https://github.com/element-hq/synapse/issues/17118
