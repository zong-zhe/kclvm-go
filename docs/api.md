<!-- Code generated by gomarkdoc. DO NOT EDIT -->

# kclvm

```go
import "kcl-lang.io/kcl-go"
```

Package kclvm

KCL Go SDK

```
┌─────────────────┐         ┌─────────────────┐           ┌─────────────────┐
│     kcl files   │         │    KCL-Go-API   │           │  KCLResultList  │
│  ┌───────────┐  │         │                 │           │                 │
│  │    1.k    │  │         │                 │           │                 │
│  └───────────┘  │         │                 │           │  ┌───────────┐  │         ┌───────────────┐
│  ┌───────────┐  │         │  ┌───────────┐  │           │  │ KCLResult │──┼────────▶│x.Get("a.b.c") │
│  │    2.k    │  │         │  │ Run(path) │  │           │  └───────────┘  │         └───────────────┘
│  └───────────┘  │────┐    │  └───────────┘  │           │                 │
│  ┌───────────┐  │    │    │                 │           │  ┌───────────┐  │         ┌───────────────┐
│  │    3.k    │  │    │    │                 │           │  │ KCLResult │──┼────────▶│x.Get("k", &v) │
│  └───────────┘  │    │    │                 │           │  └───────────┘  │         └───────────────┘
│  ┌───────────┐  │    ├───▶│  ┌───────────┐  │──────────▶│                 │
│  │setting.yml│  │    │    │  │RunFiles() │  │           │  ┌───────────┐  │         ┌───────────────┐
│  └───────────┘  │    │    │  └───────────┘  │           │  │ KCLResult │──┼────────▶│x.JSONString() │
└─────────────────┘    │    │                 │           │  └───────────┘  │         └───────────────┘
                       │    │                 │           │                 │
┌─────────────────┐    │    │                 │           │  ┌───────────┐  │         ┌───────────────┐
│     Options     │    │    │  ┌───────────┐  │           │  │ KCLResult │──┼────────▶│x.YAMLString() │
│WithOptions      │    │    │  │MustRun()  │  │           │  └───────────┘  │         └───────────────┘
│WithOverrides    │────┘    │  └───────────┘  │           │                 │
│WithWorkDir      │         │                 │           │                 │
│WithDisableNone  │         │                 │           │                 │
└─────────────────┘         └─────────────────┘           └─────────────────┘
```

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	const k_code = `
name = "kcl"
age = 1

two = 2

schema Person:
    name: str = "kcl"
    age: int = 1

x0 = Person {}
x1 = Person {
	age = 101
}
`

	yaml := kcl.MustRun("testdata/main.k", kcl.WithCode(k_code)).First().YAMLString()
	fmt.Println(yaml)

	fmt.Println("----")

	result := kcl.MustRun("./testdata/main.k").First()
	fmt.Println(result.JSONString())

	fmt.Println("----")
	fmt.Println("x0.name:", result.Get("x0.name"))
	fmt.Println("x1.age:", result.Get("x1.age"))

	fmt.Println("----")

	var person struct {
		Name string
		Age  int
	}
	fmt.Printf("person: %+v\n", result.Get("x1", &person))
}
```

</p>
</details>

## Index

- [Constants](<#constants>)
- [func FormatCode\(code interface\{\}\) \(\[\]byte, error\)](<#FormatCode>)
- [func FormatPath\(path string\) \(changedPaths \[\]string, err error\)](<#FormatPath>)
- [func GetSchemaTypeMapping\(filename string, src any, schemaName string\) \(map\[string\]\*KclType, error\)](<#GetSchemaTypeMapping>)
- [func InitKclvmPath\(kclvmRoot string\)](<#InitKclvmPath>)
- [func InitKclvmRuntime\(n int\)](<#InitKclvmRuntime>)
- [func LintPath\(paths \[\]string\) \(results \[\]string, err error\)](<#LintPath>)
- [func ListDepFiles\(workDir string, opt \*ListDepFilesOption\) \(files \[\]string, err error\)](<#ListDepFiles>)
- [func ListDownStreamFiles\(workDir string, opt \*ListDepsOptions\) \(\[\]string, error\)](<#ListDownStreamFiles>)
- [func ListUpStreamFiles\(workDir string, opt \*ListDepsOptions\) \(deps \[\]string, err error\)](<#ListUpStreamFiles>)
- [func OverrideFile\(file string, specs, importPaths \[\]string\) \(bool, error\)](<#OverrideFile>)
- [func Validate\(dataFile, schemaFile string, opts \*ValidateOptions\) \(ok bool, err error\)](<#Validate>)
- [func ValidateCode\(data, code string, opts \*ValidateOptions\) \(ok bool, err error\)](<#ValidateCode>)
- [type KCLResult](<#KCLResult>)
- [type KCLResultList](<#KCLResultList>)
  - [func MustRun\(path string, opts ...Option\) \*KCLResultList](<#MustRun>)
  - [func Run\(path string, opts ...Option\) \(\*KCLResultList, error\)](<#Run>)
  - [func RunFiles\(paths \[\]string, opts ...Option\) \(\*KCLResultList, error\)](<#RunFiles>)
- [type KclType](<#KclType>)
  - [func GetSchemaType\(filename string, src any, schemaName string\) \(\[\]\*KclType, error\)](<#GetSchemaType>)
- [type ListDepFilesOption](<#ListDepFilesOption>)
- [type ListDepsOptions](<#ListDepsOptions>)
- [type Option](<#Option>)
  - [func WithCode\(codes ...string\) Option](<#WithCode>)
  - [func WithDisableNone\(disableNone bool\) Option](<#WithDisableNone>)
  - [func WithExternalPkgs\(externalPkgs ...string\) Option](<#WithExternalPkgs>)
  - [func WithFullTypePath\(fullTypePath bool\) Option](<#WithFullTypePath>)
  - [func WithIncludeSchemaTypePath\(includeSchemaTypePath bool\) Option](<#WithIncludeSchemaTypePath>)
  - [func WithKFilenames\(filenames ...string\) Option](<#WithKFilenames>)
  - [func WithLogger\(l io.Writer\) Option](<#WithLogger>)
  - [func WithOptions\(key\_value\_list ...string\) Option](<#WithOptions>)
  - [func WithOverrides\(override\_list ...string\) Option](<#WithOverrides>)
  - [func WithPrintOverridesAST\(printOverridesAST bool\) Option](<#WithPrintOverridesAST>)
  - [func WithSelectors\(selectors ...string\) Option](<#WithSelectors>)
  - [func WithSettings\(filename string\) Option](<#WithSettings>)
  - [func WithShowHidden\(showHidden bool\) Option](<#WithShowHidden>)
  - [func WithSortKeys\(sortKeys bool\) Option](<#WithSortKeys>)
  - [func WithWorkDir\(workDir string\) Option](<#WithWorkDir>)
- [type TestCaseInfo](<#TestCaseInfo>)
- [type TestOptions](<#TestOptions>)
- [type TestResult](<#TestResult>)
  - [func Test\(testOpts \*TestOptions, opts ...Option\) \(TestResult, error\)](<#Test>)
- [type ValidateOptions](<#ValidateOptions>)


## Constants

<a name="KclvmAbiVersion"></a>KclvmAbiVersion is the current kclvm ABI version.

```go
const KclvmAbiVersion = scripts.KclvmAbiVersion
```

<a name="FormatCode"></a>
## func [FormatCode](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L143>)

```go
func FormatCode(code interface{}) ([]byte, error)
```

FormatCode returns the formatted code.

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"
	"log"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	out, err := kcl.FormatCode(`a  =  1+2`)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(string(out))

}
```

