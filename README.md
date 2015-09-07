# unexport
Tool to remove unused identifiers from go-packages

This was my entry to 5th go challenge (http://golang-challenge.com)

# Description
unexport searches unnecessarily exported identifiers from a package.
Identifiers are declared unnecessarily exported, if no-one outside the declaring
package is using them. This can't be 100% guaranteed for other than "internal"-packages,
so by default only "internal"-packages can be unexported.

Unexport candidates are provided as "gorename"-commands. Possible naming collisions caused by
unexporting are also reported.

# Usage
unexport -pkg &lt;target-package&gt; [-search &lt;search-from-package&gt;] [-unsafe] [-offset] [-help] [-report]

Flags:
* -help: print this help
* -offset: use 'file offset'-notation instead of 'from'-notation for gorename
* -pkg &lt;string&gt;: go package to unexport
* -report: show which exported identifiers are used and by whom
* -search &lt;string&gt;: search usage of exported identifiers from this package (and its subpackages) NOTE: If this has not been specified, whole $GOPATH will be searched (and it might take a while).
* -unsafe: allow unexporting other than internal packages

# Examples
unexport -pkg cmd/compile/internal/gc

unexport -pkg cmd/compile/internal/gc -search cmd/compile/internal/big

unexport -pkg cmd/compile/internal/gc -report

unexport -pkg cmd/vet -search cmd/fix -unsafe -offset
