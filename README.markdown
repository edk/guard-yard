# Guard::Yard

Guard::Yard allows you to automatically run and update your local YARD Documentation Server. It aims to centralize your file monitoring to guard instead of using the `yard server --reload` command which can be unreliable and provides little control over the generated documentation. Guard::Yard monitors files and updates only the documentation than changes, as opposed to generating the entire documentation suite. That means that changes to your documentation are available sooner!

## Requirements

* The [YARD](http://yardoc.org) documentation tool.
* The [Guard](https://github.com/guard/guard) rubygem.
* Ruby 1.9.2 or higher.

## Install

Add guard-yard to your Gemfile (inside development group):

    gem 'guard-yard'

Install or update your bundle:

    bundle install

Add the default guard-yard definition to your Guardfile:

    guard init yard

## Guardfile

Please read the [Guardfile DSL documentation](https://github.com/guard/guard#readme) for additional information.

Guard::Yard automatically detects changes in your app, lib and ext directories, but you can have it monitor additional files using the Guardfile DSL.

Also note that you may want to ignore the files changed by yard, otherwise guard may output the files and
directories that are being watched/changed.

```
ignore(%r{^doc/})
ignore(%r{^\.yardoc/})
```

Guard::Yard also provides some basic options for doc generation and running the YARD server.

    guard 'yard', :port => '8808' do
      ...
    end

Available options:

    :server => true         # Disable/Enable server
    :port => '8808'         # Port on which the server shoud run.
    :host => 'localhost'    # Host to which the server should bind.
    :stdout => 'yard.log'   # File in which to log the yard server output.
    :stderr => '/dev/null'  # File in which to log the yard server errors.
    :cli => '--plugin rest' # Additional command line options to be appended to the server command.

## Clean-Slate Documentation

To generate or re-create documentation from a clean-slate, run the following command:

    rm -rf .yardoc && yard doc

When booting guard, Guard::Yard will do this for you automatically if no .yardoc directory is present. Once guard is running you can execute this command by using the `Ctrl-\` key combination as well.


## Troubleshooting

If you are running into issues, try re-creating your documentation using `rm -rf .yardoc && yard doc`. Once this operation is complete, restart guard. If you are still having problems, open a new issue in the GitHub issue tracker for this project.

## Build Status [![Build Status](https://app.travis-ci.com/panthomakos/guard-yard.svg?branch=master)](https://secure.travis-ci.org/panthomakos/guard-yard.svg?branch=master)
