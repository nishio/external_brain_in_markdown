---
title: "Jupyter Notebook"
---

- ブレークポイント
    - 昔 `import pdb; pdb.set_trace()`してたようなことは`import IPython; IPython.embed()`でできる
    - Jupyterに限らずコンソールでスクリプトを実行するときでも使える
- Post-mortem
    - 普通のスクリプトでは -mpdbで例外発生時にpdbでの対話的デバッグに入る
    - コンソールのipythonでは%pdbしておくことで同様
    - Jupyter Notebookでは例外発生後に%debugで対話的デバッグに入れる
- プロファイリング
    - %timeit %%timeit: timeit
    - %prun %%prun: cProfile
    - line_profiler memory_profiler
        - !pip install line_profiler memory_profiler
        - %load_ext line_profiler
        - %load_ext memory_profiler

