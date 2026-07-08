```toml
[[language]]
name = "python"
language-servers = [ "pylsp" ]

[language-server.pylsp]
command = "pylsp"

[language-server.pylsp.config.pylsp.plugins]
jedi = { extra_paths = [ "src/app" ] }
```
