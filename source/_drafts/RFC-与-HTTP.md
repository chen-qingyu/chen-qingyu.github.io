---
title: RFC 与 HTTP
date: 2024-07-15
---

使用基于 UDP 的 QUIC（RFC9000）实现的 HTTP/3（RFC9114）在 2022 已成为提案标准。计算机网络教科书里关于 http 的部分可以更新了……

说“HTTP/1.1”是基于 TCP 的没错，但说“HTTP”是基于 TCP 的就有问题了。

现行的互联网标准是 HTTP/1.1(RFC 9112) / HTTP/2.0 (RFC 9113)

9114 HTTP/3 M. Bishop [ June 2022 ] (HTML, TEXT, PDF, XML) (Status: PROPOSED STANDARD) (Stream: IETF, Area: wit, WG: quic) (DOI: 10.17487/RFC9114)
9113 HTTP/2 M. Thomson, C. Benfield [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC7540, RFC8740) (Status: PROPOSED STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9113)
9112 HTTP/1.1 R. Fielding, M. Nottingham, J. Reschke [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC7230) (Also STD0099) (Status: INTERNET STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9112)
9111 HTTP Caching R. Fielding, M. Nottingham, J. Reschke [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC7234) (Also STD0098) (Status: INTERNET STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9111)
9110 HTTP Semantics R. Fielding, M. Nottingham, J. Reschke [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC2818, RFC7230, RFC7231, RFC7232, RFC7233, RFC7235, RFC7538, RFC7615, RFC7694) (Updates RFC3864) (Also STD0097) (Status: INTERNET STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9110)