#### Output

```
a = 1 + 2
```

</p>
</details>

<a name="FormatPath"></a>
## func [FormatPath](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L155>)

```go
func FormatPath(path string) (changedPaths []string, err error)
```

FormatPath formats files from the given path path: if path is \`.\` or empty string, all KCL files in current directory will be formatted, not recursively if path is \`path/file.k\`, the specified KCL file will be formatted if path is \`path/to/dir\`, all KCL files in the specified dir will be formatted, not recursively if path is \`path/to/dir/...\`, all KCL files in the specified dir will be formatted recursively

the returned changedPaths are the changed file paths \(relative path\)

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"
	"log"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	changedPaths, err := kcl.FormatPath("testdata/fmt")
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(changedPaths)
}
```

</p>
</details>

<a name="GetSchemaTypeMapping"></a>
## func [GetSchemaTypeMapping](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L237>)

```go
func GetSchemaTypeMapping(filename string, src any, schemaName string) (map[string]*KclType, error)
```

GetSchemaTypeMapping returns a \<schemaName\>:\<schemaType\> mapping of schema types from a kcl file or code.

file: string

```
The kcl filename
```

code: string

```
The kcl code string
```

schema\_name: string

```
The schema name got, when the schema name is empty, all schemas are returned.
```

<a name="InitKclvmPath"></a>
## func [InitKclvmPath](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L61>)

