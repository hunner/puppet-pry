Puppet `pry()` debugging function
=================================

When compiling puppet manifests it is often frustrating to find subtle variable
parsing or ordering problems. Introspecting specific resource parameters at a
given point is also difficult. This function makes those two tasks easier by
using [pry](http://pryrepl.org/).

Simply `gem install pry` and call `pry()` at some point during a catalog
compile by adding it to the specific line in a manifest where you would like to
inspect the compilation state, and run the process doing the compilation in the
foreground. Puppet will drop into a debugging shell in the
`Puppet::Parser::Scope` object at the time of the function call. A few helpful
tips will be printed when the shell is first entered.

When used in manifests during [rspec-puppet](http://rspec-puppet.com/) compilation, the pry REPL will appear in the shell running the spec tests. When used with a puppet master, the master process must be run in the forground with `puppet master --no-daemonize --verbose` to view the debug shell. If a daemonized master process enters the debug shell, `kill` must be used to exit the debug shell.

Please see the documentation on
[`Puppet::Parser::Scope`](https://github.com/puppetlabs/puppet/blob/master/lib/puppet/parser/scope.rb)
and
[`Puppet::Resource::Catalog`](https://github.com/puppetlabs/puppet/blob/master/lib/puppet/resource/catalog.rb)
for relevant method calls.
