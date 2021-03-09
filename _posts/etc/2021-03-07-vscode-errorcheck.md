---
layout: post
title: "VsCode c/c++ No such file or directory 오류해결"
subtitle: "VsCode 오류 해결"
categories: etc
tags: etc
comments: true
toc: true
typora-copy-images-to: ..\..\assets\img\postV
---





VsCode로 C/C++을 사용하려고 하던 중 아래와 같은 오류가 나왔다.

![image-20210307222021273](https://raw.githubusercontent.com/k-chan-l/blog_image_save/master//img/image-20210307222021273.png)



결론 부터 말하자면 

```json
{
   "label": "save and compile for C",
   "command": "gcc",
   "args": ["${file}", "-o", "${fileDirname}\\${fileBasenameNoExtension}"],
   "group": "build",
   "problemMatcher": {
​    "fileLocation": ["relative", "${workspaceRoot}"],
​    "pattern": {
​     "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
​     "file": 1,
​     "line": 2,
​     "column": 3,
​     "severity": 4,
​     "message": 5
​    }
   }
  }
```

해당 코드의 args 부분이 잘못 되었다. 현재 vscode의 터미널로 git-bash를 이용하는데 저 코드대로 진행을 하면 ${file}같은 부분에서 경로가 백슬래시로 나오게 된다. 백슬래시로 된 경로는 windows경로로 git-bash에서는 작동을 하지 않는다.



그래서 문제를 해결하기 위해 검색하던 중 git-bash에서 windows경로를 이용하기 위한 방법을 찾았다.

작은 따옴표로 백슬래시로 된 경로를 감싸면 해결이 된다고 한다.



아래는 고친 코드이다.

```json
{
   "label": "save and compile for C",
   "command": "gcc",
   "args": ["'${file}'", "-o", "'${fileDirname}\\${fileBasenameNoExtension}'"],
   "group": "build",
   "problemMatcher": {
​    "fileLocation": ["relative", "${workspaceRoot}"],
​    "pattern": {
​     "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning error):\\s+(.*)$",
​     "file": 1,
​     "line": 2,
​     "column": 3,
​     "severity": 4,
​     "message": 5
​    }
   }
  }
```



그후에 문제가 해결 된줄 알았으나 컴파일 후에 실행에서 문제가 생겼다.

```json
  // 바이너리 실행(Windows)
        {
            "label": "execute",
            "command": "cmd",
            "group": "test",
            "args": [
                "/C", "${fileDirname}\\${fileBasenameNoExtension}"
            ]  
        }
```

부분에서 실행이 되어야 하는데 cmd를 거치면 바로 실행되지 않고 cmd가 켜져서 정상적으로 작동이 되지 않는 문제였다.

굳이 cmd를 사용하지 않고서도 실행이 가능해서 이렇게 수정하였다.

```json
// 바이너리 실행(Windows)
    {
      "label": "execute",
      "command": "",
      "group": "test",
      "args": ["'${fileDirname}\\${fileBasenameNoExtension}.exe'"]
    }
```

command에 cmd를 없애고 파일 위치를 위처럼 '를 주어서 윈도우 경로가 정상적으로 작동되게 하였다.



그 후 디버깅에서도 오류가 났었는데 경로에 있는 한글을 전부다 영어로 바꾸니 정상적으로 작동하였다.



여담이지만 찾던 중 VsCode의 변수 변환에 대해서 알게 되었다.

## Predefined variables

The following predefined variables are supported:

- **${workspaceFolder}** - the path of the folder opened in VS Code
- **${workspaceFolderBasename}** - the name of the folder opened in VS Code without any slashes (/)
- **${file}** - the current opened file
- **${fileWorkspaceFolder}** - the current opened file's workspace folder
- **${relativeFile}** - the current opened file relative to `workspaceFolder`
- **${relativeFileDirname}** - the current opened file's dirname relative to `workspaceFolder`
- **${fileBasename}** - the current opened file's basename
- **${fileBasenameNoExtension}** - the current opened file's basename with no file extension
- **${fileDirname}** - the current opened file's dirname
- **${fileExtname}** - the current opened file's extension
- **${cwd}** - the task runner's current working directory on startup
- **${lineNumber}** - the current selected line number in the active file
- **${selectedText}** - the current selected text in the active file
- **${execPath}** - the path to the running VS Code executable
- **${defaultBuildTask}** - the name of the default build task
- **${pathSeparator}** - the character used by the operating system to separate components in file paths

### Predefined variables examples

Supposing that you have the following requirements:

1. A file located at `/home/your-username/your-project/folder/file.ext` opened in your editor;
2. The directory `/home/your-username/your-project` opened as your root workspace.

So you will have the following values for each variable:

- **${workspaceFolder}** - `/home/your-username/your-project`
- **${workspaceFolderBasename}** - `your-project`
- **${file}** - `/home/your-username/your-project/folder/file.ext`
- **${fileWorkspaceFolder}** - `/home/your-username/your-project`
- **${relativeFile}** - `folder/file.ext`
- **${relativeFileDirname}** - `folder`
- **${fileBasename}** - `file.ext`
- **${fileBasenameNoExtension}** - `file`
- **${fileDirname}** - `/home/your-username/your-project/folder`
- **${fileExtname}** - `.ext`
- **${lineNumber}** - line number of the cursor
- **${selectedText}** - text selected in your code editor
- **${execPath}** - location of Code.exe
- **${pathSeparator}** - `/` on macOS or linux, `\\` on Windows



이게 VsCode에서만 사용이 가능한건지 아니면 모든 json파일에 적용되는 건지는 모르겠다. 후자일 경우 나중에 유용하게 사용할 것 같아서 이렇게 적어둔다.