---
title: "Github Actionsのアクション間でコード共有"
---

[[GPT4に技術を聞く]]
複数のアクションで共有したいコードがあるけど、どうするのがいいと思う？って聞いたらこれでいいだろと言われた
:

```
- name: Run Script 1
  run: |
    # Add the library to the PYTHONPATH so that you can import it
    export PYTHONPATH=$PYTHONPATH:$GITHUB_WORKSPACE/shared_lib
    python .github/actions/script1.py

- name: Run Script 2
  run: |
    # Again, add the library to the PYTHONPATH
    export PYTHONPATH=$PYTHONPATH:$GITHUB_WORKSPACE/shared_lib
    python .github/actions/script2.py
```


exportは1回でいいよね？と聞いたら1回になった
:

```

 # Set environment variables for all steps in this job
 env:
   PYTHONPATH: ${{ github.workspace }}/shared_lib
```


それじゃダメだよね？と聞いた

:

```
    # Retrieve and update PYTHONPATH for all steps in this job
    env:
      ORIGINAL_PYTHONPATH: ${{ steps.setup.outputs.pythonpath }}
      PYTHONPATH: ${{ steps.setup.outputs.pythonpath }}:${{ github.workspace }}/shared_lib

    steps:
    - name: Get original PYTHONPATH
      id: setup
      run: echo "::set-output name=pythonpath::$(python -c 'import sys; print(":".join(sys.path))')"
```


うーん、イマイチだね
