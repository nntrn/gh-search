# gh-search

## Usage

```sh
export GITHUB_TOKEN=..

gh-search --search [SEARCH_TERM] \
  --language [LANGUAGE] \
  --user [USER] \
  --org [ORG] \
  --repo [REPO] \
  --extension [EXT] \
  --per-page [NUM] \
  --path [PATH] \
  --out [DIR]
```

## Examples

- Find instances of **api** in **json** files that isn't **package.json**

  ```sh
  gh-search --search api --language json --not --filename package.json
  ```

- Find references of **api.github.com** in **shell** scripts owned by **github**

  ```sh
  gh-search --search api.github.com --language shell --org github
  ```

- Search **jq** files that **def**ine functions and output first **10** to **/tmp/jq**

  ```sh
  gh-search --search def --extension jq --per-page 10 --out /tmp/jq
  ```

- Find instances of **episode** in **json** and **csv** fields that don't contain **/locales/**

  ```sh
  gh-search --search episode --language json --or --language csv --not --path "/locales/" --out /tmp/data/tv
  ```

- **Search github for files that mention your username that isn't owned by you**  
  (hopefully your username isn't something common)

  ```sh
  gh-search --search nntrn --not --user nntrn --out /tmp/github_nntrn
  cd /tmp/github_nntrn
  grep -r nntrn .
  ```

## Github Code Search Factsheet

Due to the complexity of searching code, there are a few restrictions on how searches are performed:

- Only the default branch is considered. In most cases, this will be the master branch.
- Only files smaller than 384 KB are searchable.
- You must always include at least one search term when searching source code. For example, searching for language:go is not valid, while amazing language:go is.

## Considerations

- By default, bare search terms search both paths and file content.

- Except with `filename` searches, you must always include at least one search term  
  (i.e. **q=language:javascript** is not valid but **q=football+language:javascript** is ok)

- `GITHUB_TOKEN` is required to search code

- Code in forks is only searchable if the fork has more stars than the parent repository

- Only the **default branch** is indexed for code search

- Only files smaller than 384 KB are searchable

- Up to 4,000 private repositories are searchable

- Only repositories with fewer than 500,000 files are searchable

- You can't use the following wildcard characters as part of your search query:  
  `` . , : ; / \ ` ' " = * ! ? # $ & + ^ | ~ < > ( ) { } [ ] @ ``

  | This search                 | Finds repositories with…                                                |
  | --------------------------- | ----------------------------------------------------------------------- |
  | `curl repo:nntrn/bookstand` | Find all instances of curl in nntrn/bookstand                           |
  | `shogun user:heroku`        | Find references to shogun from all public heroku repositories.          |
  | `join extension:coffee`     | Find all instances of join in code with coffee extension.               |
  | `system size:>1000`         | Find all instances of system in code of file size greater than 1000kbs. |
  | `examples path:/docs/`      | Find all examples in the path /docs/.                                   |
  | `replace fork:true`         | Search replace in the source code of forks.                             |

## References

- https://docs.github.com/en/rest/search/search
- https://docs.github.com/en/search-github/searching-on-github/searching-code
- https://docs.github.com/en/search-github/getting-started-with-searching-on-github/understanding-the-search-syntax
- https://github.com/search/advanced
- https://docs.github.com/en/free-pro-team@latest/rest/search/search?apiVersion=2022-11-28#search-code
