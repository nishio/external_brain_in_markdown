
Prefabから[[インスタンス]]を作成した場合、親のPrefabを編集すると、インスタンスが変化に追従するらしい([[オーバーライド]]している場合を除く)
[https://unity3d.com/jp/learn/tutorials/projects/hajiuni/creating-collectible-objects?playlist=45986](https://unity3d.com/jp/learn/tutorials/projects/hajiuni/creating-collectible-objects?playlist=45986)

- > Select ボタンを使うと、インスタンスから生成元のプレハブアセットを選択できます。これによりメインのプレハブを編集し、その変更をインスタンス全てに適用する事が可能になります。
- > Apply ボタンを使えば、インスタンス側で変更した値を元のプレハブに上書きして保存することもできます（位置と回転の変更は除外します）。これは、どれか一つのインスタンスに加えた変更を、インスタンス全体に適用したい場合に効果的です(変更した値の上書きを除く)。また、全体的な変更を手早く簡単に行う事ができます。
- > Revert ボタンを使うと、試しにプロパティを上書き変更してみたものの、デフォルトの値の方が良かったような場合に、インスタンスを元のプレハブの値に戻すことができます。
[https://docs.unity3d.com/jp/530/Manual/Prefabs.html](https://docs.unity3d.com/jp/530/Manual/Prefabs.html)