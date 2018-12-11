Errors

---

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
