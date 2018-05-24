**prescient.el:** simple but effective sorting and filtering for
Emacs.

## Summary

`prescient.el` is a library which sorts and filters lists of
candidates, such as appear when you use a package like [Ivy] or
[Company]. Extension packages such as `ivy-prescient.el` and
`company-prescient.el` adapt the library for usage with various
frameworks.

As compared to other packages which accomplish similar tasks,
including [IDO], [Ivy], [Helm], [Smex], [Flx], [Historian], and
[Company-Statistics], `prescient.el` aims to be simpler, more
predictable, and faster.

## Installation

`prescient.el` is not yet registered on MELPA. As such, you will need
to run it from source. You can do this using
[`straight.el`][straight.el] as follows:

    (straight-use-package
     '(prescient :host github :repo "raxod502/prescient.el"))

You may also use any other package manager which allows you to install
and run packages from source, or install the package manually.

## Usage

To cause [Ivy] to use `prescient.el` sorting and filtering, enable
`ivy-prescient-mode`. To cause [Company] to use `prescient.el`
sorting, enable `company-prescient-mode`. To cause your usage
statistics to be saved between Emacs sessions, enable
`prescient-persist-mode`.

## Algorithm

`prescient.el` takes as input a list of candidates, and a query that
you type. The query is first split on spaces into subqueries (two
consecutive spaces match a literal space). Each subquery filters the
candidates because it must match as either a substring of the
candidate or as an initialism (e.g. `ffap` matches
`find-file-at-point`, and so does `fa`). The last few candidates you
selected are displayed first, followed by the most frequently selected
ones, and then the remaining candidates are sorted by length.

## Configuration

* `prescient-history-length`: The number of recently selected
  candidates that are remembered and displayed at the top of the list.

* `prescient-frequency-decay`: `prescient.el` keeps a "frequency" for
  each selected candidate, which is incremented by one each time you
  select the candidate. To keep things tidy, frequencies are
  multiplied by this variable's value each time you select a new
  candidate, so they decrease over time.

* `prescient-frequency-threshold`: Once the frequency for an
  infrequently used command falls below the value of this variable,
  `prescient.el` forgets about it.

* `prescient-save-file`: Where to save statistics that are persisted
  between Emacs sessions when `prescient-persist-mode` is active. The
  default value follows the conventions of
  [`no-littering`][no-littering].

* `ivy-prescient-excluded-commands`: Some commands, like `swiper`,
  don't benefit from `prescient.el` sorting, so their usage statistics
  just pollute the save file. You can tell `prescient.el` about them
  here.

* `ivy-prescient-sort-commands`: Some [Counsel] commands, like
  `counsel-find-library`, intentionally disable sorting for their
  candidates. You can override this preference and re-enable sorting
  by adding such commands here. (To check if a command disables
  sorting, inspect its source code and see if it calls `ivy-read` with
  a nil value for the `:sort` keyword argument.)

[company]: https://github.com/company-mode/company-mode
[company-statistics]: https://github.com/company-mode/company-statistics
[counsel]: https://github.com/abo-abo/swiper#counsel
[flx]: https://github.com/lewang/flx
[helm]: https://github.com/emacs-helm/helm
[historian]: https://github.com/PythonNut/historian.el
[ido]: https://www.gnu.org/software/emacs/manual/ido.html
[ivy]: https://github.com/abo-abo/swiper#ivy
[no-littering]: https://github.com/emacscollective/no-littering
[smex]: https://github.com/nonsequitur/smex
[straight.el]: https://github.com/raxod502/straight.el
