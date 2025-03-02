
`$ pip install mecab`
ではなく
`$ pip install mecab-python3==0.996.5`
をすれば解決する
[[Heroku]] [[Mecab]]
原因については掘り下げてない

:

```
remote:        Collecting mecab==0.996.2
remote:          Downloading mecab-0.996.2.tar.gz (62 kB)
remote:            ERROR: Command errored out with exit status 1:
remote:             command: /app/.heroku/python/bin/python -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-rn_z50l9/mecab/setup.py'"'"'; __file__='"'"'/tmp/pip-install-rn_z50l9/mecab/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' egg_info --egg-base /tmp/pip-pip-egg-info-266d3ef_
remote:                 cwd: /tmp/pip-install-rn_z50l9/mecab/
remote:            Complete output (10 lines):
remote:            /bin/sh: 1: mecab-config: not found
remote:            Traceback (most recent call last):
remote:              File "<string>", line 1, in <module>
remote:              File "/tmp/pip-install-rn_z50l9/mecab/setup.py", line 53, in <module>
remote:                include_dirs=cmd2("mecab-config --inc-dir"),
remote:              File "/tmp/pip-install-rn_z50l9/mecab/setup.py", line 19, in cmd2
remote:                return cmd1(strings).split()
remote:              File "/tmp/pip-install-rn_z50l9/mecab/setup.py", line 15, in cmd1
remote:                return os.popen(strings).readlines()[0].rstrip()
remote:            IndexError: list index out of range
remote:            ----------------------------------------
remote:        ERROR: Command errored out with exit status 1: python setup.py egg_info Check the logs for full command output.
remote:  !     Push rejected, failed to compile Python app.
```