```go
func InitKclvmPath(kclvmRoot string)
```

InitKclvmPath init kclvm path.

<a name="InitKclvmRuntime"></a>
## func [InitKclvmRuntime](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L66>)

```go
func InitKclvmRuntime(n int)
```

InitKclvmRuntime init kclvm process.

<a name="LintPath"></a>
## func [LintPath](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L175>)

```go
func LintPath(paths []string) (results []string, err error)
```

LintPath lint files from the given path

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"
	"log"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	// import a
	// import a # reimport

	results, err := kcl.LintPath([]string{"testdata/lint/import.k"})
	if err != nil {
		log.Fatal(err)
	}
	for _, s := range results {
		fmt.Println(s)
	}

}
```

#### Output

```
Module 'a' is reimported multiple times
Module 'a' imported but unused
Module 'a' imported but unused
```

</p>
</details>

<a name="ListDepFiles"></a>
## func [ListDepFiles](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L160>)

```go
func ListDepFiles(workDir string, opt *ListDepFilesOption) (files []string, err error)
```

ListDepFiles return the depend files from the given path

<a name="ListDownStreamFiles"></a>
## func [ListDownStreamFiles](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L170>)

```go
func ListDownStreamFiles(workDir string, opt *ListDepsOptions) ([]string, error)
```

ListDownStreamFiles return a list of downstream depend files from the given changed path list.

<a name="ListUpStreamFiles"></a>
## func [ListUpStreamFiles](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L165>)

```go
func ListUpStreamFiles(workDir string, opt *ListDepsOptions) (deps []string, err error)
```

ListUpStreamFiles return a list of upstream depend files from the given path list

<a name="OverrideFile"></a>
## func [OverrideFile](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L187>)

```go
func OverrideFile(file string, specs, importPaths []string) (bool, error)
```

OverrideFile rewrites a file with override spec file: string. The File that need to be overridden specs: \[\]string. List of specs that need to be overridden.

```
Each spec string satisfies the form: <pkgpath>:<field_path>=<filed_value> or <pkgpath>:<field_path>-
When the pkgpath is '__main__', it can be omitted.
```

importPaths. List of import statements that need to be added

<a name="Validate"></a>
## func [Validate](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L198>)

```go
func Validate(dataFile, schemaFile string, opts *ValidateOptions) (ok bool, err error)
```

Validate validates the given data file against the specified schema file with the provided options.

<a name="ValidateCode"></a>
## func [ValidateCode](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L192>)

```go
func ValidateCode(data, code string, opts *ValidateOptions) (ok bool, err error)
```

ValidateCode validate data string match code string

<a name="KCLResult"></a>
## type [KCLResult](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L54>)



```go
type KCLResult = kcl.KCLResult
```

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	const k_code = `
name = "kcl"
age = 1
	
two = 2
	
schema Person:
    name: str = "kcl"
    age: int = 1

x0 = Person {name = "kcl-go"}
x1 = Person {age = 101}
`

	result := kcl.MustRun("testdata/main.k", kcl.WithCode(k_code)).First()

	fmt.Println("x0.name:", result.Get("x0.name"))
	fmt.Println("x1.age:", result.Get("x1.age"))

}
```

#### Output

```
x0.name: kcl-go
x1.age: 101
```

</p>
</details>

