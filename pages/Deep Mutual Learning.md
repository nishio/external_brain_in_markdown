
> Model distillation is an effective and widely used technique to transfer knowledge from a teacher to a student network. The typical application is to transfer from a powerful large network or ensemble to a small network, that is better suited to low-memory or fast execution requirements. In this paper, we present a deep mutual learning (DML) strategy where, rather than one way transfer between a static pre-defined teacher and a student, an ensemble of students learn collaboratively and teach each other throughout the training process. Our experiments show that a variety of network architectures benefit from mutual learning and achieve compelling results on CIFAR-100 recognition and Market-1501 person re-identification benchmarks. Surprisingly, it is revealed that no prior powerful teacher network is necessary -- mutual learning of a collection of simple student networks works, and moreover outperforms distillation from a more powerful yet static teacher.
[https://arxiv.org/abs/1706.00384](https://arxiv.org/abs/1706.00384)

- 強い教師モデルと、弱い生徒モデルをおく[[蒸留]]と異なり、弱い生徒モデルが複数、互いの出力の差を減らすように学習することで

[[Mutual Learning]]

- [Deep Mutual Learning (arxiv) - (iwi) 備忘録](http://iwiwi.hatenadiary.jp/entry/2017/12/13/121006)
