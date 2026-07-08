
```nushell
def main [
  github_input: string,
] {
  let github_input_as_list = $github_input
  | split row (char newline)
  | each { |it|
    $it
    | str trim
    | split row ","
  }
  | flatten
  | each { |it| $it | str trim }
  | where { |it| $it | str length > 0 }
  print $github_input_as_list
}
```

```yaml
jobs:
  some_job:
    # ...
    steps:
      - run: |
        nu main.nu \
          hello \
          world
```