<details><summary>Example ('et_struct)</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	const k_code = `
schema Person:
    name: str = "kcl"
    age: int = 1
    X: int = 2

x = {
    "a": Person {age = 101}
    "b": 123
}
`

	result := kcl.MustRun("testdata/main.k", kcl.WithCode(k_code)).First()

	var person struct {
		Name string
		Age  int
	}
	fmt.Printf("person: %+v\n", result.Get("x.a", &person))
	fmt.Printf("person: %+v\n", person)

}
```

#### Output

```
person: &{Name:kcl Age:101}
person: {Name:kcl Age:101}
```

</p>
</details>

<a name="KCLResultList"></a>
## type [KCLResultList](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L55>)



```go
type KCLResultList = kcl.KCLResultList
```

<a name="MustRun"></a>
### func [MustRun](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L71>)

```go
func MustRun(path string, opts ...Option) *KCLResultList
```

MustRun is like Run but panics if return any error.

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	yaml := kcl.MustRun("testdata/main.k", kcl.WithCode(`name = "kcl"`)).First().YAMLString()
	fmt.Println(yaml)

}
```

#### Output

```
name: kcl
```

</p>
</details>

<details><summary>Example (Raw Yaml)</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	const code = `
b = 1
a = 2
`
	yaml := kcl.MustRun("testdata/main.k", kcl.WithCode(code)).GetRawYamlResult()
	fmt.Println(yaml)

	yaml_sorted := kcl.MustRun("testdata/main.k", kcl.WithCode(code), kcl.WithSortKeys(true)).GetRawYamlResult()
	fmt.Println(yaml_sorted)

}
```

#### Output

```
b: 1
a: 2
a: 2
b: 1
```

</p>
</details>

<details><summary>Example (Schema Type)</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	const code = `
schema Person:
	name: str = ""

x = Person()
`
	json := kcl.MustRun("testdata/main.k", kcl.WithCode(code)).First().JSONString()
	fmt.Println(json)

}
```

#### Output

```
{
    "x": {
        "name": ""
    }
}
```

</p>
</details>

<details><summary>Example (Settings)</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	yaml := kcl.MustRun("./testdata/app0/kcl.yaml").First().YAMLString()
	fmt.Println(yaml)
}
```

</p>
</details>

<a name="Run"></a>
### func [Run](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L76>)

```go
func Run(path string, opts ...Option) (*KCLResultList, error)
```

Run evaluates the KCL program with path and opts, then returns the object list.

<a name="RunFiles"></a>
### func [RunFiles](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L81>)

```go
func RunFiles(paths []string, opts ...Option) (*KCLResultList, error)
```

RunFiles evaluates the KCL program with multi file path and opts, then returns the object list.

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	result, _ := kcl.RunFiles([]string{"./testdata/app0/kcl.yaml"})
	fmt.Println(result.First().YAMLString())
}
```

</p>
</details>

<a name="KclType"></a>
## type [KclType](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L57>)



```go
type KclType = kcl.KclType
```

<a name="GetSchemaType"></a>
### func [GetSchemaType](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L220>)

```go
func GetSchemaType(filename string, src any, schemaName string) ([]*KclType, error)
```

GetSchemaType returns schema types from a kcl file or code.

file: string

```
The kcl filename
```

code: string

```
The kcl code string
```

schema\_name: string

```
The schema name got, when the schema name is empty, all schemas are returned.
```

<a name="ListDepFilesOption"></a>
## type [ListDepFilesOption](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L49>)



```go
type ListDepFilesOption = list.Option
```

<a name="ListDepsOptions"></a>
## type [ListDepsOptions](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L48>)



```go
type ListDepsOptions = list.DepOptions
```

<a name="Option"></a>
## type [Option](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L47>)



```go
type Option = kcl.Option
```

<a name="WithCode"></a>
### func [WithCode](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L86>)

```go
func WithCode(codes ...string) Option
```

WithCode returns a Option which hold a kcl source code list.

<a name="WithDisableNone"></a>
### func [WithDisableNone](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L110>)

```go
func WithDisableNone(disableNone bool) Option
```

WithDisableNone returns a Option which hold a disable none switch.

<a name="WithExternalPkgs"></a>
### func [WithExternalPkgs](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L89>)

```go
func WithExternalPkgs(externalPkgs ...string) Option
```

WithExternalPkgs returns a Option which hold a external package list.

<a name="WithFullTypePath"></a>
### func [WithFullTypePath](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L118>)

```go
func WithFullTypePath(fullTypePath bool) Option
```

WithFullTypePath returns a Option which hold a include full type string in the \`\_type\` attribute.

<a name="WithIncludeSchemaTypePath"></a>
### func [WithIncludeSchemaTypePath](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L113>)

```go
func WithIncludeSchemaTypePath(includeSchemaTypePath bool) Option
```

WithIncludeSchemaTypePath returns a Option which hold a include schema type path switch.

<a name="WithKFilenames"></a>
### func [WithKFilenames](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L92>)

```go
func WithKFilenames(filenames ...string) Option
```

WithKFilenames returns a Option which hold a filenames list.

<a name="WithLogger"></a>
### func [WithLogger](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L138>)

```go
func WithLogger(l io.Writer) Option
```

WithLogger returns a Option which hold a logger.

<a name="WithOptions"></a>
### func [WithOptions](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L95>)

```go
func WithOptions(key_value_list ...string) Option
```

WithOptions returns a Option which hold a key=value pair list for option function.

<details><summary>Example</summary>
<p>



```go
package main

