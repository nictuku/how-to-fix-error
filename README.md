Errors

---

How to fix: go: github.com/Sirupsen/logrus@v1.2.0: parsing go.mod: unexpected module path "github.com/sirupsen/logrus"
===

Details:

```
$ go test -v ...
(...)
go: github.com/Sirupsen/logrus@v1.2.0: parsing go.mod: unexpected module path "github.com/sirupsen/logrus"
(...)
go: error loading module requirements
```

Why this happens:

logrus has been updated and the `Sirupsen` name is now `sirupsen`. You may be importing modules that refer to the old name.

How to fix:

If you're using go modules from 1.11+, first try updating the logrus version:

```
go get -u github.com/sirupsen/logrus
```

And try again.

If that doesn't work, you're probably using a package that is not modules-aware and that's using the Sirupsen import path. To overwrite it for all packages built within your project, add this line at the end of your `go.mod` file:

```
replace github.com/Sirupsen/logrus => github.com/sirupsen/logrus v1.2.0
```

---

how to fix: exec: "bzr": executable file not found in $PATH
===

Details:

```
$ go test -v ...
(...)
go: labix.org/v2/mgo@v0.0.0-20140701140051-000000000287: bzr branch --use-existing-dir https://launchpad.net/mgo/v2 . in /home/yves/pkg/mod/cache/vcs/ca61c737a32b1e09a0919e15375f9c2b6aa09860cc097f1333b3c3d29e040ea8: exec: "bzr": executable file not found in $PATH
go: launchpad.net/gocheck@v0.0.0-20140225173054-000000000087: bzr branch --use-existing-dir https://launchpad.net/~niemeyer/gocheck/trunk . in /home/yves/pkg/mod/cache/vcs/f46ce2ae80d31f9b0a29099baa203e3b6d269dace4e5357a2cf74bd109e13339: exec: "bzr": executable file not found in $PATH
go: error loading module requirements
```

Why this happens: bzr is not installed.

How to fix:

if using Ubuntu, `sudo apt-get install -y bzr`
