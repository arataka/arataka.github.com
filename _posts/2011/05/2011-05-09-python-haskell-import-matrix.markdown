---
layout: post
title: Python と Haskell の import の書き方対応表
---

# {{ page.title }} #

| Python                            | Haskell                        |
| --------------------------------- | ------------------------------ |
| `from Module import *`            | `import Module`                |
| `from Module import func1, func2` | `import Module (func1, func2)` |
|                                   | `import Module hiding (func)`  |
| `import Module`                   | `import qualified Module`      |
| `import Module as M`              | `import qualified Module as M` |

かな?
([Learn You a Haskell for Great Good! - Modules](http://learnyouahaskell.com/modules))