import (
	"fmt"
	"log"

	kcl "kcl-lang.io/kcl-go"
)

func main() {
	const code = `
name = option("name")
age = option("age")
`
	x, err := kcl.Run("hello.k", kcl.WithCode(code),
		kcl.WithOptions("name=kcl", "age=1"),
	)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println(x.First().YAMLString())

}
```

#### Output

```
age: 1
name: kcl
```

</p>
</details>

<a name="WithOverrides"></a>
### func [WithOverrides](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L98>)

```go
func WithOverrides(override_list ...string) Option
```

WithOverrides returns a Option which hold a override list.

<a name="WithPrintOverridesAST"></a>
### func [WithPrintOverridesAST](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L123>)

```go
func WithPrintOverridesAST(printOverridesAST bool) Option
```

WithPrintOverridesAST returns a Option which hold a printOverridesAST switch.

<a name="WithSelectors"></a>
### func [WithSelectors](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L101>)

```go
func WithSelectors(selectors ...string) Option
```

WithSelectors returns a Option which hold a path selector list.

<a name="WithSettings"></a>
### func [WithSettings](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L104>)

```go
func WithSettings(filename string) Option
```

WithSettings returns a Option which hold a settings file.

<a name="WithShowHidden"></a>
### func [WithShowHidden](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L133>)

```go
func WithShowHidden(showHidden bool) Option
```

WithShowHidden returns a Option which holds a showHidden switch.

<a name="WithSortKeys"></a>
### func [WithSortKeys](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L128>)

```go
func WithSortKeys(sortKeys bool) Option
```

WithSortKeys returns a Option which holds a sortKeys switch.

<a name="WithWorkDir"></a>
### func [WithWorkDir](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L107>)

```go
func WithWorkDir(workDir string) Option
```

WithWorkDir returns a Option which hold a work dir.

<a name="TestCaseInfo"></a>
## type [TestCaseInfo](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L52>)



```go
type TestCaseInfo = testing.TestCaseInfo
```

<a name="TestOptions"></a>
## type [TestOptions](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L51>)



```go
type TestOptions = testing.TestOptions
```

<a name="TestResult"></a>
## type [TestResult](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L53>)



```go
type TestResult = testing.TestResult
```

<a name="Test"></a>
### func [Test](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L203>)

```go
func Test(testOpts *TestOptions, opts ...Option) (TestResult, error)
```

Test calls the test tool to run uni tests in packages.

<a name="ValidateOptions"></a>
## type [ValidateOptions](<https://github.com/kcl-lang/kcl-go/blob/main/kclvm.go#L50>)



```go
type ValidateOptions = validate.ValidateOptions
```

Generated by [gomarkdoc](<https://github.com/princjef/gomarkdoc>)
