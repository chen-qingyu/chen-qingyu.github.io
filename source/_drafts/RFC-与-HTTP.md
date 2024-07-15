---
title: RFC 与 HTTP
date: 2024-07-15
---

使用基于 UDP 的 QUIC（RFC9000）实现的 HTTP/3（RFC9114）在 2022 已成为提案标准。计算机网络教科书里关于 http 的部分可以更新了……

说“HTTP/1.1”是基于 TCP 的没错，但说“HTTP”是基于 TCP 的就有问题了。

现行的互联网标准是 HTTP/1.1(RFC 9112) / HTTP/2.0 (RFC 9113)

HTTP/0.9 的请求标头是 GET /page.html ，并没有版本信息，后来 1.0 标准化之后才在后面添加的版本信息，所以形成了 GET /page.html HTTP/1.1 这样的顺序。但是响应是 HTTP/1.1 404 Not Found 这样的，版本信息又在前面，简直逼死强迫症……

Accept 和 Content-Type 不对称，Accept 应该叫 Accept-Type，和 Accept-Language 等格式也一致。逼死强迫症+2

[ETag](https://www.rfc-editor.org/rfc/rfc9110#field.etag) 表示 entity-tag 应该叫 Entity-Tag 表示实体资源，逼死强迫症+3

参考：

9114 HTTP/3 M. Bishop [ June 2022 ] (HTML, TEXT, PDF, XML) (Status: PROPOSED STANDARD) (Stream: IETF, Area: wit, WG: quic) (DOI: 10.17487/RFC9114)
9113 HTTP/2 M. Thomson, C. Benfield [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC7540, RFC8740) (Status: PROPOSED STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9113)
9112 HTTP/1.1 R. Fielding, M. Nottingham, J. Reschke [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC7230) (Also STD0099) (Status: INTERNET STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9112)
9111 HTTP Caching R. Fielding, M. Nottingham, J. Reschke [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC7234) (Also STD0098) (Status: INTERNET STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9111)
9110 HTTP Semantics R. Fielding, M. Nottingham, J. Reschke [ June 2022 ] (HTML, TEXT, PDF, XML) (Obsoletes RFC2818, RFC7230, RFC7231, RFC7232, RFC7233, RFC7235, RFC7538, RFC7615, RFC7694) (Updates RFC3864) (Also STD0097) (Status: INTERNET STANDARD) (Stream: IETF, Area: wit, WG: httpbis) (DOI: 10.17487/RFC9110)
