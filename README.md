# bfg-sensitive-data

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

## Resultado

```
Using repo : /Users/vcamaral/Code/sensitive-data.git

Found 2 objects to protect
Found 2 commit-pointing refs : HEAD, refs/heads/master

Protected commits
-----------------

These are your protected commits, and so their contents will NOT be altered:

 * commit ff083f04 (protected by 'HEAD')

Cleaning
--------

Found 2 commits
Cleaning commits:       100% (2/2)
Cleaning commits completed in 107 ms.

Updating 1 Ref
--------------

	Ref                 Before     After
	---------------------------------------
	refs/heads/master | ff083f04 | 2812aa1d

Updating references:    100% (1/1)
...Ref update completed in 47 ms.

Commit Tree-Dirt History
------------------------

	Earliest      Latest
	|                  |
	    D         m

	D = dirty commits (file tree fixed)
	m = modified commits (commit message or parents changed)
	. = clean commits (no changes to file tree)

	                        Before     After
	-------------------------------------------
	First modified commit | 6b5a31d1 | 96279fb8
	Last dirty commit     | 6b5a31d1 | 96279fb8

Changed files
-------------

	Filename     Before & After
	--------------------------------
	config.txt | 50e26069 ⇒ 692a2653


In total, 3 object ids were changed. Full details are logged here:

	/Users/vcamaral/Code/sensitive-data.git.bfg-report/2018-12-10/15-02-41

BFG run is complete! When ready, run: git reflog expire --expire=now --all && git gc --prune=now --aggressive


--
You can rewrite history in Git - don't let Trump do it for real!
Trump's administration has lied consistently, to make people give up on ever
being told the truth. Don't give up: https://www.rescue.org/topic/refugees-america
--
```

![](https://github.com/vcamaral/sensitive-data/blob/master/images/history.png)

Referências:
- https://help.github.com/articles/removing-sensitive-data-from-a-repository/
