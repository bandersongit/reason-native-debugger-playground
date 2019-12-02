# debugger-playground

## Developing:

```
npm install -g esy
git clone <this-repo>
esy install
esy build
```

To generate the .bc target run
```
esy x dune build testExe/RunDebuggerPlaygroundTests.bc
```

## Running Binary:

After building the project, you can run the main binary that is produced.

```
esy x DebuggerPlaygroundApp.exe 
```

## Running Tests:

```
# Runs the "test" command in `package.json`.
esy test
```

## Debugger attempt with ocamlearlybird
I cloned https://github.com/hackwaly/vscode-ocaml-debugger and updated the package.json to provide reason breakpoints
```
 "contributes": {
    "breakpoints": [
      {
        "language": "ocaml"
      },
      {
        "language": "ocamllex"
      },
      {
        "language": "menhir"
      },
      {
        "language": "reason"
      }
    ],
```
I also added an extension host launch config
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
			"name": "Extension",
			"type": "extensionHost",
			"request": "launch",
			"runtimeExecutable": "${execPath}",
			"args": [
				"--extensionDevelopmentPath=${workspaceFolder}"
			]
		}
    ]
}
```
I hit `F5` to open an Extension Development Host VSCode sandbox, inside that sandbox I ran 

```esy x ocamlearlybird --server --port=4711```
from there I was able to hit `F5` in the extension host and I get the output of my program in the debug console. 

I am able to set breakpoints, but I cannot hit them. When trying to step over/into/through code I get errors like this:
```
benderson-mbp:debugger-playground benderson$ esy x ocamlearlybird --server --port=4711
Fatal error: exception Invalid_argument("index out of bounds")
Raised by primitive operation at file "ocaml_debug_adapter/time_travel.ml", line 87, characters 18-58
Called from file "src/core/lwt.ml", line 1930, characters 23-26
Re-raised at file "ocaml_debug_adapter/time_travel.ml", line 83, characters 4-296
Re-raised at file "ocaml_debug_adapter/time_travel.ml", line 113, characters 6-47
benderson-mbp:debugger-playground benderson$ esy x ocamlearlybird --server --port=4711
Fatal error: exception Invalid_argument("index out of bounds")
Raised by primitive operation at file "ocaml_debug_adapter/time_travel.ml", line 87, characters 18-58
Called from file "src/core/lwt.ml", line 1930, characters 23-26
```
