# gh-search

## Usage

WIP

## Examples

- Search for **shell** scripts owned by **github** that contain **api.github.com**

  ```sh
  gh-search --search api.github.com --language shell --org github
  ```

- Search and save **10** **.jq** files to **/tmp/jq**

  ```sh
  gh-search --search jq --extension jq --per-page 10 --out /tmp/jq
  ```

- **Search github for files that mention your username that isn't owned by you**  
  (hopefully your username isn't something common)

  ```sh
  gh-search --search nntrn --not --user nntrn --out /tmp/github_nntrn
  cd /tmp/github_nntrn
  grep -r nntrn .
  ```

## Considerations

- You must be signed into a personal account on GitHub to search for code across all public repositories.

- Code in forks is only searchable if the fork has more stars than the parent repository.
  Forks with fewer stars than the parent repository are not indexed for code search.
  To include forks with more stars than their parent in the search results,
  you will need to add `fork:true` or `fork:only` to your query.

- Only the _default branch_ is indexed for code search.

- Only files smaller than 384 KB are searchable.

- Up to 4,000 private repositories are searchable. These 4,000 repositories will be the most recently
  updated of the first 10,000 private repositories that you have access to.

- Only repositories with fewer than 500,000 files are searchable.

- Only repositories that have had activity or have been returned in search results in the last year are searchable.

- Except with `filename` searches, you must always include at least one search term when searching source code. For example, searching for [language:javascript](https://github.com/search?utf8=%E2%9C%93&q=language%3Ajavascript&type=Code&ref=searchresults) is not valid, while [amazing language:javascript](https://github.com/search?utf8=%E2%9C%93&q=amazing+language%3Ajavascript&type=Code&ref=searchresults) is.
- At most, search results can show two fragments from the same file, but there may be more results within the file.
- You can't use the following wildcard characters as part of your search query: `` . , : ; / \ ` ' " = * ! ? # $ & + ^ | ~ < > ( ) { } [ ] @ ``. The search will simply ignore these symbols.

## References

- https://docs.github.com/en/rest/search/search
- https://docs.github.com/en/search-github/searching-on-github/searching-code
