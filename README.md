# lsp-intellij [![MELPA](https://melpa.org/packages/lsp-rust-badge.svg)](https://melpa.org/#/lsp-intellij)
Emacs client for [lsp-intellij-server](https://github.com/Ruin0x11/intellij-lsp-server).

## Requirements
- `lsp-mode` 4.1
  + If you get errors like `void-function` trying to load the client code (`lsp-intellij.el`), be sure your version of `lsp-mode` is up-to-date.

### Optional requirements
- `flycheck`
- `lsp-ui`
- `company` and `company-lsp`
- `kotlin-mode`

## Setup
Install the package from MELPA. Then load `lsp-mode` in your config and put the following hook afterward:
```emacs-lisp
(progn
  (add-to-list 'load-path "~/.emacs.d/elpa/dash-20200119.2310/")
  (add-to-list 'load-path "~/.emacs.d/elpa/dash-functional-20191109.1327/")
  (add-to-list 'load-path "~/.emacs.d/elpa/markdown-mode-20200413.2232/")
  (add-to-list 'load-path "~/.emacs.d/elpa/s-20180406.808/")
  (add-to-list 'load-path "~/src/reading/lsp-mode/")
  (require 'lsp-mode)
  (add-to-list 'load-path "~/src/reading/lsp-intellij")
  (with-eval-after-load 'lsp-mode
    (require 'lsp-intellij)
    (add-hook 'java-mode-hook #'lsp-intellij-enable))
  (add-to-list 'load-path "~/.emacs.d/elpa/company-20200324.2145/")
  (require 'company)
  (add-to-list 'load-path "~/src/reading/company-lsp")
  (add-to-list 'load-path "~/.emacs.d/elpa/flycheck-20200405.2310")
  (add-to-list 'load-path "~/src/reading/lsp-ui")
  (require 'lsp-ui)
  (add-hook 'lsp-after-open-hook #'lsp-ui-mode)

  (require 'company-lsp)
  (setq company-lsp-enable-snippet t
        company-lsp-cache-candidates t)
  (push 'company-lsp company-backends)
  (push 'java-mode company-global-modes))


```
Finally, start IntelliJ with the [server plugin](https://github.com/Ruin0x11/intellij-lsp-server), then visit a `.java` file tracked by a project you've previously opened in IDEA.

You can enable Kotlin support by installing `kotlin-mode`, then adding another hook for `lsp-intellij-enable` in `kotlin-mode-hook`.

For features like diagnostics and snippet completion, `lsp-ui` and `company-lsp` are required. Here are the respective config options for each.
```emacs-lisp
(require 'lsp-ui)
(add-hook 'lsp-after-open-hook #'lsp-ui-mode)

(require 'company-lsp)
(setq company-lsp-enable-snippet t
      company-lsp-cache-candidates t)
(push 'company-lsp company-backends)
(push 'java-mode company-global-modes)
(push 'kotlin-mode company-global-modes) ;; if using Kotlin
```

### Spacemacs layer
See [here](https://github.com/Ruin0x11/lsp-intellij-spacemacs).
