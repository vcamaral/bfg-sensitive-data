# sensitive-data

Exemplo de remoção de dado sensível do histórico do GitHub com a ferramenta [BFG](https://rtyley.github.io/bfg-repo-cleaner/).

## Utilização

```
git clone git@github.com:vcamaral/sensitive-data.git --mirror
echo 123456 > passwords.txt
bfg --replace-text passwords.txt sensitive-data.git
cd sensitive-data.git
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push
```

Referências:
- https://help.github.com/articles/removing-sensitive-data-from-a-repository/
