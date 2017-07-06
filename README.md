# test-recall.vim

test-recall.vim is a vim plugin that is focused centrally around making it
easier to run tests and get feedback appropriately in a the red, green,
refactor cycle.

It handles the normal use cases for running tests. However, it has an
additional killer feature, **recollection**. This means that it will
automatically **recall** the last test that you ran, and allow you to
rerun that test while in implementation code. This saves you the effort
of having to jump back and forth between the test and implementation
code during the red, green, refactor cycle.

## Install

The following is the recommended approach using the vim8's built in package
management. If you aren't using vim8 then upgrade to get the latest goodness.

    cd ~/.vim/
    git submodule add https://github.com/uptech/vim-test-recall.git pack/bundle/start/vim-test-recall
    git add .
    git commit -m "Added vim-test-recall plugin to my setup."

If you are using another method, you are on your own.

## Usage

This plugin exposes a number of functions which are intended be used,
and probably mapped. The breakdown of these functions and what they do
is provided below.

- `RunAllTestsInCurrentTestFile()` - runs all the tests in the current test file
- `RunNearestTest()` - runs the test nearest the cursor
- `RunAllRSpecTests()` - runs all rspec tests across code base
- `RunAllCucumberFeatures()` - runs all cucumber features across code base
- `RunWipCucumberFeatures()` - run all wip'd cucumber features across code base

I personally have the above functions mapped as follows in my
[vimrc](https://github.com/cyphactor/dotvim).

    " Map all the run test calls provided by vim-test-recall
    map <leader>t :call RunAllTestsInCurrentTestFile()<cr>
    map <leader>T :call RunNearestTest()<cr>
    map <leader>a :call RunAllRSpecTests()<cr>
    map <leader>c :call RunAllCucumberFeatures()<cr>
    map <leader>w :call RunWipCucumberFeatures()<cr>

## Configuration

The following are optional configs that if not set have common default fall back
strategies. Any of the following could be set in a similar fashion as
this example in your `vimrc`.

    " set vim-test-recall.vim to use rspec with full backtraces
    let g:vim_test_recall_rspec_command = 'rspec -b'

- `g:vim_test_recall_cucumber_command` - if not set this first attempts to
fall back to `bin/cucumber` if present, after that it falls back to
`zeus cucumber` if `zeus.json is present, after that it falls back to
`script/features` if present, after that it falls back to `bundle exec
cucumber`.

- `g:vim_test_recall_rspec_command` - if not set this first attempts to
fall back to `bin/rspec` if present, after that it falls back to `zeus
test` if `zeus.json` is present, after that it falls back to
`script/test` if present, after that it falls back to `bundle exec
rspec` if `Gemfile` is present, after that it falls back to `rspec`.

- `g:vim_test_recall_snapdragon_command` - if not set this first attempts
to fall back to `bundle exec snapdragon` if `Gemfile` is present, after
that it falls back to `snapdragon`.

## License

Copyright (c) Andrew De Ponte. Distributed under the same terms as Vim itself.
See `:help license`.
