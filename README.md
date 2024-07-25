# gopdf

gopdf is a simple library for generating PDF document written in Go lang.

A minimum version of Go 1.13 is required.

#### Features

- Unicode subfont embedding. (Chinese, Japanese, Korean, etc.)
- Draw line, oval, rect, curve
- Draw image ( jpg, png )
  - Set image mask
- Password protection
- Font [kerning](https://en.wikipedia.org/wiki/Kerning)

## Installation

```
go get -u github.com/jingcsdn/gopdf
```

### Print text to then specified page

```go

package main
import (
	"log"
	"github.com/jingcsdn/gopdf"
)

func GetImageBytes(path string) (re []byte) {
	re, _ = os.ReadFile(path)
	return
}

func main() {

	pdf := gopdf.GoPdf{}
	pdf.Start(gopdf.Config{ PageSize: *gopdf.PageSizeA4 })
	pdf.AddPage()
	err := pdf.AddTTFFont("wts11", "../ttf/wts11.ttf")
	if err != nil {
		log.Print(err.Error())
		return
	}

	err = pdf.SetFont("wts11", "", 14)
	if err != nil {
		log.Print(err.Error())
		return
	}
    //add image load from bytes
    pdf.ImageFormStream(GetImageBytes("../imgs/gopher.jpg"), 200, 50, nil) //print image index 0

    pdf.ImageFormStream(GetImageBytes("../imgs/gopher.jpg"), 200, 50, nil) //print image index 1
    
    //add set current page index 0, modify page 0 content
    pdf.SetCurPage(0)
    pdf.SetXY(10.00, 10.00)
    pdf.Text(`您好`)

    pdf.WritePdf("hello.pdf")

}

```
 
 

visit https://github.com/oneplus1000/gopdfsample for more samples.
