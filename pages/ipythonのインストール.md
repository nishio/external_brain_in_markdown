
2022-12-04
親切にも「パスが通ってないから通せ」と言ってくれる
:

```
% pip3 install ipython     
Defaulting to user installation because normal site-packages is not writeable
Collecting ipython
...
WARNING: The scripts ipython, ipython3 and ipython3.10 are installed in '/Users/nishio/Library/Python/3.9/bin' which is not on PATH.
```

[[Defaulting to user installation because normal site-packages is not writeable]]

ちなみにsudoで入れようとすると「システムのパッケージマネージャとぶつかるからそういうことをしてはいけない」と諭して無視する、親切。
:

```
% sudo pip3 uninstall ipython
Password:
...
WARNING: Skipping ipython as it is not installed.
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```


というわけで素直にパスを通しました
.zshrc

```
export PATH=$PATH:/Users/nishio/Library/Python/3.9/bin
```

