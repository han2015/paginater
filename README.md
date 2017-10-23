Paginater [![Build Status](https://travis-ci.org/Unknwon/paginater.svg?branch=master)](https://travis-ci.org/Unknwon/paginater)
=========

Package paginater is a helper module for custom pagination calculation.

## Installation

	go get github.com/Unknwon/paginater

## Getting Started

The following code shows an example of how to use paginater:

```go
package main

import "github.com/Unknwon/paginater"

func main() {
	// Arguments:
	// - Total number of rows
	// - Number of rows in one page
	// - Current page number 
	// - Number of page links to be displayed
	p := paginater.New(45, 10, 3, 3)
	
	// Then use p as a template object named "Page" in "demo.html"
	// ...
}
```

`demo.html`

```html
{{if gt .Page.TotalPages 1}}
    <div class="pagination">
        <div class="page-container clearfix">
            {{$prefix:=.PageListURL}}
            {{if .Page.HasPrevious}}<div class="page-link-prev fl"><a href='{{printf "%s%v" $prefix .Page.Previous}}'></a></div>{{end}}
            <div class="page-links fl">
            {{range .Page.Pages}}
                {{if le .Num 0}}
                {{else}}
                    {{if .IsCurrent}}
                        <strong>{{.Num}}</strong>
                    {{else}}
                        <a href='{{printf "%s%v" $prefix .Num}}'>{{.Num}}</a>
                    {{end}}
                {{end}}
            {{end}}
            </div>
            {{if .Page.HasNext}}<div class="page-link-next fl"><a href='{{printf "%s%v" $prefix .Page.Next}}'></a></div>{{end}}
        </div>
    </div>
    {{end}}
```

Possible output:

```
[First](1) [Previous](2) ... 2 3(current) 4 ... [Next](4) [Last](5)
```

As you may guess, if the `Page` value is `-1`, you should print `...` in the HTML as common practice.

## Getting Help

- [API Documentation](https://gowalker.org/github.com/Unknwon/paginater)
- [File An Issue](https://github.com/Unknwon/paginater/issues/new)

## License

This project is under Apache v2 License. See the [LICENSE](LICENSE) file for the full license text.
