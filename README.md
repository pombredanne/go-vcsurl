=============================================
go-vcsurl - Lenient VCS repository URL parser
=============================================

go-vcsurl parses VCS repository URLs in many common formats.

Note: the public API is experimental and subject to change until further notice.


Usage
=====

See full package documentation at
[godoc.org/github.com/sqs/go-vcsurl](http://godoc.org/github.com/sqs/go-vcsurl).

Example: [example_test.go](https://github.com/sqs/go-vcsurl/blob/master/example_test.go):

```go
package vcsurl_test

import (
	"fmt"
	"github.com/sqs/go-vcsurl"
)

func ExampleParse() {
	urls := []string{
		"github.com/alice/libfoo",
		"git://github.com/bob/libbar",
		"code.google.com/p/libqux",
		"https://code.google.com/p/libbaz",
	}
	for i, url := range urls {
		if info, err := vcsurl.Parse(url); err == nil {
			fmt.Printf("%d. %s %s\n", i+1, info.VCS, info.CloneURL)
			fmt.Printf("   name: %s\n", info.Name)
			fmt.Printf("   host: %s\n", info.RepoHost)
		} else {
			fmt.Printf("error parsing %s\n")
		}
	}

	// output:
	// 1. git git://github.com/alice/libfoo.git
	//    name: libfoo
	//    host: github.com
	// 2. git git://github.com/bob/libbar.git
	//    name: libbar
	//    host: github.com
	// 3. hg https://code.google.com/p/libqux
	//    name: libqux
	//    host: code.google.com
	// 4. hg https://code.google.com/p/libbaz
	//    name: libbaz
	//    host: code.google.com
}
```


Running tests
=============

Run `go test`.


Contributors
============

* Quinn Slack <sqs@sourcegraph.com>
