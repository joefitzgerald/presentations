# [fit] Building An Editor
# [fit] ~~Plugin~~ Package For Go

### **Joe Fitzgerald**, *Director, Cloud Foundry Services @ Pivotal*

---

## Meet Joe

* I work @ ![Pivotal](http://blog.clearpathsg.com/Portals/154661/images/pivotal-logo1-resized-600.png) (http://pivotal.io)
* I sell and deliver professional services for ![Cloud Foundry](https://www.gopivotal.com/assets/images/cf/logo-cf.png)
* You can find me at:
  * ![Github](https://assets-cdn.github.com/images/modules/logos_page/GitHub-Logo.png): [`@joefitzgerald`](https://github.com/joefitzgerald)
  * ![Twitter](https://g.twimg.com/Twitter_logo_blue.png): [`@joefitzgerald`](https://twitter.com/joefitzgerald)
  * ![Pivotal](http://blog.clearpathsg.com/Portals/154661/images/pivotal-logo1-resized-600.png): [jfitzgerald@pivotal.io](mailto://jfitzgerald@pivotal.io)

---

# And...

## [fit] Since March
### [fit] _I've been working on a Go package for Atom_

---

# [fit] I Know What You Are Thinking...

---

# [fit] You Are Crazy

# _Because I ![inline](/Users/jfitzgerald/Projects/presentations/Building An Editor Package For Go/assets/heart.png):_
#### **Vim, Emacs, Sublime, IntelliJ, Eclipse, LiteIDE... Acme (?)**

---

![fit](http://fc06.deviantart.net/fs70/f/2012/329/1/1/bring_all_the_pitchforks__by_palaeorigamipete-d5m49bd.png)

---

# [fit] You're Right
# [fit] _I'm Not Here To Change Your Mind_

---

# [fit] So Why'd You Do It?

---

# [fit] It Was March
# [fit] _And It Sounded Like A Good Idea (?)_

---

# Meet Atom

![right 40%](https://raw.githubusercontent.com/atom/atom/master/resources/atom.png)

* Built By: ![](https://assets-cdn.github.com/images/modules/logos_page/GitHub-Logo.png)
* Find It At: [`atom.io`](https://atom.io)
* License: [`MIT`][os] – Yes, It's Open Source!

![inline](https://atom.io/assets/screenshot-main@2x-284f83cd218bd0521ebe3f4a932b170c.gif)

[os]: http://blog.atom.io/2014/05/06/atom-is-now-open-source.html

---

# [fit] But...

![inline](/Users/jfitzgerald/Projects/presentations/Building An Editor Package For Go/assets/Chromium_11_Wordmark_Logo.png)
+
![inline](http://nodeblog.files.wordpress.com/2011/07/nodejs.png)

# [fit] = Slow, _Right?_

---

![right](https://raw.githubusercontent.com/wiki/facebook/react/react-logo-1000-transparent.png)

# React
## The Default Editor View
## _As Of July 23, 2014_
## **= Much Faster**

---

# [fit] I Created A Package
# [fit] _It's Called: `go-plus`_

---

# [fit] Right Now It Supports:

* Formatting source using `gofmt`
* Formatting and managing imports using `goimports`
* Code quality inspection using `go vet`
* Linting using `golint`
* Syntax checking using `go build` and `go test`
* Display of test coverage using `go test -coverprofile`

---

![](/Users/jfitzgerald/Projects/presentations/Building An Editor Package For Go/assets/atomio-go-plus-package.png)

---

![](/Users/jfitzgerald/Projects/presentations/Building An Editor Package For Go/assets/atomio-go-plus-package-osx.png)

---

![](/Users/jfitzgerald/Projects/presentations/Building An Editor Package For Go/assets/atomio-go-plus-package-windows.png)

---

![](/Users/jfitzgerald/Projects/presentations/Building An Editor Package For Go/assets/github-joefitzgerald-go-plus.png)

---

# A Tour Of _Version 1:_

---

![fit](https://camo.githubusercontent.com/dfd447388f9d6506dcdd19e6c5c431bf4211e673/687474703a2f2f636c2e6c792f696d6167652f3339327a324c3066304534312f676f2d706c75732d6578616d706c652e676966)

---

# [fit] I Made Some Rookie Mistakes

## [fit] _(But I'm Not So Sure Others Have Realized IT)_

## [fit] [(Because These Seem Like Common Editor Mistakes)]()

---

# [fit] Why Should Someone Have To Configure The Path To Tools?

# [fit] _Like_ `gofmt`

---

# [fit] Wouldn't It Be Better To Use...

# _`go env`_

# ?

---

```bash
$ go env
GOARCH="amd64"
GOBIN=""
GOCHAR="6"
GOEXE=""
GOHOSTARCH="amd64"
GOHOSTOS="darwin"
GOOS="darwin"
GOPATH="/Users/jfitzgerald/go"
GORACE=""
GOROOT="/usr/local/Cellar/go/1.3/libexec"
GOTOOLDIR="/usr/local/Cellar/go/1.3/libexec/pkg/tool/darwin_amd64"
CC="clang"
GOGCCFLAGS="-fPIC -m64 -pthread -fno-caret-diagnostics -Qunused-arguments -fmessage-length=0 -fno-common"
CXX="clang++"
CGO_ENABLED="1"
```

---

```bash
GOBIN=""
  +
GOEXE=""
  +
GOPATH="/Users/jfitzgerald/go"
  +
GOROOT="/usr/local/Cellar/go/1.3/libexec"
  +
GOTOOLDIR="/usr/local/Cellar/go/1.3/libexec/pkg/tool/darwin_amd64"
```

# [fit] Is everything you need to find go tools
# [fit] _(Plus `$PATH` / `%Path%`)_

---

# [fit] So We Just Need To Find

# [fit] _`go`_

---

# Where Is Go, You Ask?

1. Start With _`$PATH` / `%PATH%`_ Segments, Then:
1. OSX: _`/usr/local/go/bin`_ (Package Installer)
1. OSX: _`/usr/local/bin`_ (Homebrew)
1. Windows: _`C:\Go\bin`_ (Package Installer)

---

# So Now We Can Find:

1. `go`
1. `godoc`
1. `gofmt`
1. `vet`
1. `cover`

---

# But What About:

1. `goimports`
1. `golint`
1. `oracle`
1. And Other `$GOPATH` / `%GOPATH%` Bin Executables?

_They aren't in `GOTOOLDIR` or `GOROOT`..._

---

# They Be Here, Somewhere:

1. Start With _`$PATH` / `%PATH%`_ Segments, Then:
1. Look In _`$GOBIN` / `%GOBIN%`_
1. Look In _`$GOPATH` / `%GOPATH%`_ Segments In The _bin_ Directory

---

# [fit] And then if you can't find them, offer to:

# [fit] _`go get -u`_

# [fit] the required tools!

# [fit] _(There is no magic, this can be disabled)_

---

# [fit] This revelation led to `go-plus` v2

## [fit] _(Plus a load of other internal awesomeness)_

## [fit] To Prepare For The Addition Of:

---

# [fit] Autocomplete

# [fit] _(Powered By `gocode`)_

---

# [fit] Oracle

# [fit] _(Powered By `oracle`)_ ;)

---

# [fit] Go To Definition

# [fit] _(Powered By `godef`)_

---

# [fit] Go To Documentation

# [fit] _(Powered By `godoc`)_

---

# [fit] And `ctags` Support

# [fit] _(Powered By `gotags`)_

---

# [fit] Also

# [fit] _The Package Is Written In CoffeeScript_

## [fit] **(Yeah, I Made A Few Mistakes As I Learned CoffeeScript)**

## [fit] _Is This As Ironic To You As It Is To Me?_

---

# [fit] And On That Bombshell...

# [fit] **_Goodnight_**

# [fit] Got Any Questions?

## _twitter: @joefitzgerald_
