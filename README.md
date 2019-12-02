# debugger-playground


[![CircleCI](https://circleci.com/gh/yourgithubhandle/debugger-playground/tree/master.svg?style=svg)](https://circleci.com/gh/yourgithubhandle/debugger-playground/tree/master)


**Contains the following libraries and executables:**

```
debugger-playground@0.0.0
│
├─test/
│   name:    TestDebuggerPlayground.exe
│   require: debugger-playground/library
│
├─library/
│   library name: debugger-playground/library
│   require:
│
└─executable/
    name:    DebuggerPlaygroundApp.exe
    require: debugger-playground/library
```

## Developing:

```
npm install -g esy
git clone <this-repo>
esy install
esy build
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
