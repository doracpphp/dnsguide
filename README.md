Building a DNS server in Rust
=============================

The internet has a rich conceptual foundation, with many exciting ideas that
enable it to function as we know it. One of the really cool ones is DNS. Before
it was invented, everyone on the internet - which admittedly wasn't that many at
that stage - relied on a shared file called HOSTS.TXT, maintained by the Stanford
Research Institute. This file was synchronized manually through FTP, and as the
number of hosts grew, so did the rate of change and the unfeasibility of the
system. In 1983, Paul Mockapetris set out to find a long term solution to the
problem and went on to design and implement DNS. It's a testament to his
genius that his creation has been able to scale from a few thousand
computers to the Internet as we know it today.

インターネットは豊かな概念的基盤を持っており、私たちが知っているように機能することを可能にする多くのエキサイティングなアイデアを持っています。その中でも特に素晴らしいのがDNSです。DNSが発明される前は、インターネット上の誰もが（その段階ではそれほど多くはなかったと思いますが）、スタンフォード研究所が管理するHOSTS.TXTという共有ファイルに依存していました。このファイルはFTPで手動で同期されており、ホストの数が増えるにつれて、変更の速度も上がり、システムの実現性も低くなっていました。1983年、Paul Mockapetrisはこの問題に対する長期的な解決策を見出すことに着手し、DNSの設計と実装に踏み切りました。彼の創造物が、数千台のコンピュータから今日のインターネットに至るまで拡張できたのは、彼の天才的な才能を証明するものです。

With the combined goal of gaining a deep understanding of DNS, of doing
something interesting with Rust, and of scratching some of my own itches,
I originally set out to implement my own DNS server. This document is not
a truthful chronicle of that journey, but rather an idealized version of it,
without all the detours I ended up taking. We'll gradually implement a full
DNS server, starting from first principles.

DNSを深く理解すること、Rustで何か面白いことをすること、そして自分自身の痒いところを掻くこと、これらを兼ねて私はもともと自分自身のDNSサーバを実装することに着手していました。このドキュメントは、その旅の真実の記録ではなく、むしろ理想化されたもので、私が結局取ったすべての回り道を除いたものです。第一原理から始めて、徐々に完全なDNSサーバを実装していく予定です。


 * [Chapter 1 - The DNS protocol](/chapter1.md)
 * [Chapter 2 - Building a stub resolver](/chapter2.md)
 * [Chapter 3 - Adding more Record Types](/chapter3.md)
 * [Chapter 4 - Baby's first DNS server](/chapter4.md)
 * [Chapter 5 - Recursive Resolve](/chapter5.md)

Samples
-------

Each chapter has a corresponding sample which contains the full code up to
that point in the guide, named `sample1.rs` through `sample5.rs`. These can be
run using, for first chapter, `cargo run --example sample1`.

各章には、対応するサンプルがあり、そのサンプルには、その章までの全コードが含まれています。
このガイドでは、`sample1.rs`から`sample5.rs`という名前で、その時点の内容を説明しています。これらは
最初の章は、`cargo run --example sample1` で実行できます。

Revision History
----------------

 * June 2020 - Fixed a security vulnerability in `read_qname` which allowed for
   a malicious packet to trigger an infinite loop. Modernized the code to
   conform to current rust practices, and fixed various ugly inefficiencies.
 * July 2016 - Initial version
