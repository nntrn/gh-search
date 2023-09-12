# gh-search

## Usage

WIP

## Examples

Search github for files that isn't owned by you that contain your username (hopefully your username isn't something common)

```sh
gh-search --content nntrn --not --user nntrn --out /tmp/github_nntrn
cd /tmp/github_nntrn
grep -r nntrn .
```

Save files that contain `kona_player_info` to `/tmp/kona_player_info`

```sh
gh-search --content kona_player_info --out /tmp/kona_player_info
```

https://docs.github.com/en/rest/search/search
