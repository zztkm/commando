# Commando

Commando is a framework for batch processing.

コマンドラインツールを脳筋で実行していくバッチ処理のためのフレームワーク。
基本的にPythonの構文でワークフローを構築できるので、バッチ処理での変数の取り回しなどがしやすいのがメリット。

Shell Script や Bat ファイルを書かなくても実行したいコマンドさえわかっていればバッチ処理が書ける。

## Concept 
- バッチ処理ワークフローを構築するためのフレームワーク
- 逐次処理で書く
- 外部コマンドに関しては subprocess.run()が走る


## Feature
- `add()`
    - add command
- `execute(): `
    - Execute the added command.
- Process them in the order they were added.
- Functions can also be executed as commands

## Usage

install
```shell
pip install pycommando
```

script
```python
import logging

from commando import commando

logging.basicConfig(filename="test.log", level=logging.DEBUG)


def zero():
    1 / 0


commando.add("mkdir test")
commando.add("touch test\\test.txt")
commando.add(zero)

commando.execute()
```

log
```log
DEBUG:commando.commando:mkdir test
DEBUG:commando.commando:touch test\test.txt
DEBUG:commando.commando:<function zero at 0x01A177C0>
ERROR:commando.commando:Could not execute function
Traceback (most recent call last):
  File "C:\Users\takum\dev\pydev\commando\commando\commando.py", line 29, in execute
    cmd()
  File "main.py", line 9, in zero
    1 / 0
ZeroDivisionError: division by zero
```
