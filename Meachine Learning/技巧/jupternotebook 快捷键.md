- `Ctrl + Shift + P`：调起快捷键

- `Esc + F` 查找和替换你的代码，但不包括代码的输出内容。

- `Esc + o` 打开代码块输出。

- 选择多个 cell。 `Shift + J` 或 `Shift + Down` 向下选中下一个cell. 你可以通过 `Shift + K` 或 `Shift + Up` 向上选中 cell。(译者：jk，与vim的移动方式一致)

  - 一旦 cell 被选中，接着你可以进行批量删除/复制/剪切/粘贴.当你需要移动一部分notebook时，这非常有用。
  - 你也可以执行 `Shift + M` (译者：m记为merge)对多个cell进行合并。

- ```
  from IPython.core.interactiveshell import InteractiveShell
  InteractiveShell.ast_node_interactivity = "all"
  ```

  设置每行的输出

- ```
  !pip list | grep pandas
  !pip list
  ```

  查看安装的包

- 安装扩展包

  ```
  pip install jupyter_contrib_nbextensions && jupyter contrib nbextension install
  ```


http://liuchengxu.org/pelican-blog/jupyter-notebook-tips.html